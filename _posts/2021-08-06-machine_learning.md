---
last_modified_at : 2021-08-06
layout : single
title:  "머신러닝 개요"
categories: ML
tags : [머신러닝, machine learning]

toc: true
toc_sticky: true
---
## 서론
머신러닝으로 프로젝트를 하고 있어서 조금 정리해볼 생각입니다.
### *참고
<a href='https://opentutorials.org/module/4916'>Opentutorials: Machine learning 1</a>

## 개요
### 머신러닝의 종류
<img src = 'https://user-images.githubusercontent.com/67966414/128478844-de6e59b8-0b61-46a0-b9f1-912287971a4f.jpeg' alt = '머신러닝 종류' style="margin-left: auto; margin-right: auto; display: block;">

## 지도학습 (Supervised Learning)
지도학습이란 기계를 가르친다(supervised)는 의미, 이미 답이 있는 데이터를 가지고 그 답이 나오도록 학습시킨다. 지도학습은 역사적이다. 과거의 원인과 결과를 바탕으로 결과를 모르는 원인이 발생했을 때 그것이 어떤 결과를 초래할 것인가를 추측하는 것이 목적이다. 독립변수와 종속변수가 필요하다.
1. 회귀(regression)
* 숫자를 예측하고 싶을 때 사용
* 정확히는 양적(Quantitative) 데이터를 예측하고 싶을때 사용한다.
2. 분류(classification)
* 이름 혹은 문자를 예측하고 싶을 때 사용
* 정확히는 범주(Categorical) 데이터를 예측하고 싶을때 사용한다.

## 비지도학습 (Unsupervised Learning)
비지도학습은 지도학습과 반대되는 의미, 즉 답을 알려주지 않았는데도 데이터에 대한 관찰을 통해 새로운 의미나 관계를 밝혀낸다. 비지도 학습은 탐험적이다. 탐험이 미지의 세계를 파악하는 것처럼 데이터들의 성격을 파악하는 것이 목적이다. 독립변수와 종속변수의 구분이 중요하지 않다. 데이터만 있으면 된다.
1. 군집화(clustering)
* 분류와 헷갈리지만 군집화는 분류할 그룹 자체를 만드는 것이다.
* 분류는 그 후에 어느 그룹에 속하는지를 판단하는 것이다.
2. 연관(association)
* 데이터 간의 연관성을 파악한다. 서로 관련이 있는 특성(열)을 찾아준다.
* 쇼핑 추천, 음악 추천, 영화 추천, 검색어 추천, 동영상 추천...등의 활용이 연관을 이용한 것이다.
3. 변환(transform)
* 데이터를 새롭게 표현하여 사람이나 다른 머신러닝 알고리즘이 원래 데이터보다 쉽게 해석할 수 있도록 만드는 것이다.
* 고차원 데이터의 특성의 수를 줄이면서 꼭 필요한 특징을 포함한 데이터로 표현하는 차원축소가 대표적인 예

## 강화학습 (Reinforcement Learning)
더 좋은 보상을 찾도록 강화한다는 의미, 학습을 통해서 능력을 향상한다는 점에서 지도학습과 비슷하지만 강화학습은 답을 알려주진 않는다. 모델 자체가 경험을 통해 더 좋은 답을 찾아가도록 하는 것이 목적이다. 강화학습의 핵심은 일단 해보는 것. 지도학습이 배움이라면 강화학습은 경험이다.
1. __
* 알파고, 자율 주행 자동차 같은 예가 있다.

## 문제에 필요한 머신러닝을 찾는 방법
<img src = 'https://user-images.githubusercontent.com/67966414/128483625-291b534e-3b4c-4ecf-a395-c7694072f7eb.jpeg' alt = '머신러닝 종류' style="margin-left: auto; margin-right: auto; display: block;">

## 생각
