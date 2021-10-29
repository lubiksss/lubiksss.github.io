---
last_modified_at : 2021-10-29
layout : single
title: "Network protocol"
categories: Network
tags : [Network, protocol]

toc: true
toc_sticky: true
---
## 서론
### 참조
<a target = '_blank' href='https://www.youtube.com/watch?v=8kI5OIrfZtI&list=PLQFHF6cwEgwMcGFaqV8oe_Eqq5jlFMOvW'>(2)Computer Network (Data 전달과정)</a>

* 간단한 키워드를 통해서 정리해보겠습니다.
* 완벽하게 제가 궁금했던 정보가 있습니다. 네트워크 지식이 파편으로 있었는데 조금 정리가 되는 것 같습니다.

## Protocol
* 통신에 참여하는 주체 간의 Data를 주고받는 과정을 정의한 규칙
* 효율성, 호환성을 위해 정해 놓은 규칙으로 다수의 업체와 관련 제품군의 등장 및 이용 가능
* 통신을 위해 사용하는 프로토콜이 엄청 많다. 통신하는 컴퓨터끼리는 같은 프로토콜들을 사용해야 통신할 수 있는데 이 사용하는 프로토콜들을 프로토콜 스택이라고 한다. 현재는 TCP/IP 프로토콜 스택이 가장 많이 사용된다.
* 실제로 하는 것
1. Data(Message)의 포맷과 구조화
2. Network Device에서 어떻게 처리할 것인지에 대한 정보
3. Device간의 Error 처리에 대한 방식
4. Data 전송 절차의 Setup과 종료

## OSI 7 Layer
<img src = 'https://user-images.githubusercontent.com/67966414/139423591-3b4ef903-ff52-4f2b-8258-9425fe152607.png' alt = '네트워크계층' style="margin-left: auto; margin-right: auto; display: block;">

* Data가 전달되기 위한 과정을 계층화 => 모듈화
* 복잡도를 줄이고, 모듈화를 통한 기술 발전, 호환성 가능, 상호 독립성을 가질 수 있음.
* OSI 7 Layer는 이론적인 참조 모델이고 실제론 TCP/IP 모델을 사용한다.
1. Application
2. Presentation
3. Session
4. Transport
5. Network
6. Data Link
7. Physical
* TCP/IP
1. Application
2. Transport
3. Network
4. Network Access

## 캡슐화/디캡슐화
<img src = 'https://user-images.githubusercontent.com/67966414/139423571-b7bce995-0731-4e96-8a1e-f90bfe7ca4c0.png' alt = '캡슐화' style="margin-left: auto; margin-right: auto; display: block;">

1. Application에서 만들어진 Data가 해당 Device에서 네트워크를 통해 전달되는 과정
2. 각 계층에서 동작하는 protocol 별로 정보(헤더)가 추가되고, 벗겨지는 과정
3. 네트워킹한다는 의미의 기술적인 설명임

## 헤더
각각의 헤더는 아래의 정보를 담고 있다.
1. Application
    * Encoded application data
2. Transport
    * Destination and Source process number (ports)
    * TCP/UDP information
3. Network
    * Destination and Source logical network addresses (IP Addr.)
4. Data link
    * Destination and Source logical physical addresses (MAC Addr.)

## 캡술화(Encapsulation)
1. Application에서 data가 만들어진다.
2. Transport 계층으로 data가 내려오고 거기에 sport와 헤더로 붙여서 Segment가 만들어진다. (TCP의 경우는 이런 걸 하기 전에 연결을 확보하는데 그것은 TCP 프로토콜을 공부하면서 다시 적겠습니다.)
3. Network 계층으로 Segment가 내려오고 거기에 sIP와 dIP를 붙여서 Packet을 만든다.
4. 이때 그럼 dIP를 어떻게 구할 것이냐는 DNS를 통해서 구한다.
5. 마지막으로 Data Link 계층으로 Packet이 내려오고 sMAC과 dMAC을 붙여서 Frame을 만든다.
6. 그럼 dMAC은 어떻게 아느냐? 목적지로 바로 가는 것이 아니기 때문에 Next Hop의 MAC주소를 적는다. Next Hop의 MAC주소는 라우팅 테이블에 쓰여 있다. 그리고 라우팅을 통해서 Next Hop의 IP를 구하는 것이 라우팅.
7. 이제 이게 전기적인 신호로 네트워크로 들어가게 된다.

## 스위치
스위치는 Frame을 받고 Frame을 해석할 수 있는 기능이 있다. Frame을 해석해서 내가 어떤 Interface로 Frame을 다시 내보내야 하는 지를 판단한다.

## 라우터
라우터도 Frame을 받는다(사실 모든 네트워크 장비는 Frame을 받는다.) Frame을 해석해서 dMAC이 자기 자신의 MAC이면 Frame을 디 캡슐화해서 패킷을 또 해석한다. 패킷의 dIP정보를 보고 Next Hop의 dMAC주소(라우팅과 ARP로 확인함)로 다시 캡슐화해서 Next Hop으로 보낸다.

## 서버
결국 서버가 Frame을 받게 되면 dMAC도 자기 자신, dIP도 자기 자신이므로 패킷도 디 캡슐화하여 Segment를 확인하게 되고 Segment에 쓰여 있는 포트 번호를 확인하여 필요한 프로세스에 data를 전달하게 된다. 예제에선 HTTP 통신이었으니 index.html을 달라고 했을 테니 index.html을 돌려주게 된다.

## 생각
* 라우터들은 도착한 프레임 데이터를 까서 Destination IP를 확인한 후 그 IP를 가진 Terminal이 있으면 다시 MAC 주소로 캡슐화하여 보내거나 없으면 Next Hop에 해당하는 MAC 주소로 캡슐화하여 Next Hop으로 보낸다.
* 이 부분이 항상 궁금했다. layer를 거쳐서 한방에 캡슐화를 하고 받아서 한방에 디 캡슐화로 다 까보는 게 아니라 각 네트워크 장비들은 한 계층씩 디 캡슐화를 하며 목적지를 계속 확인하며 각 계층을 왔다 갔다 한다. 그리고 결국 마지막에 도착지에 도착했을 때 모든 layer를 디캡슐하게 된다.
* 호스트가 통신을 한다는 것은 각 계층에서의 헤더를 만드는 과정이다. 소스는 알 수 있지만 데스티네이션은 알 없으므로 destination IP는 DNS로, destination MAC은 Routing과 ARP로 알 수 있다.
* Framce의 dMAC정보만 계속 바뀌면서 네트워킹이 된다. 학교 수업을 들으면서도 너무나도 궁금하고 교수님도 알려주지 않았던\.\.\.드디어 알았습니다\.\.

<img src = 'https://user-images.githubusercontent.com/67966414/139431929-4a48e293-b66c-4ce4-a3e8-996f804761b5.PNG' alt = '네트워킹과정' style="margin-left: auto; margin-right: auto; display: block;">

