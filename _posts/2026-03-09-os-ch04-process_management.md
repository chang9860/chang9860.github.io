---
title: "OS CH04 - Process Management"
date: 2026-03-09
categories: [Devlog]
tags: [os, study, ban-hyokyung-os, ch04]
excerpt: "Chapter 4 summary: 프로세스 생성(Process Creation), 프로세스와 관련한 시스템콜, 프로세스 간 협력, Message Passing, Interprocess communication, CPU and I/O Bursts in Program Execution, CPU-burst Time의 분포, 프로세스의 특성 분류"
---

## 1. 프로세스 생성
COW(Copy-on-write)  

부모 프로세스가 자식 프로세스 생성<br>
자식은 부모와 자원을 공유하거나 운영체제로부터 받는다.<br>
  
프로세스의 트리(계층 구조) 형성  

자원의 공유
* 부모와 자식이 모든 자원 공유
* 일부 공유
* 공유 X
  
수행
* 부모와 자식이 공존하며 수행되는 모델
* 자식이 종료될 때까지 부모는 wait하는 모델

주소공간
* 자식은 부모의 공간을 복사함
* 자식은 그 공간에 새로운 프로그램을 올림<br>
ex. fork 시스템 콜(그대로 복사), exec 시스템 콜(완전히 새로운 프로그램)

## 2. 프로세스 종료
exit: 운영체제에게 끝났다고 알려줌
* 자식이 부모에게 끝났다는 메시지 보냄(wait을 위해) --> 자발적 종료
* 프로세스의 각종 자원들이 운영체제에게 반납됨  

abort: 부모 프로세스가 자식의 수행을 종료시킴 --> 비자발적 종료
* 자식이 할당 자원의 한계치를 넘어섬
* 자식에게 할당된 태스크가 더 이상 필요하지 않음
* 부모가 종료하는 경우<br>
    + 운영체제는 부모가 종료하는 경우 자식의 수행을 막는다.
    + 단계적인 종료(자식 노드를 죽이는 경우 그 밑에도 다 죽인다.)

## 3. 프로세스 간 협력
독립적 프로세스(원칙): 하나의 프로세스는 다른 프로세스에 간섭하지 못한다.  
  
협력 프로세스: 하나의 프로세스가 다른 프로세스의 수행에 영향력 가능  
  
프로세스 간 협력 메커니즘
* message passing: 커널을 통해 메시지 전달<br>
    + Direct communication: 협력하려는 프로세스의 이름 명시
    + Indirect communication: mailbox(또는 port)를 통해 간접 전달
* shared memory: 다른 프로세스와 일부 주소 공간 공유(처음은 운영체제의 허락이 있어야 가능.)

## 4. CPU, I/O Burst in program Execution
![CPU_Burst](/assets\images\ban-hyokyung-os\CPU_Busrt.png)
CPU가 일하는 중간 중간 I/O Burst 발생
I/O bound job: I/O 작업이 많이 발생하는 일(cpu bound job보다 자주 발생함)
CPU bound job: I/O 인터럽트 방해 거의 없이 CPU 작업(계산)이 많은 일 
