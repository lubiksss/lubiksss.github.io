---
last_modified_at : 2021-11-03
layout : single
title:  "Algorithm 소팅"
categories: Algorithm
tags : [Algorithm, 소팅, sorting]

toc: true
toc_sticky: true
---
## 서론
기본적으로 소팅의 원리와 동작은 이해했고 구현에 대한 부분만 연습할 겸 적어봤습니다.
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
def merge_sort(nlist, left, right):
    # left,right 포함
    # 분할정복을 사용하기 때문에 end조건
    if left == right:
        return
    mid = (left+right)//2
    merge_sort(nlist, left, mid)
    merge_sort(nlist, mid+1, right)

    sorted = [0]*len(nlist)
    idx = left
    ls = left
    le = mid
    rs = mid+1
    re = right

    # 왼쪽 파트와 오른쪽 파트를 작은 거부터 순서대로 넣음
    while ls <= le and rs <= re:
        if nlist[ls] <= nlist[rs]:
            sorted[idx] = nlist[ls]
            ls += 1
        else:
            sorted[idx] = nlist[rs]
            rs += 1
        idx += 1

    # 한쪽 파트가 다넣어졌을때 남은 파트를 넣는 부분
    if ls <= le:
        for i in range(ls, le+1):
            sorted[idx] = nlist[i]
            idx += 1
    if rs <= re:
        for i in range(rs, re+1):
            sorted[idx] = nlist[i]
            idx += 1
    for i in range(left, right+1):
        nlist[i] = sorted[i]

    return nlist
```
## 퀵 정렬 (Quick)
```python
def quick_sort(nlist, left, right):
    # left,right 포함
    # 분할정복을 사용하기 때문에 end조건
    if left >= right:
        return

    pvt = left
    ls = left
    rs = right
    # 피벗을 기준으로 왼쪽에는 작은숫자 오른쪽에는 큰숫자를 남김
    while ls <= rs:
        while ls <= right and nlist[ls] <= nlist[pvt]:
            ls += 1
        while rs > left and nlist[rs] >= nlist[pvt]:
            rs -= 1
        # 왼쪽포인터와 오른쪽포인터가 교차하지 않았으면 바꿀게 있단 뜻
        if ls <= rs:
            swap(nlist, ls, rs)
        # 교차했으면 이제 왼쪽엔 작은것만 남고 오른쪽엔 작은것만 남았단 뜻
        # 피벗과 rs를 바꿔준다.
        else:
            swap(nlist, pvt, rs)
    quick_sort(nlist, left, rs-1)
    quick_sort(nlist, rs+1, right)

    return nlist
```
<!-- ## 힙 정렬 (Heap) -->

## 테스트 결과
```python
nlist = random.sample(range(1, 1001), 1000)
start = time.time()
selection_sort(nlist)
print(f'selection_sort\tn=1000\ttime: {time.time()-start:.5f}')
nlist = random.sample(range(1, 10001), 10000)
start = time.time()
selection_sort(nlist)
print(f'selection_sort\tn=10000\ttime: {time.time()-start:.5f}')
```
```cmd
selection_sort  n=1000  time: 0.02601
selection_sort  n=10000 time: 2.44855

insertion_sort  n=1000  time: 0.05555
insertion_sort  n=10000 time: 5.34221

bubble_sort     n=1000  time: 0.06702
bubble_sort     n=10000 time: 6.97594

shell_sort      n=1000  time: 0.00400
shell_sort      n=10000 time: 0.06703

merge_sort      n=1000  time: 0.00400
merge_sort      n=10000 time: 0.12603

quick_sort      n=1000  time: 0.00200
quick_sort      n=10000 time: 0.02400
```
리스트의 길이가 10배가 되었을 때 n^2 시간 복잡도인 정렬들은 시간이 약 100배가 되는 것을 확인할 수 있습니다. shell 정렬의 경우 n^1.5보다 성능이 좋게 나왔고 merge 정렬은 nlogn, quick 정렬도 nlogn보다 성능이 좋게 나온 것을 볼 수 있습니다.

## 생각
제자리 정렬을 구현하기 위해선 신경을 좀 써야 합니다. 리스트 슬라이싱을 사용하면 훨씬 쉽게 풀 수 있지만 메모리가 복사되기 때문에 제자리 정렬이 아니게 됩니다.
소팅에대해서도 공부했는데 분할정복에서 인덱스를 다루면서 재귀를 어떻게 부르는지에 대해서 많이 생각해 볼 수 있었습니다.
