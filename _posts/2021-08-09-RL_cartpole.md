---
last_modified_at : 2021-08-09
layout : single
title:  "DQN을 통한 cartpole게임 학습"
categories: ML
tags : [강화학습, DQN, CartPole]

toc: true
toc_sticky: true
---
## 서론
### *참고
<ul>
    <li><a href='https://jeinalog.tistory.com/20'>강화학습 개념부터 Deep Q Networks까지, 10분만에 훑어보기</a></li>
    <li><a href='https://tutorials.pytorch.kr/intermediate/reinforcement_q_learning.html'>강화 학습 (DQN) 튜토리얼</a></li>
    <li><a href='https://wegonnamakeit.tistory.com/59'>DQN 실습 :: CartPole 게임</a></li>
</ul>
간단한 DQN모델을 통해서 CartPole게임을 pytorch를 통해 구현했습니다. 바로 아래 학습 결과를 CartPole이 쓰러지지 않고 버티는걸 볼 수 있습니다.  

DQN을 구현하는데 환경은 gym을 통해서 얻었고, NN에는 Bellman Equation, Replay Buffer, Double Deep Q Learning 개념이 사용되었습니다. 위의 참고자료를 읽어보시면 자세하게 알 수 있습니다. 저는 구현하는 게 목적이었기 때문에 이론적인 접근보다는 그 개념이 코드를 통해서 어떻게 구현되는지 기록해놓도록 하겠습니다.
## 학습 결과
<div style = 'column-count :2;'>
<p>학습 전</p>
<img src = 'https://user-images.githubusercontent.com/67966414/128750030-1efe42b4-9d27-4ebd-aef4-b2d92dc24253.gif' alt = '학습 전' style="margin-left: auto; margin-right: auto; display: block;">
<p>학습 후</p>
<img src = 'https://user-images.githubusercontent.com/67966414/128750009-61e1297e-1fcc-423b-a314-765f83a01db3.gif' alt = '학습 후' style="margin-left: auto; margin-right: auto; display: block;">
</div>

