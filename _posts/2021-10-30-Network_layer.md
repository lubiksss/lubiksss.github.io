---
last_modified_at : 2021-10-30
layout : single
title: "Network layer"
categories: Network
tags : [Network, layer]

toc: true
toc_sticky: true
---
## 서론
### 참조
<a target = '_blank' href='https://www.youtube.com/watch?v=D_GGPjn_Fds&list=PLQFHF6cwEgwM7qKyoF2QnUPE3AVub7leJ&index=1'>(3)Computer Network (계층모델별 특징)</a>

* 간단한 키워드를 통해서 정리해보겠습니다.

## Application Layer
* Application에서 Data가 생성/처리되는 계층
* Application 별로 사용하는 Protocol 정의되어, 하위 Transport layer와 Socket 연결됨

## Transport Layer
* Application에서 내려온 Data에 TCP/UDP 헤더를 추가 하여 Segment화
* TCP : Connection Oriented, Reliable, Flow Control
* UDP : Connectionless, Unreliable, Congestion Control

## Network Layer
* 상위 Transport Layer에서 만든 Segment에 헤더를 붙여 packet을 만드는 단계(IP헤더)
* End to End Device의 식별(Addressing), Routing(내 주변의 어디로 보내야 할지의 결정)
* 기본적으로 IP Packet자체는 Connectionless이다.

### IP Address
<img src = 'https://user-images.githubusercontent.com/67966414/139518324-4ae0947d-0667-4ed9-96b1-00b524390db1.png' alt = 'IP_class' style="margin-left: auto; margin-right: auto; display: block;">  


### Routing
* 라우팅 테이블: netstat -r
* Destination IP를 보고 해당 Packet을 어디(어떤 인터페이스)로 내보낼지를 결정하는 과정
* Routing Table을 만들어 이용, 선택 과정
* 같은 네트워크면 그냥 그 IP로 보내면 되지만 같은 네트워크가 아니면 무조건 게이트웨이로 보낸다. 이 뜻은 게이트웨이의 MAC 어드레스를 써서 보낸다는 소리이다.
* 라우터의 경우는 여러 네트워크에 연결돼 있으므로 IP를 보고 어느 쪽으로 어느 네트워크로 보낼지를 결정한다.
* 가장 중요한 것은 라우팅 테이블을 어떤 식으로 만드냐이다.

## Datalink Layer(Ethernet)
* 상위 IP Layer에서 넘어온 정보에 Ethernet 헤더를 붙여 Frame을 만드는 과정 진행
* Ethernet Protocol: Source, Destination MAC Address, ARP과정, LAN->WAN
* 라우팅을 통해서 Next Hop IP를 찾을 수 있고
* ARP를 통해서 Next Hop IP의 MAC address를 찾을 수 있다
* 보통 MAC주소를 physical, IP주소를 logical이라고 함

### ARP
* ARP 테이블: arp -a
* Ethernet 헤더 상의 destination MAC 주소를 완성하기 위해 사용(내가 만들어 보낸 Frame을 누가 받아야 하는지를 결정)
* ARP Table 생성(Request/reply) / 관리(timer), GARP
* ARP는 브로드 캐스트로 보냄. host 주소를 모두 255로 보내는 것. => 당연하다 MAC 주소를 모르니까 전부 모두에게 보내야 함.
* 스위치는 브로드 캐스트 받으면 받은 인터페이스 빼고 모든 인터페이스로 다 보냄.
* 테이블 안에서 dynamic이면 이런 ARP 쿼리를 통해서 받은 것이고 static이면 그냥 메모리상에 박혀있다는 뜻


### GARP
1. IP 주소 충돌 감지  
자신의 IP 주소를 타겟으로 하여 ARP 요청을 보낸다. 만약 다른 호스트가 이에 대한 응답이 있으면 이미 해당 IP 주소를 사용하는 호스트가 존재함을 뜻한다.
2. ARP 테이블 갱신  
누군가가 GARP 패킷을 보내면, 이를 수신한 모든 호스트/라우터는 GARP 패킷의 Sender MAC과 IP Address로 자신의 ARP 테이블을 갱신한다.
3. VRRP/HSRP  
위 프로토콜에서 사용한다고 하는데 나중에 자세히 공부하겠습니다.

## Physical Layer
* Frame을 전기적인 신호로 변환하여 전달하는 기능
* 매체(Media)에 따라 구성요소, 가능 B/W, 제약사항 등에 대한 숙지 필요

## 생각
ARP가 Network Layer랑 Data Link Layer에서 혼용되는 것 같은데 뭐가 정확한지 궁금합니다. 구글링을 해도 혼용해서 사용되고 있는 것 같습니다.
