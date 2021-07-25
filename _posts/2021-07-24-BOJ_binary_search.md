---
last_modified_at : 2021-07-24
layout : single
title:  "백준 이분 탐색(binary search)"
categories: BOJ
tags : [python, 1920번, 10816번, 1654번, 2805번, 2110번, 이분 탐색]

toc: true
toc_sticky: true
---
## 서론
<a href='https://www.acmicpc.net/step/29'>단계별로 풀어보기: 이분 탐색</a>

코딩을 손에 익히고 알고리즘도 공부하고자 백준 문제들을 단계별로 풀어보고 있습니다. 이번에는 이분 탐색(binary search) 단계의 문제를 몇 문제 풀었는데 알고리즘 구조가  조금은 이해가 돼서 적어놓으려고 합니다. 그리고 이분 탐색을 활용한 문제에도 이분 탐색을 적용하며 문제를 풀어보겠습니다.

## 알고리즘 구조
기본적으로 이분 탐색 관련 문제는 다 똑같습니다. brute force를 사용하면 시간제한에 걸리기 때문에 총 데이터의 길이에서 절반씩 잘라가며 탐색하는 방법입니다. 이렇게 하면 절반을 기준으로 조건에 맞는 왼쪽과 오른쪽에 둘 중 하나에 대해서만 다시 탐색하면 되기 때문에 시간복잡도는 logn을 가집니다.  

특징으로는 조건보다 작다면 왼쪽을 탐색 조건보다 크다면 오른쪽을 탐색하기 때문에 데이터는 이미 정렬이 되어 있어야 합니다. 데이터를 오름차순 정렬하는 함수 자체가 시간복잡도 nlogn이라는 비용이 있지만, 이분 탐색을 하지 않고 brute force를 사용할 경우 nlogn보다 큰 방법이 나오게 되어 정렬 복잡도 nlogn은 무시합니다.  

기본적으로 이분 탐색은 start와 end 인덱스를 가지고 절반인 mid에서의 조건을 확인하며 start와 end를 옮기며 탐색 범위를 좁힙니다. edge case에 대하여 start와 end의 값을 조정하는 여러 가지 방법이 있겠지만 저 같은 경우는 아래와 같은 코드가 직관적으로 이해되고 손에 익어서 사용 중입니다.
```python
def binary_search(start, end, target):
    tmp = -1
    while start <= end:
        mid = (start+end)//2
        if target == data[mid]:
            tmp = mid
            break
        elif x > data[mid]:
            start = mid+1
        else:
            end = mid-1
    return tmp
```
start와 end는 데이터의 인덱스 첫 값과 끝 값이고 target은 찾으려는 값입니다. 우선 mid에서 값을 찾고 맞으면 그대로 break, 찾으려는 값이 더 작으면 인덱스를 옮겨 왼쪽에서, 크면 오른쪽에서 찾습니다. 그리고 while문의 조건으로 start와 end가 교차하게 되면(모든 데이터를 다 확인하면) 탐색이 끝납니다. 찾은 경우 tmp값이 mid 값으로 바뀌기 때문에 찾은 경우만 찾으려는 값의 인덱스를 리턴합니다.

## 10816번: 숫자 카드 2
이분 탐색으로 lower bound와 upper bound를 찾는 문제입니다. 이 두 개념은 유명한 개념이라고 하는데 간단하게 설명해 드리면 lower bound는 데이터 안에서 찾고자 하는 숫자가 처음 나오는 곳이고 upper bound는 데이터 안에서 찾고자 하는 숫자보다 큰 숫자가 처음 나오는 곳입니다. 이문제를 이분 탐색을 활용하여 풀 수 있습니다.  

이분 탐색과 똑같은 구조에서 성공했을 때도 break하지 않고 탐색을 계속하면 됩니다. lower bound의 경우 값을 찾았어도 앞쪽에서 더 먼저 같은 값이 나왔을 수 있으므로 왼쪽에서 또 탐색하면 되고 upper bound의 경우는 반대입니다. 코드는 아래와 같습니다.
```python
def lower_bound(start, end, target):
    tmp = -1
    while start <= end:
        mid = (start+end)//2
        if data[mid] == target:
            tmp = mid
            end = mid-1
        elif target > data[mid]:
            start = mid+1
        else:
            end = mid-1
    return tmp
        
def upper_bound(start, end, target):
    tmp = -1
    while start <= end:
        mid = (start+end)//2
        if data[mid] == target:
            tmp = mid
            start = mid+1
        elif target > data[mid]:
            start = mid+1
        else:
            end = mid-1
    return tmp
```
제가 짠 코드에선 upper bound가 찾고자 하는 숫자보다 큰 숫자가 처음 나오는 곳이 아닌 찾고자 하는 숫자가 마지막으로 나온 곳입니다. 이 부분은 참고하시면 되겠습니다.

