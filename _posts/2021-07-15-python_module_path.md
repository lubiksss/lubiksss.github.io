---
last_modified_at : 2021-07-15
layout : single
title:  "python import module 경로 확인하기"
categories: python
tags : [python, import module, system path]

toc: true
toc_sticky: true
---
## 서론
python 사용 시 module이 import가 제대로 되지 않는 경우가 있습니다. 이 경우 보통 그 module을 import 할 때 사용하는 system path를 정확히 고려하지 않은 경우입니다. 따라서 아래와 같이 system path를 추가하게 되면 module이 제대로 import 됩니다. 제 프로젝트 파일을 예로 설명하겠습니다.

## system path 추가
아래는 제가 지금 공부하고 있는 프로젝트 파일 구조입니다.
```
DLFS
│
├─1_HELLOPYTHON
│  └─  ex_matplotlib.py
│
├─2_NEURALNETWORK
│  └─ MNIST_ex.py
│
├─data
│  └─  lenna.png
│
├─dataset
│  └─ mnist.py
│
└─lib
   └─ activation_function.py
```
이 경우 2_NEURALNETWORK 폴더 안에서 MNIST_ex.py를 편집하면서 lib 폴더의 activation_function.py를 import 하고 싶어서 아래 코드를 적어도 module이 import 되지 않습니다.
```python
import activation_function
```
```
ModuleNotFoundError: No module named 'activation_function'
```
이유는 파이썬 코드가 실행될 때 module을 import 하는 경로를 system path와 현재 폴더 내로 설정하기 때문입니다. 따라서 아래와 같이 코드를 수정하여 system path에 상위 폴더를 추가해주게 되면 제대로 import 되게 됩니다.
```python
import sys,os
sys.path.append(os.pardir)
import lib.activation_function
```
하지만 보통 프로젝트가 이런 구조를 가지진 않을 것 같습니다. 학업용이기 때문에 챕터를 분리해서 폴더를 넘나드는 구조를 가지게 되었지만, 보통은 메인 파일과 같은 폴더 안에 lib나 data폴더를 같이 두는 게 좋을 것 같습니다.
