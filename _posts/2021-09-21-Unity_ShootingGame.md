---
last_modified_at : 2021-09-21
layout : single
title:  "Unity ShootingGame"
categories: Unity
tags : [C#, ShootingGame]

toc: true
toc_sticky: true
---

## *참고
<a href='https://www.youtube.com/watch?v=ETYzjbnLixY&list=PLO-mt5Iu5TeYtWvM9eN-xnwRbyUAMWd3b&index=1'>2D 종스크롤 슈팅 - 플레이어 이동 구현하기 [유니티 기초 강좌 B27 + 에셋 다운로드]</a>  
<a href='https://github.com/lubiksss/ShootingGame'>github_백업용</a>

Unity로 Shooting Game을 만들었습니다. 튜토리얼을 거쳐서 이번엔 정말 게임다운 게임을 만든 것 같습니다. 고민도 정말 많이 했고 게임을 만드는 기술도 많이 배웠습니다. 이번 프로젝트가 지금까지 배운 모든 것들의 집약체이기 때문에 이번 프로젝트는 작성한 스크립트나 배운 기술들을 정리해보도록 하겠습니다.

## Preview
<div>
    <img src="https://user-images.githubusercontent.com/67966414/137348947-b342bf9c-f3a4-43b3-8a1a-f8c0c11788dc.jpg" alt="1" style="width:24%;"/>
    <img src="https://user-images.githubusercontent.com/67966414/137348954-27063584-ce64-4c85-855b-4740622f4128.jpg" alt="2" style="width:24%;"/>
    <img src="https://user-images.githubusercontent.com/67966414/137348955-6dbdc93b-a1ef-4cfa-a07b-e42304c37c73.jpg" alt="3" style="width:24%;"/>
    <img src="https://user-images.githubusercontent.com/67966414/137348958-cc15c754-1df0-4f04-93e6-390c6ea2090a.jpg" alt="4" style="width:24%;"/>
</div>
<div>
    <img src="https://user-images.githubusercontent.com/67966414/137348963-348aaa7f-4be9-4b00-80e5-9c65433e748c.jpg" alt="Boss1" style="width:24%;"/>
    <img src="https://user-images.githubusercontent.com/67966414/137348965-ea445288-df5d-4368-bc2a-657b6141f7b7.jpg" alt="Boss2" style="width:24%;"/>
    <img src="https://user-images.githubusercontent.com/67966414/137348968-ebee1cad-ef5b-48c7-bb79-0baf33b3332f.jpg" alt="Boss3" style="width:24%;"/>
    <img src="https://user-images.githubusercontent.com/67966414/137348970-0652d247-eef4-4a8e-a466-a1e75f360c4e.jpg" alt="Boss4" style="width:24%;"/>
</div>


## Unity 기본
### 객체의 컴포넌트 제어
유니티에서 각 객체는 여러 가지 컴포넌트를 가질 수 있습니다. 이 컴포넌트라는 것은 그 객체의 특징을 설명하는 것이라고 보면 됩니다. 그 컴포넌트들을 잘 조합하여 객체의 특징을 잘 정의하는 것이 게임에서의 객체 1개를 만들어내는 것과 같습니다.  

모든 객체는 기본적으로 Transform이라는 위치정보를 담은 객체를 가집니다. 또한 특정한 예를 들면 Player라는 객체는 이미지를 담고 있는 Sprite Renderer라는 컴포넌트를 가지고 PlayerAction이라는 스크립트 컴포넌트를 가지며 Animator, Collider, Rigidbody등의 객체를 갖습니다. 이름이 굉장히 직관적이기 때문에 무슨 특징을 가질지 바로 알 수 있습니다. 제가 만든 Player는 아래와 같은 컴포넌트를 가집니다.  

<img src="https://user-images.githubusercontent.com/67966414/134113892-fafce52f-63b8-48f8-9d8b-2f86af1c5359.png" alt="Component" style="margin-left: auto; margin-right: auto; display: block">
<br>
이런 컴포넌트를 PlayerAction이라는 스크립트에서 컨트롤하기 위해서는 아래와 같이 쓸 수 있습니다. Animator 타입의 변수를 설정하고, 그 변수를 Awake라는 Unity 함수에서 초기화 한 뒤 일반 변수 사용하듯이 사용할 수 있습니다. 이렇게 하면 객체의 스크립트 컴포넌트에서 모든 컴포넌트를 사용할 수 있게 해줍니다.

```cs
// Player Script
public Animator animator;
void Awake()
{
    animator = GetComponent<Animator>();
}
animator.SetInteger("isLR", (int)h);
```

### 객체에서 다른 객체를 제어
게임을 만들 때 객체는 Player만 있는 것이 아니기 때문에 모든 객체는 다른 객체를 제어할 수 있어야 합니다. 예를 들어 GameManager라는 객체는 Player를 부활시키기 위해 Player라는 객체를 제어해야 하는데 이 부분은 Unity Editor를 아래와 같이 사용합니다. 우선 GameManager 스크립트 안에서 player라는 GameObject변수를 public으로 선언하고 Editor를 통해서 그 변수에 Player 객체를 넣어주어야 합니다.
```cs
// GameManager Script
public GameObject player;

// Editor를 통해 객체를 넣어 주지 않으면 사용 불가능.
void RespawnPlayerExe()
    {
        player.transform.position = Vector3.down * 4;
        player.SetActive(true);
        // 이것처럼 객체를 넣었기 때문에 객체 아래의 컴포넌트도 모두 접근 할 수 있다.
        PlayerAction playerLogic = player.GetComponent<PlayerAction>();
        playerLogic.isHit = false;
    }
```
위에서는 객체 자체를 넣고 컴포넌트를 불러와서 사용했지만, 그냥 컴포넌트 자체를 넣을 수도 있습니다. 아래는 GameManager에 객체와 컴포넌트가 참조되고 있는 모습입니다.  

<img src="https://user-images.githubusercontent.com/67966414/134115486-10fd4a05-41ce-4066-b083-3bc676f7ca85.png" alt="GameObject" style="margin-left: auto; margin-right: auto; display: block">
<br>

## 객체별 분석
많은 객체가 등장하지만 몇몇 객체들만 정리하면서 복습해보도록 하겠습니다. 객체를 어떤 식으로 다시 분석해보면 좋을까 생각하다가 스크립트를 기준으로 분석하며 복습해보도록 하겠습니다.

### Player
1. Move  
기본적인 움직임입니다. 모바일 빌드를 하였기 때문에 JoyPad를 9칸으로 나눠 각 칸의 버튼이 눌렸을 시 8방향으로 움직일 수 있습니다. 카메라 라인 밖으로 나갈 수 없게 예외 처리 되어있으며 Update함수에서 불리기 때문에 Time.deltaTime을 사용하여 각 환경에서의 속도를 맞췄습니다.
2. Fire  
총알 발사에 대한 처리가 되어있습니다. 버튼 인풋을 받아 총알을 발사합니다. 파워에 따라서 총알의 모양이 바뀌며, 총알을 불러오는 것은 미리 선언되어 있는 Objectpool에서 불러옵니다. 불러옴과 동시에 총알의 강체에 힘을 주고 속도를 정해줍니다.
3. Boom  
기본적인 슈팅 게임에 있는 필살기입니다. 버튼 인풋을 받아 실행하고, 맵 상의 모든 적과 총알을 없앱니다. 역시 Objectpool에 Object들을 모두 반납합니다.
4. OnTriggerEnter2D  
충돌에 대한 모든 정리가 되어있습니다. 카메라 가장자리에 대한 충돌, 적과 적 총알에 대한 충돌, Item과의 충돌이 있습니다.

### Enemy
Enemy는 처음부터 맵상에 존재하지는 않습니다. Prefab으로 저장이 되어있으며 GameManager가 stage를 불러와서 그에 따라서 spawn을 하는 구조입니다. 이번에 배우게 된 건데 Prefab들은 Prefab상태에서 다른 객체를 참조할 수가 없습니다. 따라서 GameManager에서 Prefab을 spawn 할 때 Enemy가 사용해야 하는 객체를 따로 넘겨주어야 합니다.
1. Move(없음)  
Enemy는 Move가 없습니다. 기본적으로 GameManager가 Enemy를 spawn할때 아래 방향으로 힘을 주면서 spawn하기 때문에 아래 방향으로만 움직이고 다른 Move는 없습니다. 만약 랜덤적인 움직임이나 인공지능을 통한 움직임을 주려면 이 부분도 추가하면 될 것 같습니다.
2. Fire  
Player의 Fire와 같지만, 인풋을 받지 않고 자동으로 쏩니다. Enemy의 경우 Boss제외 3가지 종류가 있으므로 종류에 따른 코딩이 되어있습니다.
3. OnTriggerEnter2D  
Player와 마찬가지로 충돌에 대한 모든 정리가 되어있습니다. Enemy의 경우는 플레이어와의 충돌, 플레이어의 총알과의 충돌입니다.

### Boss(Enemy)
Boss는 기본적으로 Enemy입니다. 처음 코드를 짤 때 공통부분을 짜고 Boss가 상속받았으면 좋았을 텐데 그렇게 하지 못했고 Enemy안에서 if 문으로 Boss에 대한 컨트롤을 했습니다. 일반 Enemy와 다른 점은 4가지 총알 패턴을 가진다는것인데 이 부분은 모두 총알을 불러오고 강체에 힘을 제각기 주거나 타이밍을 주고 주는 방법이기 때문에 따로 적진 않겠습니다. github에서 열어보면 자세하게 볼 수 있습니다.
1. FireForward
2. FireShot
3. FireArc
4. FireAround

### GameManager
처음에 튜토리얼들을 진행할 때 GameManager라는 오브젝트를 두는 걸 보고 '이런걸 따라 하면서 게임메이킹에 대해서 배우는 거구나' 라고 생각했었습니다. GameManager는 게임 내 등장 객체들이 하는 일을 제외한 모든 일을 한다고 생각하면 됩니다.
1. SpawnEnemy  
기본적으로 Enemy는 Prefab으로 저장되어있고 GameManager객체가 text형식으로 저장된 stage를 읽어서 시나리오대로 Enemy를 spawn합니다.
2. RespawnPlayer  
플레이어를 respawn합니다.
3. StageStart
4. StageEnd
5. GameOver
6. GameRetry
7. 각종 UI 업데이트

### ObjectManager
ObjectPooling이라는 개념은 이번 프로젝트에서 처음 해본 개념입니다. 게임 내에서 사용할 Object들을 미리 모두 초기화시켜놓고 사용할 때만 active하고 사용 후에는 deactive하여 다시 pool로 돌아오게 합니다. 적들이나 총알들을 Prefab으로 저장해두고 그때그때 초기화해서 쓸 수도 있지만 이렇게 되면 프로세서의 자원을 많이 잡아먹게 되어 framedrop이 일어날 수 있기 때문에 ObjectPooling을 사용한다고 합니다.
1. Generate  
사용할 Object들을 모두 초기화합니다.
2. MakeObj  
다른 함수에서 Objpool에서 Obj를 불러올 때 사용합니다. 이 함수를 호출 시 ObjectManager는 사용하지 않고 있는 Obj를 리턴해서 주게 됩니다.
3. GetPool  
풀 안의 모든 Obj를 전부 불러올 때 사용합니다. 이번 프로젝트에서는 Player가 Boom을 사용할 때 모든 Obj를 없애기 위해서 사용했습니다.


## 생각
스크립트를 정리하면서 코드에 대해서 정리를 하게 될 줄 알았는데 사실 코드는 딱히 적을게 없는 것 같습니다. 어차피 보려면 github에서 모두 볼 수 있습니다. 프로젝트를 진행하면서 배운 건 코드 구현도 있지만, 게임의 구조나 흘러가는 flow인 것 같습니다. 구현하는 기술 자체가 어려운게 아니면 구현이야 구글링을 통해서도 할 수 있는 거고 이런 게임 구조에 대해서 배우면서 게임메이킹에 대해서 알아가는 것 같습니다.  

복습은 많이 됐습니다만 기본적으로 기획안 없이 무작정 따라 만들고 나서 나중에 정리해보려니까 정리도 이렇게 두서없이 되는 것 같습니다. 유니티나 게임 만들기 커뮤니티 글들을 볼 때 기획안에 대한 어려움을 토로한 글들을 많이 봤었는데 그 부분에 대해서 정확히 공감하게 된 것 같습니다. 다음번에 제가 기획한 게임을 만들게 된다면 기획안부터 작성해서 차근차근 정리하고 게임을 만들어보도록 해야겠습니다.