## 필요한 것
```python
import gym
from collections import deque as dq
import random

import torch
import torch.nn as nn
import torch.optim as optim
import torch.nn.functional as F

# NN를 학습시키기 위한 hyperparameter
learning_rate = 0.0005
batch_size = 32

# 감마는 할인율이라고 부르는 값으로, 미래가치에 대한 중요도를 조절합니다.
# 클수록 미래에 받을 보상에 더 큰 가치를 두는 것.
gamma = 0.98

buffer_limit = 50000
```
## Replay Buffer
```python
# 강화학습은 Training data set이라는게 따로 없다. Agent가 행동을 취하고 데이터셋을 쌓아나가야합니다.
# 그 데이터셋을 쌓기 위한 버퍼
class ReplayBuffer():
    def __init__(self):
        self.buffer = dq(maxlen=buffer_limit)
    
    # 버퍼에는 (state, action ,reward, nstate, done) 값이 들어갑니다.
    def put(self, transition):
        self.buffer.append(transition)
    
    # 샘플 함수를 만드는 이유는 버퍼에 쌓인 데이터셋에서 랜덤으로 학습을 시키기 위함입니다.
    # 그냥 연속해서 쌓인 n개의 데이터셋을 그대로 사용하면 데이터간의 상관관계가 너무 크기 때문에 학슴이 잘 안됩니다.
    def sample(self, n):
        mini_batch = random.sample(self.buffer, n)
        s_lst, a_lst, r_lst, s_prime_lst, done_mask_lst = [], [], [], [], []
        
        for transition in mini_batch:
            s, a, r, s_prime, done_mask = transition
            s_lst.append(s)
            a_lst.append([a])
            r_lst.append([r])
            s_prime_lst.append(s_prime)
            done_mask_lst.append([done_mask])

        return torch.tensor(s_lst, dtype=torch.float), torch.tensor(a_lst), \
               torch.tensor(r_lst), torch.tensor(s_prime_lst, dtype=torch.float), \
               torch.tensor(done_mask_lst)
    
    def size(self):
        return len(self.buffer)
```
## DQN
```python
# cartpole의 state가 4개고 action은 2개이기 때문에 input 4, output 2인 NN생성
# 2층짜리 NN입니다. 임의로 설계했습니다.
class Qnet(nn.Module):
    def __init__(self):
        super(Qnet, self).__init__()
        self.fc1 = nn.Linear(4, 128)
        self.fc2 = nn.Linear(128, 128)
        self.fc3 = nn.Linear(128, 2)

    def forward(self, x):
        x = F.relu(self.fc1(x))
        x = F.relu(self.fc2(x))
        x = self.fc3(x)
        return x
    
    # epsilon greedy 전략을 사용합니다.
    # 간단하게 설명하면 탐험이라는 개념을 통해서 가보지 않은 경로를 가볼 수 있게 해줍니다.
    def sample_action(self, observation, epsilon):
        out = self.forward(observation)
        coin = random.random()
        if coin < epsilon:
            return random.randint(0,1)
        else : 
            return out.argmax().item()
```
## Train
```python
def train(q, q_target, memory, optimizer):
    for i in range(10):
        s,a,r,s_prime,done_mask = memory.sample(batch_size)
        
        # 벨만함수로부터 유도된 DQN 비용함수를 구현 학습시킵니다.
        q_out = q(s)
        q_a = q_out.gather(1,a)
        max_q_prime = q_target(s_prime).max(1)[0].unsqueeze(1)
        target = r + gamma * max_q_prime * done_mask
        loss = F.smooth_l1_loss(q_a, target)
        
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()
```
## code
```python
# gym을 통한 CartPole env 생성
env = gym.make('CartPole-v1')
# Double Deep Q Learning 개념
# target_net을 semi constant로 사용
q = Qnet()
q_target = Qnet()
q_target.load_state_dict(q.state_dict())
memory = ReplayBuffer()

print_interval = 20
score = 0.0  
optimizer = optim.Adam(q.parameters(), lr=learning_rate)

for n_epi in range(500):
    epsilon = max(0.01, 0.08 - 0.01*(n_epi/200)) #Linear annealing from 8% to 1%
    s = env.reset()
    done = False

    while not done:
        a = q.sample_action(torch.from_numpy(s).float(), epsilon)      
        s_prime, r, done, info = env.step(a)
        done_mask = 0.0 if done else 1.0
        memory.put((s,a,r/100.0,s_prime, done_mask))
        s = s_prime

        score += r
        if done:
            break
    
    # 메모리가 어느정도 차야 random sample이 가능하기 때문에 일정 이상 차면 학습을 진행
    if memory.size()>2000:
        train(q, q_target, memory, optimizer)

    if n_epi%print_interval==0 and n_epi!=0:
        # 일정 주기마다 semi constant인 target-net도 업데이트.
        q_target.load_state_dict(q.state_dict())
        print("n_episode :{}, score : {:.1f}, n_buffer : {}, eps : {:.1f}%".format(
                                                        n_epi, score/print_interval, memory.size(), epsilon*100))
        score = 0.0
env.close()
```
## test
```python
state = env.reset()
state = torch.tensor(state, dtype=torch.float)
done = False

for i in range(500+1):

    if done:
        env.render()
        env.step(action)
    else:
        env.render()
        # 이부분이 위에서 학습한 모델에 state를 넣어서 취해야 하는 action을 받는 부분입니다.
        action = q.forward(state).argmax().item()
        
        state, reward, done, info = env.step(action)
        state = torch.tensor(state, dtype=torch.float)
        # print(state, done)

        if done or i==500:
            print(i)

env.close()
```

## 생각
코드의 주석으로 설명을 써놓았기 때문에 위의 참고 링크 세 개를 잘 읽어보시면 쉽게 이해하고 구현할 수 있을 거라고 생각합니다.
