---
last_modified_at : 2021-09-11
layout : single
title:  "Unity TopDownRPG"
categories: Unity
tags : [C#, TopDownRPG]

toc: true
toc_sticky: true
---
## 서론
### *참고
<a href='https://www.youtube.com/watch?v=JY-KFx3OsJo&list=PLO-mt5Iu5TeYfyXsi6kzHK8kfjPvadC5u'>탑다운 2D RPG - 도트 타일맵으로 쉽게 준비하기 [유니티 기초 강좌 B20 + 에셋 다운로드]</a>
<a href='https://github.com/lubiksss/TopDownRPG'>github_백업용</a>

Unity로 2D TopDown RPG를 만들었습니다. BOLT를 사용하지 않고 C# Script로만 구현했습니다. 지난 프로젝트들에서 BOLT를 사용하면서 Script를 사용하지 않은 것에 대한 답답함이 있었는데 이번 프로젝트를 하면서 Script로만 구현해보면서 두 가지 다 활용하는 게 좋을 것 같다고 생각했습니다.  
이번에 만들면서 제일 배운 게 많습니다. 크게 세 가지를 배웠습니다.
1. 퀘스트 시스템 구현
2. NPC 대화 구현
3. 모바일 건설을 위한 버튼으로 인풋 받기
4. Save, Load 시스템  

지금까지 사용했던 Game Manager나 Sound Manager처럼 Quest Manager, Talk Manager를 구현하고 Game Manager를 통해 접근하는 방법을 배웠습니다. 또 이번에는 모바일 빌드를 목적으로 했기 때문에 일반 Unity에서 제공하는 PC 입력이 아닌 Button UI를 통해 입력을 직접 받았고, PC와 모바일에서 둘 다 호환 가능한 input system을 만들었습니다.  

또 Save, Load 시스템을 구현했는데 이건 현재 구글 플레이에서 사용 중인 계정 로그인 형태는 아니고 그냥 모바일 기기 내에 저장하는 방법입니다. Unity 자체에서 기능을 제공하기 때문에 굉장히 간단합니다. 이 기능은 보안에 굉장히 취약하므로 다음에 진짜 개발을 할 때는 계정연동이나 서버 연동 같은 시스템을 만들어야 할 것 같습니다.  

특히 퀘스트를 구현하는 부분이 특정 순서에 맞게 퀘스트를 흘러가게 해야 하고 연속된 퀘스트를 구현하는 등 가장 어려웠습니다. 후에 퀘스트 부분에 대해서 더 공부하고 추가하도록 하겠습니다.  

현재로선 Github에 올리는 이유가 버전관리보다는 Backup의 목적이 큰데 C# Script를 사용하였을 경우 필요할 경우 바로 열어볼 수 있어서 좋은 것 같습니다.

## Preview
<div>
    <img src="https://user-images.githubusercontent.com/67966414/132933860-340c1516-b505-4544-8e96-bf3e4c5e2860.jpg" alt="test" style="width:24%;"/>
    <img src="https://user-images.githubusercontent.com/67966414/132933857-dbc81267-a624-48f3-8e8c-34cc063f65ed.jpg" alt="UI" style="width:24%;"/>
    <img src="https://user-images.githubusercontent.com/67966414/132933859-99504a69-926b-49d8-ad3b-483c9747ab90.jpg" alt="NPCA" style="width:24%;"/>
    <img src="https://user-images.githubusercontent.com/67966414/132933858-244c8e17-7e10-4122-805b-e1107bc3bca9.jpg" alt="NPCB" style="width:24%;"/>
</div>

