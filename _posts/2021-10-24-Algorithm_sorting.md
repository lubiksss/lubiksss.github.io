---
last_modified_at : 2021-10-24
layout : single
title:  "Algorithm 소팅"
categories: Algorithm
tags : [Algorithm, 소팅, sorting]

toc: true
toc_sticky: true
---
## 서론
### 참조
<!-- <a target = '_blank' href=''></a>   -->

## 요약
<table width = '100%'>
  <thead>
    <tr>
        <th style="text-align: center"><strong>구분</strong></th>
        <th style="text-align: center"><strong>시간복잡도</strong></th>
        <th style="text-align: center"><strong>공간복잡도</strong></th>
        <th style="text-align: center"><strong>안정성</strong></th>
        <th style="text-align: center"><strong>비고</strong></th>
    </tr>
  </thead>
  <tbody>
    <tr>
        <td style="text-align: center">선택 정렬</td>
        <td style="text-align: center">n^2</td>
        <td style="text-align: center">제자리 정렬</td>
        <td style="text-align: center">불안정</td>
        <td style="text-align: center"></td>
    </tr>
    <tr>
        <td style="text-align: center">삽입 정렬</td>
        <td style="text-align: center">n^2</td>
        <td style="text-align: center">제자리 정렬</td>
        <td style="text-align: center">안정</td>
        <td style="text-align: center">어느 정도 정렬된 상태에서 효율성 좋음</td>
    </tr>
    <tr>
        <td style="text-align: center">버블 정렬</td>
        <td style="text-align: center">n^2</td>
        <td style="text-align: center">제자리 정렬</td>
        <td style="text-align: center">안정</td>
        <td style="text-align: center"></td>
    </tr>
    <tr>
        <td style="text-align: center">셸 정렬</td>
        <td style="text-align: center">n^1.5</td>
        <td style="text-align: center">제자리 정렬</td>
        <td style="text-align: center">불안정</td>
        <td style="text-align: center">삽입정렬은 발전시킨 정렬</td>
    </tr>
    <tr>
        <td style="text-align: center">병합 정렬</td>
        <td style="text-align: center">nlogn</td>
        <td style="text-align: center">정렬된 리스트를 담을 공간이 필요 O(n)</td>
        <td style="text-align: center">안정</td>
        <td style="text-align: center"></td>
    </tr>
    <tr>
        <td style="text-align: center">퀵 정렬</td>
        <td style="text-align: center">nlogn</td>
        <td style="text-align: center">제자리 정렬</td>
        <td style="text-align: center">불안정</td>
        <td style="text-align: center">nlogn 정렬 중 가장 빠름</td>
    </tr>
    <tr>
        <td style="text-align: center">힙 정렬</td>
        <td style="text-align: center">nlogn</td>
        <td style="text-align: center">정렬된 리스트를 담을 공간이 필요 O(n)</td>
        <td style="text-align: center">불안정</td>
        <td style="text-align: center">가장 큰 값 몇개만 필요할때 효율적</td>
    </tr>

  </tbody>
</table>

