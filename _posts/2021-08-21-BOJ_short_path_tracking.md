---
last_modified_at : 2021-08-21
layout : single
title:  "백준 최단 거리 추적"
categories: BOJ
tags : [python, short path, tracking]

toc: true
toc_sticky: true
---
## 서론
<a href='https://www.acmicpc.net/step/41'>최단거리 역추적</a>

최단 거리를 역추적하는 방법에 관해서 공부했습니다. 지난번에 플루이드 와샬 알고리즘으로 최단 경로를 구하면서 역추적하는 방법을 적은 적이 있는데 해당 알고리즘 말고 다른 알고리즘으로 푸는 문제들도 많이 풀어봤습니다.  

최단 거리라고 하면 BFS, Dijkstra, Bellman-Ford, Floyd-Warshall 알고리즘이 떠오르는데 해당하는 알고리즘만 알고 있다면 푸는 방법은 모두 똑같습니다.  

해당 정점을 최단으로 오기 전에 지나온 정점을 담는 리스트를 한 개 더 선언하면 됩니다. 그리고 그 리스트는 최단 경로를 나타내는 리스트와 크기가 같습니다. 예를 들어 Dijkstra의 경우는 path[n]으로 최단 경로를 나타내기 때문에 이전 정점을 나타내는 리스트도 prev[n]으로 만들면 되고 Floyd는 path[n][n]을 가지기 때문에 이전 정점 리스트도 prev[n][n]으로 만들면 됩니다. 그리고 최단 경로를 갱신할 때마다 이 리스트도 갱신해주면 perv 리스트로 최단 경로 역추적이 가능합니다.

## 제한 조건
<ul>
  <li>시간제한</li>
</ul>
문제에 알맞은 알고리즘으로 풀면 시간제한은 문제없습니다. prev리스트를 인덱스로 접근하여 갱신시키는 게 추가되기 때문에 이 부분에 대한 추가 코스트는 없습니다.
<ul>
  <li>메모리 제한</li>
</ul>
이전 정점 리스트를 선언해야 하므로 조금의 메모리가 더 들어가지만 보통의 문제의 경우 제한에 걸리지 않습니다. 역시 문제에 맞는 알고리즘으로 알맞게 풀어야 하고 제가 메모리 제한에 걸린 적은 거의 변수선언보다는 BFS를 사용할 경우 que에 정점들이 중복이나 다른 이유로 너무 많이 쌓여서였습니다.

