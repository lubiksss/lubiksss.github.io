---
last_modified_at : 2021-10-29
layout : single
title:  "백준 2448번 별 찍기"
categories: BOJ
tags : [2448번, python, 재귀함수, 분할정복]

toc: true
toc_sticky: true
---
## 서론
<a href='https://www.acmicpc.net/problem/2448'>별 찍기 - 11</a>

기본적으로 분할정복과 재귀함수를 이용해서 프랙탈 구조를 만드는 문제입니다. 요즘 분할정복과 재귀함수에 대해서 다시 한번 생각해보고 있어서 풀어 보았습니다. 기본적으로 재귀를 할 때 리스트를 건네주게 되는데 리스트 자체를 복사해서 건네주고 거기서 다시 인덱스에 접근하면 쉬운데 이때는 리스트가 복사된다는 단점이 있습니다. 이런 최적화 문제는 인덱스를 건네주면서 풀어야 하는데 그 부분이 생각할 점이 좀 많은 것 같습니다.

## 제한 조건
<ul>
  <li>시간제한 1초</li>
</ul>
기본적으로 1초에 1억 번 연산한다고 생각하고 풉니다. 문제의 경우 row의 최댓값이 약 3000이고 col의 최댓값이 약 두 배인 6,000정도 됩니다. 모든 탐색을 해도 18,000,000번으로 1억 번에는 안 미치지만 프랙탈 구조상 3등분씩 하며 탐색하니 시간제한은 문제없습니다.

<ul>
  <li>메모리 제한 256MB</li>
</ul>
위에서 말한 대로 인풋을 최댓값으로 선언 시 천팔백만 개의 문자열이 생성되고 이것만 해도 이미 매우 크기 때문에 재귀함수를 쓸 때 리스트를 복사해서 넘겨주게 되면 메모리 제한이 걸리게 되고 인덱스로 접근을 해야 합니다.


## 재귀함수
```python
import sys
input = sys.stdin.readline

N = int(input())

board = [[' ']*((N//3)*5+(N//3-1)) for __ in range(N)]


def star(board, srow, erow, col):
    if (erow-srow) // 2 >= 3:
        star(board, srow, srow+(erow-srow)//2, col)
        star(board, srow+(erow-srow)//2, erow, col-(erow-srow)//2)
        star(board, srow+(erow-srow)//2, erow, col+(erow-srow)//2)
        return
    board[srow][col] = '*'
    board[srow+1][col-1] = '*'
    board[srow+1][col+1] = '*'
    board[srow+2][col-2] = '*'
    board[srow+2][col-1] = '*'
    board[srow+2][col] = '*'
    board[srow+2][col+1] = '*'
    board[srow+2][col+2] = '*'


def print_star(board):
    for row in board:
        print(''.join(row))


star(board, 0, N, len(board[0])//2)

print_star(board)
```

## 생각
재귀함수가 진짜 신기하고 재밌는 거 같습니다. 매번 문제를 풀 때마다 뭔가 깨닫건 많은데 막상 글로 적기가 힘든 것 같습니다. 문제를 많이 풀어보고 익혀야겠네요.
### 재귀함수 구조
재귀함수를 통해 문제를 분할정복해서 푼다고 했을 때 가장 중요한 건 문제를 쪼갤 수 있을 때까지 쪼개고 쪼갤 수 없는 순간을 정하여 코딩하는 것입니다. 굉장히 쉬운 아이디어인데 뭔가 문제에 적용되어 풀리는 걸 보면 엄청 신기합니다.
