---
last_modified_at : 2021-09-17
layout : single
title:  "백준 유니온 파인드"
categories: BOJ
tags : [python, union find, tree]

toc: true
toc_sticky: true
---
## 서론
<a href='https://www.acmicpc.net/step/14'>유니온 파인드</a>

유니온 파인드에 대한 개념을 몰랐기 때문에 처음 풀 때는 다 틀렸었습니다. 개념을 몰라도 풀 수 있는 문제가 있었지만 모두 시간제한에 걸려서 틀렸습니다. 유니온 파인드를 학습한 후에도 알고리즘이 문제에 적용되는 것이 직관적으로 와닿지 않아서 어려워서 꽤 오랜 시간 생각을 했고 개념부터 정리하려고 기록합니다.

## 제한 조건
<ul>
  <li>시간제한</li>
</ul>
기본적으로 유니온 파인드를 사용하지 않으면 모두 시간제한에 걸립니다. 유니온 파인드 같은 경우 정확하게 시간복잡도를 계산할 수 없지만, 코드를 보면 find 함수로 유니온 파인드의 시간복잡도가 계산되고 이 find 함수는 tree를 생성하기 때문에 O(logn)의 시간복잡도를 가집니다.  

하지만 tree가 skewed 될 경우 최악의 경우 O(n)이 되기 때문에 다른 처리를 해주어야 합니다. 일반적으로 유니온파인드의 경로압축(Union Find Path Comprehension)이라는 방법을 사용하는데 재귀함수를 통해서 루트노드를 찾을 때 이 시간을 줄이는 방법입니다. 코드는 아래와 같습니다. 이 방법을 사용하게 되면 시간복잡도가 O(a(n))이 된다고 하고 여기서 a는 아커만 함수를 의미합니다. 아커만 함수에서 n이 2^65536일때 값이 5이므로 find의 시간복잡도는 상수라고 보면 됩니다.

```python
# 경로압축 사용
def find(a):
  if parent[a] == a:
      return a
  # 이부분을 통해서 최상위 root노드를 저장해줍니다.
  # 실제로 연결된 트리는 바뀌게 되지만 유니온 파인드를 구현하는데는 지장 없음.
  parent[a] = find(parent[a])
  return parent[a]

# 경로압축 미사용
def find(a):
  if parent[a] == a:
    return a
  return find(parent[a])
```

<ul>
  <li>메모리 제한</li>
</ul>
parent 노드를 담을 n 크기만큼의 양만 있으면 되므로 메모리 제한은 문제없습니다.

## Union Find
> Union-Find란 Disjoint Set을 표현할 때 사용하는 독특한 형태의 자료구조로, 공통원소가없는, 즉 "상호 배타적"인 부분 집합 들로 나눠진 원소들에 대한 정보를 저장하고 조작하는 자료구조  

유니온파인드를 검색하면 위처럼 나옵니다. 저는 문제를 풀면서 집합을 서로 교집합이 없는 부분집합으로 나눌때 사용하는 알고리즘이라고 이해를 했습니다.
알고리즘을 구현하는 연산은 다음과 같습니다.
1. 초기화: 각각의 원소가 혼자만을 원소로 하는 집합으로 나누어집니다.
2. Union(합치기): 두 원소 a,b가 주어질 때, 이들이 속한 두 집합을 하나로 합칩니다.
3. Find(찾기): 어떤 원소 a가 주어질 때, 이 원소가 속한 집합을 반환합니다.  

개념 자체는 어렵지 않은데, 주어진 문제가 유니온 파인드를 사용하는 문제라고 알려주지 않을 때 유니온 파인드를 떠올리기가 쉽지 않을 것 같습니다. 아래 예제를 쭉 적어봤습니다.

