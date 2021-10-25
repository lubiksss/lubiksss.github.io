---
last_modified_at : 2021-10-25
layout : single
title:  "python 숫자 객체"
categories: python
tags : [python, 소팅, sorting]

toc: true
toc_sticky: true
---
## 서론
### 참조
<a target = '_blank' href='https://tyanjournal.com/tips/python-int-type-%EB%B3%80%EC%88%98%EC%9D%98-identity-%EB%B0%8F-console%EA%B3%BC-script%EC%97%90%EC%84%9C%EC%9D%98-%EC%8B%A4%ED%96%89-%EA%B2%B0%EA%B3%BC/'>[Python] int type 변수의 identity 및 console과 script에서의 실행 결과</a>  
<a target = '_blank' href='파이썬의 효과적인 메모리 재활용 방법 - Interning'>[Python] int type 변수의 identity 및 console과 script에서의 실행 결과</a>  

기존에 공부할 때 파이썬에서는 자주 사용하는 숫자(-5~256)도 객체로 만들어 넣고 그 객체를 생성할 시 기존에 만들어져있던 reference를 리턴한다고 배웠습니다. 근데 이 실행 결과가 콘솔(interpreter)에서와 에디터(.py)에서가 다릅니다.

## 결과
콘솔에서는 공부했던 거처럼 숫자 257부터는 서로 다른 객체를 생성하게 되어 257부터는 서로가 다른 객체를 가리키게 되어 a is b의 결과가 false가 나오는 것을 볼 수 있습니다.
```cmd
>>> a = 255
>>> b = 255
>>> a is b
True
>>> a = 256
>>> b = 256
>>> a is b
True
>>> a = 257
>>> b = 257
>>> a is b
False
```
하지만 에디터를 통해(저는 vscode를 사용했습니다.) .py을 생성하고 그것을 컴파일하여 돌려 보게 되면 모두 True가 나옴을 확인 할 수 있습니다. 왜 그런지 한참을 이유를 찾았는데 이 이유는 컴파일러가 코드를 분석하고 bytecode를 최적화하기 때문이라고 합니다.
```python
a = 255
b = 255
print(a is b)

a = 256
b = 256
print(a is b)

a = 257
b = 257
print(a is b)
```
```cmd
True
True
True
```

## 생각
그럼 이 결과가 어떻게 보면 python의 원리에 어긋나는 결과 같은데 컴파일러가 이렇게 맘대로 바꿔도 되는지 모르겠습니다. 일단 그렇다고 이해는 했는데 이 부분을 어떻게 해석해야 할까요.  
참조링크에 설명이 쓰여 있긴 한데 그렇게 바꾼 합리적인 이유에 대해서는 쓰여 있진 않습니다.
