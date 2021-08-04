---
last_modified_at : 2021-08-05
layout : single
title:  "파이썬 함수로 인자 전달"
categories: python
tags : [call by value, mutable, object]

toc: true
toc_sticky: true
---
## 서론
파이썬에 대한 얕은 지식으로 알고리즘 문제를 풀려고 하다 보니 파이썬의 근본적인 개념을 알아야 하는 상황이 왔습니다. 코딩 문제를 풀 때 메모리 제한을 피하고자 `괜히 함수에 인자로 복사하여 메모리 잡아먹지 말고 전역변수로 사용하는 것이 좋습니다`라는 표현을 썼었는데 이 부분이 저도 이해가 안 되는 상황이 왔습니다.

## 함수로 인자 전달
우선 파이썬의 모든 것은 객체이고 객체는 두 가지 종류가 있습니다. immutable 객체(int, string, tuple)와 mutable 객체(list, dict)입니다.  

immutable 객체는 함수에 인자로 전달될 때 call by value 형식으로 전달되고 mutable 객체는 함수에 인자로 전달될 때 call by reference 형식으로 전달됩니다. 이런 특징 때문에 파이썬은 call by assignment라는 이름을 갖습니다.

## 생각
1. 그럼 사실상 함수로 mutable 한 객체인 int나 string을 전달 할 때는 몇 개 되지도 않는데 매개변수로 받아도 메모리를 얼마 안 먹지 않을까? immutable 한 객체인 list를 전달할 때도 값을 복사하는 게 아닌 call by reference니, 실질적으로는 메모리를 얼마 안 먹지 않을까? 하는 궁금증이 생깁니다.

2. 근데 애초에 코딩 문제 구조가 한파일 안에서 주어진 값들은 전부 전역변수로 쓰는데 굳이 함수에 인자로 전달해야 할까? 도 뭔가 해결이 안 됩니다.

우선 까먹을까 봐 적어놨습니다. 해결되는 대로 고쳐서 적도록 하겠습니다.