## 12852: 1로 만들기2
이 문제는 굳이 BFS를 사용하지 않아도 되지만 역추적 카테고리상 BFS로 탐색을 하면서 최단 거리를 찾고 prev를 갱신한다는 뜻으로 BFS로 풀어보았습니다.
```python
import sys
from collections import deque as dq
input = sys.stdin.readline

N = int(input())
prev_path = [0, 0] + [0]*(N-1)

que = dq()
visited = [False] * (N+1)

que.append([1, 0])
visited[1] = True

while que:
    v, time = que.popleft()
    if v == N:
        print(time)
        break
    if v*3 <= N and not visited[v*3]:
        que.append([v*3, time+1])
        prev_path[v*3] = v
        visited[v*3] = True
    if v*2 <= N and not visited[v*2]:
        que.append([v*2, time+1])
        prev_path[v*2] = v
        visited[v*2] = True
    if v+1 <= N and not visited[v+1]:
        que.append([v+1, time+1])
        prev_path[v+1] = v
        visited[v+1] = True

# 이렇게 prev리스트를 참조하며 최단경로를 역추적 할 수 있습니다.
idx = N
while idx != 0:
    print(idx, end=' ')
    idx = prev_path[idx]1
```
## 13913: 숨바꼭질 4
위의 문제와 똑같습니다.
```python
import sys
from collections import deque as dq
input = sys.stdin.readline

N, K = map(int, input().split())
MAX = 100000
prev_path = [0]*(MAX+1)

que = dq()
visited = [False] * (MAX+1)

que.append([N, 0])
visited[N] = True

while que:
    v, time = que.popleft()
    if v == K:
        print(time)
        break
    if 2*v <= MAX and not visited[2*v]:
        que.append([2*v, time+1])
        prev_path[2*v] = v
        visited[2*v] = True
    if v+1 <= MAX and not visited[v+1]:
        que.append([v+1, time+1])
        prev_path[v+1] = v
        visited[v+1] = True
    if 0 <= v-1 <= MAX and not visited[v-1]:
        que.append([v-1, time+1])
        prev_path[v-1] = v
        visited[v-1] = True

idx = K
tmp = []
while idx != N:
    tmp.append(idx)
    idx = prev_path[idx]
tmp.append(idx)

print(*reversed(tmp))
```
## 9019: DSLR
계산기를 구현하는 부분에서 최적화를 시켜야 하는 게 좀 어려웠고, 최단 경로를 구하는 개념은 똑같습니다. 그리고 이문제에서 문자열을 다루는 함수를 쓰는 게 얼마나 느린지 확인했습니다. 되도록 문자열을 다루는 함수는 안 쓰는 게 좋을 것 같습니다.
```python
from collections import deque as dq
import sys
input = sys.stdin.readline


def fD(num):
    return num*2 % 10000


def fS(num):
    return (num-1) % 10000


def fL(num):
    return ((num*10)+(num//1000)) % 10000


def fR(num):
    return ((num % 10)*1000 + (num//10)) % 10000


for __ in range(int(input())):
    start, end = map(int, input().split())

    que = dq()
    path = ['']*10000

    que.append(start)
    # 원래시작점은 아무데서도 오지않았다고 표현하는게 맞지만
    # visited 배열처럼 쓰기위해서 방문했다는 의미로 아무거나 써넣고
    # 나중에 지움.
    path[start] = 'A'

    # 보통 큐가 비지않으면 이라고 썻었는데
    # 큐를 확인할 필요없이 그냥 목적지에 path가 완성되면 바로 break
    while not path[end]:
        v = que.popleft()

        D = fD(v)
        S = fS(v)
        L = fL(v)
        R = fR(v)

        if not path[D]:
            que.append(D)
            path[D] = path[v]+'D'
        if not path[S]:
            que.append(S)
            path[S] = path[v]+'S'
        if not path[L]:
            que.append(L)
            path[L] = path[v]+'L'
        if not path[R]:
            que.append(R)
            path[R] = path[v]+'R'

    print(path[end].lstrip('A'))
```
## 11779: 최소비용 구하기 2
Dijkstra 알고리즘만 알고 있다면 똑같습니다.
```python
import sys
from collections import deque as dq
import heapq
input = sys.stdin.readline


def make_graph(n, m):
    graph = {}
    for i in range(1, n+1):
        graph[i] = []
    for i in range(m):
        start, end, weight = map(int, input().split())
        graph[start].append([end, weight])
    return graph


def Dijkstra(graph, n, start):
    que = [[0, start]]
    path = [sys.maxsize] * (n+1)
    prev_path = [-1] * (n+1)

    path[start] = 0
    prev_path[start] = 0

    while que:
        base_w, base_v = heapq.heappop(que)
        if base_w > path[base_v]:
            continue
        for next_v, next_w in graph[base_v]:
            next_path = path[base_v]+next_w
            if next_path < path[next_v]:
                path[next_v] = next_path
                prev_path[next_v] = base_v
                heapq.heappush(que, [next_path, next_v])

    return path, prev_path


n, m = int(input()), int(input())
graph = make_graph(n, m)
start, end = map(int, input().split())

path, prev_path = Dijkstra(graph, n, start)

idx = end
tmp = []
while idx:
    tmp.append(idx)
    idx = prev_path[idx]

print(path[end])
print(len(tmp))
print(*reversed(tmp))
```
## 11780: 플로이드 2
Floyd 알고리즘만 알고 있다면 똑같습니다.
```python
import sys
from pprint import pprint
input = sys.stdin.readline


def make_dist(n, m):
    dist = [[sys.maxsize]*n for __ in range(n)]
    prev = [[-1]*n for __ in range(n)]
    for i in range(n):
        dist[i][i] = 0
    for __ in range(m):
        start, end, weight = map(int, (input().split()))
        dist[start-1][end-1] = min(dist[start-1][end-1], weight)
        prev[start-1][end-1] = start
    return dist, prev


def Floyd(dist, prev, n):
    for mid in range(n):
        for start in range(n):
            for end in range(n):
                if dist[start][end] > dist[start][mid]+dist[mid][end]:
                    dist[start][end] = dist[start][mid]+dist[mid][end]
                    prev[start][end] = prev[mid][end]


n, m = int(input()), int(input())
dist, prev = make_dist(n, m)
Floyd(dist, prev, n)

for i in range(n):
    for j in range(n):
        if dist[i][j] == sys.maxsize:
            dist[i][j] = 0

dist = [[0 if x == sys.maxsize else x for x in row] for row in dist]

for row in dist:
    print(*row)

for start in range(n):
    for end in range(n):
        if prev[start][end] == -1:
            print(0)
        else:
            tmp = []
            idx = end
            while prev[start][idx] != -1:
                tmp.append(idx+1)
                idx = prev[start][idx]-1
            tmp.append(start+1)
            print(len(tmp), end=' ')
            print(*reversed(tmp))
```


## 생각
