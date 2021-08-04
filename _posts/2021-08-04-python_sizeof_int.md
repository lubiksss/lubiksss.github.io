---
last_modified_at : 2021-08-04
layout : single
title:  "파이썬 int형 크기"
categories: python
tags : [int 크기, 정수형 크기, 28바이트]

toc: true
toc_sticky: true
---
## 서론
요즘 파이썬을 공부하면서 코딩 문제를 풀고 있는데 오늘은 도저히 메모리 초과가 나올 수 없는 부분에서 메모리 초과가 나와서 고민을 좀 해 봤습니다. 알고리즘 자체가 완전히 적합한 알고리즘은 아니었지만 제가 계산하는 방법으로 계산하면 (<a href='/boj/BOJ_6549/'>메모리를 계산하는 과정</a>) 메모리 초과가 나올 수가 없습니다. 그래서 왜 그런지 찾아보았습니다.

## 파이썬 int형 크기
제가 파이썬을 공부하기 전에 C를 먼저 공부했었는데 파이썬에서도 당연히 C언어처럼 int 형의 크기가 4바이트인 줄 알고 있었습니다. 그리고 파이썬의 경우 arbitrary precision이라고 하여 데이터의 크기만큼 메모리를 할당한다는 것도 알고 있었기에 4바이트에서 시작해서 그 이상으로 데이터의 크기가 넘어갈 때마다 메모리를 더 할당한다고 생각했었습니다.  

하지만 파이썬의 정수형 크기는 4바이트 시작이 아니고 28바이트 시작이었습니다. 간단하게 pyplot을 통해 그려봤습니다.  

<img src = 'https://user-images.githubusercontent.com/67966414/128191005-aacc5084-3796-4996-838d-d775ff6251ae.png' alt='파이썬 int형의 크기' style="margin-left: auto; margin-right: auto; display: block;">

```python
import sys
from matplotlib import lines
import matplotlib.pyplot as plt

x = []
y = []
for i in range(100):
    x.append(i)
    y.append(sys.getsizeof(2**i))

plt.plot(x, y, color='black')
plt.xticks(range(0, 100, 30))
plt.xlabel('X')
plt.ylabel('sizeof(2^X)(byte)')
for i in range(1, 100, 30):
    plt.vlines(i, min(y), max(y), color='red', linestyle='--')
plt.show()
```
보시다시피 2^0~2^30까지는 데이터가 0이든 10억이든 메모리는 28바이트를 차지합니다. 그리고 그 후로 2^30배마다 4바이트를 추가로 할당합니다. 음수도 마찬가지입니다.

## 생각
애초에 파이썬이 사용자가 코딩할 때 컨트롤할것이 적어서 빠르게 유명해지긴 했지만, 데이터가 0이든 10억이든 같은 메모리 그것도 28바이트나 쓴다는 건 조금 비효율적인 것 같습니다. 편의성 말고도 다른 이유가 있다면, 없을 것 같지만 찾는다면 추가로 적도록 하겠습니다.  

처음에 코딩 문제를 풀면서 데이터 하나를 4바이트로 잡고 계산했기 때문에 28바이트로 다시 계산하면 메모리 초과가 나는 게 맞았습니다… 그리고 지금까지 푼 문제들이 잘못 푼 건 아니지만, 메모리를 계산하는데 메모리 여유가 7배만큼이나 있었기 때문에 통과했던 거였습니다. 앞으로는 이것저것 당연하다고 생각하지 말고 꼭 확인해보고 하겠습니다.

### *참고
<a href = 'https://ahracho.github.io/posts/python/2017-05-09-python-integer-overflow/'>[기초 파이썬] 파이썬 3에는 오버플로우가 없다?</a>
