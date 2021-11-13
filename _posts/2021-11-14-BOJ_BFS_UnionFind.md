---
last_modified_at : 2021-11-14
layout : single
title:  "백준 연결 요소의 개수"
categories: BOJ
tags : [python, BFS, union find]

toc: true
toc_sticky: true
---
## 서론
<a href='https://www.acmicpc.net/problem/11724'>연결 요소의 개수</a>

BFS를 정리해보려고 문제 몇 개를 푸는 중에 BFS 문제가 Union Find로도 풀릴 것 같아 Union Find를 적용해봤더니 풀려서 기록해봅니다.

## 제한 조건
<ul>
  <li>시간제한 3초</li>
</ul>
기본적으로 1초에 1억 번 연산한다고 생각하고 풉니다. BFS의 경우 O(V+E)의 시간복잡도를 가지는데 여기서 V = 1000, M = V^2이므로 V+E는 약 1,000,000이고 3초의 시간이면 충분합니다. 실버단계 문제라서 시간을 여유롭게 준걸까요? 3초까진 필요 없을 것 같습니다.

<ul>
  <li>메모리 제한 512MB</li>
</ul>
그래프를 선언해놓고 풀면 약 E의 두 배에 해당하는 공간이 필요한데(방향성이 없으므로 양 시작 노드에 다 들어가므로) 2,000,000개의 파이선 힌트형 28byte 면 56MB이니 메모리 제한도 충분합니다.


## BFS
기본적으로 그래프를 한 번씩 다 탐색해보면서 연결된 애들은 visited 리스트에 같은 숫자를 넣었습니다.
```python
import sys
from collections import deque as dq
input = sys.stdin.readline

N, M = map(int, input().split())
graph = {}
for i in range(1, N+1):
    graph[i] = []
for i in range(M):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)

cnt = 0
visited = [0]*(N+1)

for i in range(1, N+1):
    if visited[i] == 0:
        que = dq()
        que.append(i)
        cnt += 1
        visited[i] = cnt

        while que:
            base = que.popleft()
            for next in graph[base]:
                if visited[next] == 0:
                    que.append(next)
                    visited[next] = cnt

print(max(visited))
```


### Union Find
연결된 요소를 찾는다는 것 자체가 Union Find 느낌이 와서 적용해봤는데 잘 풀리는 것 같습니다. 주의할 점은 지금까지 Union Find에서 parent를 구할 때 parent 리스트는 같은 그룹이라고 같은 숫자가 쓰여있는 것이 아니기 때문에 문제에 맞게 바꾸기 위해서 한 번 더 최신화를 해주었습니다.
```python
import sys
sys.setrecursionlimit(10**6)
input = sys.stdin.readline

N, M = map(int, input().split())

parent = [i for i in range(N+1)]


def find(a):
    if parent[a] == a:
        return a
    parent[a] = find(parent[a])
    return parent[a]


def union(a, b):
    a = find(a)
    b = find(b)

    if a == b:
        return
    parent[a] = b


for __ in range(M):
    a, b = map(int, input().split())
    union(a, b)

# 이 부분이 최신화를 해주는 부분. 이렇게 한번더 정리해주면 같은 그룹은 같은 숫자를 가지는 parent리스트가 됩니다.
for i in range(N+1):
    parent[i] = find(i)

print(len(set(parent[1:])))
```

## 생각
그럼 뭐가 더 효율적일지를 생각해보면
1. 시간복잡도 측면에서는 BFS는 O(V+E)를 가지고 Union Find는 정확히 설명할 순 없지만 두 개의 루프가 V, E로 돌아가고 루프 안의 Union과 Find 함수는 일반적으로 상수라고 알려져 있으므로 O(V+E)쯤이 될 것 같습니다. 시간복잡도 측면에선 거의 비슷하겠네요.
2. 공간복잡도 측면에서는 BFS는 그래프를 선언해놓고 하면 O(V+E)의 공간복잡도를 가지게 되지만 Union Find는 V에 해당하는 parent 리스트만 있으면 E에 해당하는 선언은 할 필요가 없습니다. 그래서 공간복잡도 상으로는 Union Find가 이득일 것 같습니다.