인터넷에 위의 코드보다 깔끔한 코드들이 많은데 기본적으로 tmp같은 값을 사용하지 않고 인덱스만 사용하고 있습니다. 하지만 이런 부분이 직관적으로 와닿지 않고 이해하기 어려워서 제가 이해한 대로 코드를 작성했습니다. tmp 저장 공간과 조건문 한 개 정도의 비용을 더 소모하는데 무시할 정도입니다.

## 1654번, 2805번, 2110번: 이분 탐색으로 최댓값 구하기
모두 똑같은 개념의 문제라서 묶었습니다. 조건을 만족하는 최댓값을 이분 탐색으로 구할 수 있습니다.  

간단하게 brute force로 최댓값의 범위를 모두 돌아가며 조건에 맞는 최댓값을 구하는 경우를 생각해보면 이 부분만 이분 탐색을 활용하면 이분 탐색으로 최댓값을 구하는 게 됩니다. lower, upper bound와 맥락은 똑같습니다. 탐색 후에도 break하지 않고 더 탐색하면 됩니다. 최댓값을 구해야 하니 오른쪽 부분을 탐색하면 되겠습니다. 코드는 아래와 같습니다.
```python
def cal_max(start, end):
    tmp = -1
    while start <= end:
        mid = (start+end)//2
        if function(mid):
            tmp = mid
            start = mid+1
        else:
            end = mid-1
    return tmp
```
주의해야 할 점은 여기서는 데이터의 인덱스가 아니라 최댓값을 확인해봐야 하는 값의 범위가 start, end라는 것입니다. 문제마다 function의 구현은 다르겠지만 일반적인 이분 탐색 문제와 똑같은 구조입니다. 그리고 여기서는 최댓값을 구하는 문제이므로 조건 만족 시 오른쪽을 확인하게 짰습니다. function의 경우는 따로 적지 않겠습니다. function을 짤 때 주의할 점은 이분 탐색의 전체 시간복잡도가 nlogn이라는 것입니다. 위의 구조에서 function의 시간복잡도가 n을 넘어가게 되면 시간복잡도가 >nlogn이 되어 이분 탐색의 효율을 떨어뜨립니다.

## 생각
이분 탐색(binary search) 문제를 몇 문제 푸니까 알고리즘의 구조가 확실하게 보여서 기록해봤습니다. 또 기록하려고 문제들을 다시 풀어봤는데 처음에는 조금씩 다르게 코딩했던 걸 같은 구조로 통일 시킬 수 있었습니다. 이런 식의 글을 작성하면서 배우는 점이 많은 것 같습니다. 앞으로도 카테고리별로 묶을 수 있는 경우가 생기면 이런 식으로 정리를 해야겠습니다.  
### *추가
인터넷에 깔끔한 lower, upper bound 코드가 직관적으로 이해가 안 돼서 tmp를 사용한 코드를 사용했는데 나중에 다른 문제들을 풀다 보니 위의 코드는 해당하는 값이 없으면 == 조건에 들어가지 못하고 tmp값을 변경하지 못하고 리턴 하는 값도 엉뚱한 값인 문제가 있었습니다. 따라서 문제의 조건에 해당하는 값이 반드시 있다고 주어지지 않으면 아래와 같은 코드를 사용해야 합니다.
```python
def lower_bound(start, end, target):
    while start < end:
        mid = (start+end)//2
        if data[mid] >= target:
            end = mid
        else:
            start = mid+1
    return end

def lower_bound(start, end, target):
    while start < end:
        mid = (start+end)//2
        if data[mid] > target:
            end = mid
        else:
            start = mid+1
    return end
```
위 코드에서 end값은 제가 짠 코드와 다르게 인덱스의 end보다 1 큰 값입니다.(len(data))


