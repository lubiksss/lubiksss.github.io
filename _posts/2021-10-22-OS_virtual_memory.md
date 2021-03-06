---
last_modified_at : 2021-10-22
layout : single
title:  "OS 가상메모리"
categories: OS
tags : [virtual memory]

toc: true
toc_sticky: true
---
## 서론
### 참조
<a target = '_blank' href='https://vmilsh.tistory.com/384'>운영체제 가상메모리 (Virtual Memory)란?</a>  
<a target = '_blank' href='https://libertegrace.tistory.com/entry/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B0%80%EC%83%81-%EB%A9%94%EB%AA%A8%EB%A6%AC%EC%9D%98-%EC%9D%B4%ED%95%B4'>[운영체제] 가상 메모리의 이해</a>

## 가상메모리란?
> 메모리로서 실제 존재하지는 않지만, 사용자에게 있어 메모리로서 역할을 하는 메모리. 다시 말해 프로그램이 수용될 때는 가상메모리의 크기에 맞춰 수용되는 것이다. 그러나 가상메모리에 수용된 프로그램이 실행될 때는 실제 물리 메모리가 필요하게 된다.

> 가상메모리 안에 프로그램이 실행될 때는 실제 메모리에 머물러 있어야 한다. 그러나 프로그램 실행 시 반드시 프로그램 전체가 실제 메모리에 있을 필요는 없다. 현재 실행되어야 하는 부분만이 실제 메모리에 옮겨져 있으면 되는 것이므로 실제 메모리용량보다 큰 프로그램이 가상메모리의 등장으로 실행 가능하다.

## 페이징
가상메모리와 실제 메모리를 매핑 해주는 방법. 현재 가장 주목받고 있는 방법이다.
페이징 방식에서는 가상메모리상의 주소공간을 일정한 크기의 페이지로 분할하게 되는데 실제 메모리 또한 가상메모리와 같은 크기의 페이지로 분할하게 된다. 페이지는 1,2, 4KB 등으로 시스템에 따라 다르지만 보통 4KB를 사용한다. 페이지 크기는 단편화를 고려해 작을수록 좋겠지만 무조건 작은 것 역시 문제가 있으니 적절한 크기를 사용하면 된다.

## 페이지 테이블
가상메모리의 페이지 넘버와 실제 메모리의 페이지 프레임을 하나의 순서쌍으로 저장하고 있는 테이블이다. 이 테이블을 사용하여 프로그램에서 사용되는 가상주소를 실제 메모리 주소로 변환되게 된다.

## 페이지 적재 청잭
1. 디맨딩 페이징  
paging system을 사용하면 프로세스에서 나눠진 page를 언제 물리 메모리에 올려놓을지에 대한 정책이 필요하다. 선행 페이징으로 하면 그냥 프로세스를 시작하자마자 page를 먼저 다 올려두는 것인데 이것 보다 실제로 필요할 때 page를 올리는 것이 좋을 것이다. 이게 demand paging이다.

## 페이지 교체 정책
1. FIFO  
가장 먼저 들어온 페이지를 내린다.
2. OPT(OPTimal) 알고리즘  
앞으로 가장 오랫동안 사용하지 않을 페이지를 내린다. => 그러나 미래에 어떤 페이지를 얼마나 사용할 것인지는 알 수 없으므로 일반 OS에서는 구현이불가능하다.
3. LRU(Leaset Recently Used) 알고리즘  
가장 오래전에 사용된 페이지를 내리자.
4. LFU(Leaset Frequently Used) 알고리즘  
가장 적게 사용된 페이지를 내리자.
