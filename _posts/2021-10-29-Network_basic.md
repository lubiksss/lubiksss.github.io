---
last_modified_at : 2021-10-29
layout : single
title: "Network 기본"
categories: Network
tags : [Network, basic]

toc: true
toc_sticky: true
---
## 서론
### 참조
<a target = '_blank' href='https://www.youtube.com/watch?v=v9IVz5m_SCs&list=PLQFHF6cwEgwPYzMqIzpczc8sYe3VOe6Si'>(1)Computer Network (Overview)</a>

간단한 키워드를 통해서 정리해보겠습니다.

## 개념
1. Computere Device간에 Data가 전달되는 과정을 이해하는 것
2. 물리적/논리적인 흐름에 대한 이해
3. 전달 과정상에 존재하는 구성요소에 대한 이해

## 구성요소
1. Device
    * 데이터 자체를 생성하고 변환하는 컨셉이 아니고 단순히 전달만 한다.
    * End Device : PC, Server, SmartPhone, IoT기기 등
    * Networking Device : 전송 장비, Switch, AP, Router, L4/L7, Firewall, VPN
2. Application
3. Media(매체)
    * 유/무선
4. Protocol
    * 컴퓨터 네트워킹에서 가장 중요한 부분
    * 각각의 데이터를 전달되는 과정을 규칙으로 정해 놓은 것. 전 세계 표준이다.
    * HTTP, TCP, UDP, IP 등등

## 방식
1. Unicast, Multicast, Broadcast
    * 1:1, 1:N, 1:All
2. Simplex, Duplex
    * Simplex는 단방향, Duplex는 쌍방향
    * Simplex 무전기를 예로 들 수 있다.
3. Connection Oriented / Conectionless
    * session을 생성하는 과정을 거치고 데이터를 주고받는지 아닌지
    * 프로토콜 별로 특징을 가질 수 있다. 대표적으로 TCP / UDP
4. LAN / WAN
    * 보통 LAN은 건물
    * WAN은 LAN과 LAN을 연결 보통 사업자가 구성하고 사용자에게 임차함
    * 보통 회사의 경우 LAN은 회사가 관리하고 WAN의 회선은 ISP를 받아와서 사용
5. Point to Point, Multi-Access (direct)
6. Circuit Switching / Packet Switching (indirect)
    * A와 B가 통신할 때 A, B 사이의 Circuit이 점유된다 => Circuit Switching
    * 데이터를 중심으로 A, B 사이의 Circuit을 보냄, 점유하지 않음 => Packet Switching
7. Network Topology
    * Bus, Start, Ring, Hierarchical, Mesh, Hub&Spoke
    * 네트워크가 연결된 방식을 말함

## 주소
1. Data에 최종수신자의 Address를 표기하고, 나와 연결된 주변 Network Device가 받아 전달되는 방식임 (Hop by Hop)
2. 사용되는 주요 Address
    * IP Address (Data의 최종 수신자에 대한 정보로 사용됨)
    * Mac Address (최종 수신자로 전달하기 위해 나의 Next Hop에 보내기 위해 이용)
    * Domain Name (편의로 만든 알파벳 주소, IP Address로 변환됨)
3. 도로로 비유하자면 교차로에서 온 차를 열어보고 목적지를 확인해서 목적지로 보내거나 근처에 목적지가 없으면 목적지로 가기 위한 근처 교차로로 다시 보낸다.

## 품질
Infra로서의 특징 : 돈과의 Trade off  
Networking 구성요소가 매우 많으므로 100% 자산 소유가 불가함
1. Bandwidth
    * bps(bit per second)
2. Latency
    * RTT(Round Trip Time)
    * 패킷이 목적지에 도달하고 나서 해당 패킷에 대한 응답이 출발지로 다시 돌아오기까지의 시간. 즉, RTT는 패킷 왕복 시간입니다.
3. Jitter
    * Latency의 변동
4. Loss
    * 말 그대로 loss, 에러율
    * 유선상에선 거의 발생하지 않음, 인터넷망이나 무선에서는 발생 가능

## 망분류
1. Internet
2. Intranet
3. Extranet