---
last_modified_at : 2021-09-04
layout : single
title:  "Unity Platformer"
categories: Unity
tags : [C#, Platformer]

toc: true
toc_sticky: true
---
## 서론
### *참고
<a href='https://www.youtube.com/watch?v=v_Y5FH_tCpc&list=PLO-mt5Iu5TeZGR_y6mHmTWyo0RyGgO0N_'>2D 플랫포머 - 프로젝트 준비하기 [유니티 기초 강좌 B13 + 에셋 다운로드]</a>
<a href='https://github.com/lubiksss/Platformer'>github_백업용</a>

Unity로 만든 2D 플랫포머 게임입니다. 이번에는 BOLT를 사용하지 않았으며 C# Scripting으로만 구현했습니다.  

일반적인 2D 플랫포머 게임입니다.
사용된 객체는 플레이어, 몬스터, 아이템, 플랫폼이며 각 객체의 이동, 충돌 등을 구현했습니다. 또 게임매니저, 사운드매니저라는 게임 객체를 통해 각종 게임의 효과를 구현했습니다.  
이번에는 BOLT를 사용하지 않았기 때문에 C#스크립트가 그대로 구현되어 있는데 다음에 사용할 때 쉽게 참고할 수 있겠습니다.

## Platformer
![normal](./images/test.JPG)
![collide](./images/collide.JPG)

## 생각
처음에 Unity를 공부할 때 자료를 볼트로 시작해서 C#스크립트를 작성하지 않는 것에 대한 찝찝함이 있었는데 이번 프로젝트를 하면서 사실상 BOLT에서 배운 모든 기능을 C#으로 구현할 수 있게 되었습니다. 딱 하나 객체의 State를 이동하는 부분을 C#으로 배우지 않았는데 이 부분만 해결하면 BOLT와 C#을 동시에 사용할 수 있게 될 거 같습니다. 다음에 또 공부하면서 C#으로 State 관련 개념을 구현하게 되면 적도록 하겠습니다.