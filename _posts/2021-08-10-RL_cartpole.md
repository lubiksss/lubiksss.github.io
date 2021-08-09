---
last_modified_at : 2021-08-10
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

## 학습 결과
<div style = 'column-count :2;'>
<p>학습 전</p>
<img src = 'https://user-images.githubusercontent.com/67966414/128750030-1efe42b4-9d27-4ebd-aef4-b2d92dc24253.gif' alt = '학습 전' style="margin-left: auto; margin-right: auto; display: block;">
<p>학습 후</p>
<img src = 'https://user-images.githubusercontent.com/67966414/128750009-61e1297e-1fcc-423b-a314-765f83a01db3.gif' alt = '학습 후' style="margin-left: auto; margin-right: auto; display: block;">
</div>


## 생각