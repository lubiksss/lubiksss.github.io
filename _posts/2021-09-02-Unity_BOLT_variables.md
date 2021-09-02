---
last_modified_at : 2021-09-02
layout : single
title:  "Unity Variables"
categories: Unity
tags : [BOLT, Variables]

toc: true
toc_sticky: true
---
## 서론
### *참고
<a href='https://www.youtube.com/watch?v=C3u-qeanSy8'>볼트 - 변수 | 유니티</a>

## BOLT Variables
1번부터 6번까지의 순서대로 넓은 범위로 간다고 보면 됩니다.
1. Flow Variables  
가장 짧은 기간 동안 존재하는 변수로 그래프 안에서 하나의 Flow가 진행하는 동안에만 존재합니다. 같은 그래프 안에서도 다른 Flow라면 사용할 수 없습니다.
2. Graph Variables  
하나의 그래프 안에 있는 모든 flow 들이 공유 가능한 변수입니다.
3. Object Variables  
그래프를 넘어 같은 게임 객체에 붙어있는 그래프끼리 공유할 수 있는 타입의 변수입니다. 다른 게임 객체의 변수는 사용할 수 없습니다.
4. Scene Variables  
객체보다 넓은 변수로 같은 씬안의 있는 모든 객체들이 접근해서 사용할 수 있는 변수입니다.
5. App Variables  
씬이 바뀌어도 유지되는 변수로 게임이 실행되는 순간부터 종료되는 순간까지 공유됩니다.
6. Saved Variables  
게임이 종료된 이후에도 값이 유지되는 변수입니다. 게임이 종료 돼도 값이 유지되기 때문에 게임 데이터를 저장하는 데 사용됩니다. 하지만 값을 레지스트리에 저장하기 때문에 보안의 이유로 데이터를 저장하기보다는 설정값을 저장하는 용도로 사용하는 것이 좋습니다.

## 생각