## 선택 정렬 (Selection)
```python
def swap(a, b):
    nlist[a], nlist[b] = nlist[b], nlist[a]


def selection_sort(nlist):
    # 처음부터 끝까지 돌면서
    for i in range(len(nlist)):
        minidx = i
        # 정렬된곳 빼고 최솟값을 찾아서
        for j in range(i, len(nlist)):
            if nlist[j] < nlist[minidx]:
                minidx = j
        # 바꿉니다.
        swap(i, minidx)
    return nlist
```
## 삽입 정렬 (Insertion)
```python
def insertion_sort(nlist):
    # 두번째 원소부터 끝까지 돌면서
    for i in range(1, len(nlist)):
        # 앞의 원소들이랑 비교하면서
        for j in range(i, 0, -1):
            if nlist[j] < nlist[j-1]:
                # 바꿉니다.
                swap(j, j-1)
            # 앞의 것보다 안작을 때 브레이크를 걸어줘야 더 이상 확인안하기 때문에
            # 최적의 경우 n이 나올 수 있음 (어느정도 정렬된 리스트는 효과가 좋다)
            else:
                break
    return nlist
```
## 버블 정렬 (Bubble)
```python
def bubble_sort(nlist):
    # 처음부터 끝까지 돌면서
    for i in range(len(nlist)):
        # 정렬된곳 빼고 뒤로 가면서 한번씩 비교하면서
        for j in range(len(nlist)-i-1):
            if nlist[j+1] < nlist[j]:
                # 바꿉니다.
                swap(j+1, j)
    return nlist
```
## 셸 정렬 (Shell)
```python
def shell_insertion_sort(start, gap):
    # 시작+gap부터 원소부터 끝까지 돌면서
    for i in range(start+gap, len(nlist), gap):
        # 한gap앞의 원소들이랑 비교하면서
        for j in range(i, start, -gap):
            if nlist[j] < nlist[j-gap]:
                # 바꿉니다.
                swap(j, j-gap)
            # 앞의 것보다 안작을 때 브레이크를 걸어줘야 더 이상 확인안하기 때문에
            # 최적의 경우 n이 나올 수 있음 (어느정도 정렬된 리스트는 효과가 좋다)
            else:
                break


def shell_sort(nlist):
    # 삽입정렬을 발전시킨 정렬로 삽입정렬을 gap이 1이었다.
    # 여기선 gap을 리스트 길이의 절반씩 나눠가며 진행한다.
    gap = len(nlist)//2
    # 갭을 절반씩 줄여나가면서 정렬할것임.
    while gap > 0:
        # gap만큼 띄워서 부분리스트를 만들면 부분리스트 갯수는 gap개가 됨
        for i in range(gap):
            # 그 부분리스트들을 삽입정렬함
            # print(nlist[i::gap])
            shell_insertion_sort(i, gap)
            # print(nlist[i::gap])
        gap = gap//2
    return nlist
```
## 병합 정렬 (Merge)
```python
def merge(nlist, left, mid, right):
    sorted = [0]*len(nlist)
    lstart = left
    lend = mid
    rstart = mid+1
    rend = right
    idx = left

    # 분할된 애들을 앞에서 부터 비교하면서 작은것먼저 sorted에 넣음
    while lstart <= lend and rstart <= rend:
        if nlist[lstart] <= nlist[rstart]:
            sorted[idx] = nlist[lstart]
            lstart += 1
            idx += 1
        else:
            sorted[idx] = nlist[rstart]
            rstart += 1
            idx += 1

    # 다넣었는데 왼쪽이 남았다? 그대로 넣는다.
    if lstart <= lend:
        for i in range(lstart, lend+1):
            sorted[idx] = nlist[i]
            idx += 1
    # 다넣었는데 오른쪽이 남았다? 그대로 넣는다.
    if rstart <= rend:
        for i in range(rstart, rend+1):
            sorted[idx] = nlist[i]
            idx += 1

    for i in range(left, right+1):
        nlist[i] = sorted[i]


def merge_sort(nlist, left, right):
    # 분할정복방법이니 탈출 조건
    # 한개만 남게되면 아무것도 안하고 merge하면됨.
    if left == right:
        return

    # 결국에 쪼개놓고 머지를 하면서 올라오는것
    # 아랫단계에서부터 nlist의 값을 고치면서 올라옴.
    if left < right:
        mid = (left+right)//2
        merge_sort(nlist, left, mid)
        merge_sort(nlist, mid+1, right)
        merge(nlist, left, mid, right)

    return nlist
```
## 퀵 정렬 (Quick)
```python
def quick_sort(nlist, left, right):
    # 분할정복방법이니 탈출조건
    # 원소가 한개만 남으면 아무것도 안하면됨
    if left >= right:
        return

    # 피벗은 첫번째 원소 (랜덤으로 해도됨)
    pivot = left
    lstart = left
    rstart = right
    while(lstart <= rstart):
        # 왼쪽부터 피벗보다 큰수를 찾음
        while lstart <= right and nlist[lstart] <= nlist[pivot]:
            lstart += 1
        # 오른쪽부터 피벗보다 작은수를 찾음
        while rstart > left and nlist[rstart] >= nlist[pivot]:
            rstart -= 1
        # 만약에 엇갈렸다면 피벗과 작은데이터와 교체한다
        # 결국 엇갈리는 부분이 최상위 while문이 끝나는 부분임.
        # pivot의 위치는 rstart가 됨
        if lstart > rstart:
            swap(pivot, rstart)
        # 그렇지 않다면 두개를 바꾼다.
        else:
            swap(lstart, rstart)
    # 그리고 피벗 좌우로 분할정복을 해준다.
    quick_sort(nlist, left, rstart-1)
    quick_sort(nlist, rstart+1, right)
    return nlist
```
## 힙 정렬 (Heap)


## 생각
제자리 정렬을 구현하기 위해선 신경을 좀 써야 합니다. 리스트 슬라이싱을 사용하면 훨씬 쉽게 풀 수 있지만 메모리가 복사되기 때문에 제자리 정렬이 아니게 됩니다.
소팅에대해서도 공부했는데 분할정복에서 인덱스를 다루면서 재귀를 어떻게 부르는지에 대해서 많이 생각해 볼 수 있었습니다.