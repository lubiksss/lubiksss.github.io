---
last_modified_at : 2021-10-13
layout : single
title:  "백준 스위핑 알고리즘"
categories: BOJ
tags : [스위핑, python, sweeping]

toc: true
toc_sticky: true
---
## 서론
<a href='https://www.acmicpc.net/problemset?sort=ac_desc&algo=106'>스위핑</a>

스위핑 관련 문제를 선 긋기라는 문제로 처음 접하고 나서 쭉 스위핑 관련 문제를 보았는데 풀 수가 없었습니다. 그 후에 검색을 통해서 스위핑이라는 알고리즘이 있는 것을 확인했고 스위핑 알고리즘을 학습 후에 몇 문제 풀어보았습니다.

## 스위핑 알고리즘
> 스위핑 알고리즘이란 단어의 뜻 그대로 휩쓸고 지나가며 문제를 해결하는 방식으로, 특정 기준에 따라 정렬한 후 순서대로 처리하는 알고리즘이다. 보통 문제들의 경우 인풋의 범위만큼 브루트 포스를 사용하게 되면 선분일 경우 n의 시간복잡도, 평면일 경우 n^2의 시간복잡도를 가지게 되는데 이것으로 시간초과가 될 경우 사용한다(인풋의 범위만큼 배열을 선언할 때 공간복잡도도 마찬가지). 스위핑 알고리즘은 정렬의 시간복잡도인 nlogn이 대부분이다.

## 제한 조건
<ul>
  <li>시간제한</li>
</ul>
위에서 말한 대로 보통 문제들의 경우 n이나 n^2의 시간복잡도를 가지고 이것으로 시간초과가 나는 경우 스위핑 알고리즘을 사용합니다. 보통의 스위핑 알고리즘의 경우 정렬을 기준으로 시간복잡도가 정해지기 때문에 nlogn을 가집니다. (인풋의 개수만큼 탐색하기 때문에 탐색은 n)

<ul>
  <li>메모리 제한</li>
</ul>
위에서 말한 대로 보통 문제들의 인풋 범위를 모두 선언할 때 n이나 n^2의 공간복잡도를 가지고 이것으로 메모리 초과가 나는 경우 스위핑 알고리즘을 사용합니다. 보통의 스위핑 알고리즘의 경우 인풋의 개수만큼의 데이터만 기억하기 때문에 공간복잡도는 n입니다.


## 2170번: 선긋기
스위핑에서 가장 평범한 문제로 합쳐진 선분의 길이를 구하는 문제입니다. 선분의 범위를 모두 배열로 선언해놓고 선분을 그린 부분만 더하면 쉬울 거 같은데 메모리 초과로 그런 방법은 사용할 수 없습니다. 따라서 인풋을 정렬해놓고 스위핑하며 조건에 맞게 선분의 길이를 계산해야 합니다. 여기서 특이한 점은 tuple과 list의 계산 속도가 다른 거네요…. tuple이 list보다 계산 속도가 빨라서 통과했습니다.
```python
import sys
input = sys.stdin.readline

N = int(input())
nlist = []
for __ in range(N):
    nlist.append(tuple(map(int, input().split())))
    # 이부분을 list로 하니까 시간초과가 나옴 tuple이 list보다 계산이 빠르다.
    # nlist.append(list(map(int, input().split())))
nlist.sort()

length = 0
pe = -sys.maxsize

for s, e in nlist:
    if s >= pe:
        length += (e-s)
    else:
        if e > pe:
            length += (e-pe)
    pe = max(e, pe)
print(length)
```

## 1668번: 트로피 진열
이 문제도 스위핑 문제로 분류되어있긴 한데 정확히 와닿진 않지만, reverse를 사용해서 정렬했고 그 후에 카운팅을 했기 때문인 거 같습니다.
```python
import sys
input = sys.stdin.readline

N = int(input())
tlist = []
for __ in range(N):
    tlist.append(int(input()))

cnt = 1
top = tlist[0]
for t in tlist:
    if t > top:
        cnt += 1
    top = max(t, top)

tlist.reverse()
rcnt = 1
top = tlist[0]
for t in tlist:
    if t > top:
        rcnt += 1
    top = max(t, top)

print(cnt)
print(rcnt)
```

## 2672번: 여러 직사각형의 전체 면적 구하기
제가 생각하기에 가장 sweeping 다웠다고 생각한 문제입니다. 인풋의 범위가 x, y 좌표로 1000.0까지기 때문에 xy배열을 선언하거나 탐색하게 되면 메모리 초과, 시간초과가 나옵니다. 따라서 sweeping 기본처럼 x축을 정렬하여 범위를 줄여주고, y축에 대해서만 1000.0을 선언해서 진짜 x축부터 sweeping 하듯이 탐색하며 오면 됩니다. 아래 링크에 설명이 잘되어 있어서 링크를 달아놓겠습니다. sweeping 문제인 것도 알고 있고, 개념도 공부한 채였는데 적용을 못 했습니다. 문제들을 열심히 풀어봐야겠습니다.  
<a href='https://rebro.kr/65'>스위핑</a>
```python
import sys
input = sys.stdin.readline


def count(list):
    cnt = 0
    for e in list:
        if e != 0:
            cnt += 1
    return cnt


N = int(input())
rec = []
for __ in range(N):
    x, y, w, h = map(float, input().split())
    rec.append([x, y, y+h, 1])
    rec.append([x+w, y, y+h, -1])

rec.sort()
# print(rec)

area = 0
ylist = [0]*25001

for i in range(len(rec)-1):
    x, y1, y2, flag = rec[i]
    y1 = int(y1*10)
    y2 = int(y2*10)
    if flag == 1:
        for j in range(y1, y2):
            ylist[j] += 1
    if flag == -1:
        for j in range(y1, y2):
            ylist[j] -= 1
    area += (rec[i+1][0] - x)*count(ylist)/10

if area-int(area) > 0:
    print(f'{area:0.2f}')
else:
    print(int(area))
```

## 생각
알고리즘을 배울 때마다 느끼는 건데 문제를 보고 이게 이 알고리즘으로 푸는 문제를 인지 어떻게 알 수 있을까요…. 너무 어렵습니다.

### list.reverse(), list.sort(reverse = True)
두 개 때문에 엄청나게 헤맸습니다…. reverse는 그냥 단순하게 리스트를 뒤집는 거고. sort는 소팅조건을 뒤집는 겁니다. 트로피 진열 문제가 브론즈 문제인데 이것 때문에 괜히 시간 잡아먹었습니다.