## 1717: 집합의 표현
문제 자체가 유니온 파인드를 익히기 위한 문제입니다. 여기서는 문제없이 유니온 파인드만 구현하면 잘 실행이 됩니다.
```python
import sys
sys.setrecursionlimit(10**6)
input = sys.stdin.readline

n, m = map(int, input().split())
parent = [0]*(n+1)

for i in range(n+1):
    parent[i] = i


def find(a):
    if parent[a] == a:
        return a
    parent[a] = find(parent[a])
    return parent[a]


def union(x, y):
    a = find(x)
    b = find(y)
    if a == b:
        return
    parent[a] = b


for __ in range(m):
    op, a, b = map(int, input().split())
    if op == 0:
        union(a, b)
    else:
        parenta = find(a)
        parentb = find(b)

        if parenta == parentb:
            print("YES")
        else:
            print("NO")
```
## 1976: 여행 가자
이 문제 역시 같습니다. 동혁이가 여행을 계획한 도시들이 같은 그룹에 있는지 확인하면 됩니다.
```python
import sys
sys.setrecursionlimit(10**6)
input = sys.stdin.readline

sys.setrecursionlimit(10**6)
input = sys.stdin.readline

N = int(input())
M = int(input())

parent = [0]*(N+1)
for i in range(N+1):
    parent[i] = i


def find(x):
    if parent[x] == x:
        return x
    parent[x] = find(parent[x])
    return parent[x]


def union(x, y):
    a = find(x)
    b = find(y)
    if a == b:
        return
    parent[b] = a


for i in range(N):
    con_list = list(map(int, input().split()))
    for j in range(N):
        if con_list[j] == 1:
            union(i+1, j+1)


city_list = list(map(int, input().split()))
tmp = set()
for city in city_list:
    tmp.add(find(parent[city]))

if(len(tmp) == 1):
    print("YES")
else:
    print("NO")

```
## 4195: 친구 네트워크
같은 개념이지만 이번에는 속한 그룹의 개수를 카운트 해야 합니다. 떠올리기가 어려워서 그렇지 코드 자체는 쉽습니다. count 하는 dict를 한 개 더 만들고 초깃값을 1로 초기화합니다. 그 후에 유니온 할 때마다 개수를 늘려가면 됩니다.
```python
import sys
sys.setrecursionlimit(10**6)
input = sys.stdin.readline


def find(x):
    if x == parent[x]:
        return x
    # 부모노드를 최상단 루트로 바꿔줌.
    parent[x] = find(parent[x])
    return parent[x]


def union(x, y):
    a = find(x)
    b = find(y)
    if a == b:
        return
    parent[a] = b
    count[b] += count[a]


for __ in range(int(input())):
    F = int(input())
    parent = {}
    count = {}
    for __ in range(F):
        a, b = input().split()
        if a not in parent:
            parent[a] = a
            count[a] = 1
        if b not in parent:
            parent[b] = b
            count[b] = 1
        union(a, b)
        print(count[find(a)])
```

## 20040: 사이클 게임
이 문제가 가장 어려웠습니다. 어렵다기보다는 이문제를 어떻게 유니온 파인드로 풀어야 할지를 몰랐습니다. 도움을 받아서 풀었는데 유니온을 하기 전에 합치려는 두 집합을 파인드해서 루트가 같으면 사이클이 생긴다는 개념이 너무 신기했습니다. 이런 것을 떠올리기는 사실 쉽지가 않은데 앞으로 많이 경험해야 할 것 같습니다.
```python
import sys
sys.setrecursionlimit(10**6)
input = sys.stdin.readline


def find(x):
    if parent[x] == x:
        return x
    parent[x] = find(parent[x])
    return parent[x]


def union(x, y):
    a = find(x)
    b = find(y)
    if a == b:
        return
    parent[a] = b


n, m = map(int, input().split())

parent = [0]*n
for i in range(n):
    parent[i] = i

flag = 1
for i in range(m):
    a, b = map(int, input().split())
    if find(a) == find(b):
        print(i+1)
        flag = 0
        break
    union(a, b)
if flag:
    print(0)
```

## 생각
