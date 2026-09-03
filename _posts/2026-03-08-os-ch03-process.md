---
title: "OS CH03 - Process"
date: 2026-03-08
categories: [Devlog]
tags: [os, study, ban-hyokyung-os, ch03]
permalink: /devlog/os-ch03-process/
devlog_type: study-note
series: ban-hyokyung-os
series_order: 3
excerpt: "Chapter 3 summary: 프로세스의 개념, 프로세스의 상태(Process State), 프로세스의 개념, 프로세스 상태도, Process Control Block(PCB), 문맥교환(Context Switch), 프로세스를 스케줄링하기 위한 큐, Ready Queue와 다양한 Device Queue, 스케줄러(Scheduler), 프로세스 스케줄링 큐의 모습, Thread, Single and Multithreaded Processes, Benefits of Threads, Implemetation of Threads"
---

## 1. 프로세스의 개념
![process_concept](/assets/images/ban-hyokyung-os/process_concept.png)<br>
: 프로세스는 프로그램의 실행이다.<br>
프로세스의 문맥  
* cpu 상태를 나타내는 하드웨어 문맥<br> program counter(PC), 각종 register
* 프로세스의 주소 공간<br> 
code, data, stack
* 프로세스 관련 커널 자료 구조<br>
PCB, kernel stack 

## 2. 프로세스의 상태
![process_state](/assets/images/ban-hyokyung-os/process_state.png)
* Running: cpu를 잡고 instruction 실행중인 상태
* Ready: cpu 받기를 기다리는 상태
* Blocked: cpu 받아도 instruction 실행 못하는 상태 ex. I/O 요청을 하고 기다리는 상태 --> 자신이 요청한 event가 완료되면 다시 Ready.
* New: 프로세스가 생성중인 상태
* Terminated: 수행이 끝난 상태
* Suspected: 외부적인 이유로 프로세스의 수행이 정지된 상태(메모리에 올라가있던 프로세스가 메모리를 빼앗기고 디스크에 swap out 된다.) --> 외부에서 허락해줘야 다시 active. 

## 3. 프로세스의 문맥 교환(context switch)
: cpu를 한 프로세스에서 다른 프로세스로 넘겨주는 일(기존의 프로세스 상태를 그 프로세스의 pcb에 저장하고 다른 프로세스의 pcb를 읽어온다.)

PCB 구조도
![PCB](/assets/images/ban-hyokyung-os/PCB.png)

주의: System call이나 interrupt가 발생시 반드시 context switch가 일어나는 것은 아님
-> 사용자 프로그램이 interrupt or system call을 한 뒤 커널 모드에서 그에 맞는 함수 실행 뒤 context switch 없이 기존 사용자 프로그램 복귀

## 4. 프로세스를 스케줄링하기 위한 큐
* Job queue: 현재 시스템 내에 있는 모든 프로세스의 집합
* Ready queue: 현재 메모리 내에 있으면서 cpu를 잡아 실행되기 기다리는 프로세스의 집합
* Device queues: I/O devices의 처리를 기다리는 프로세스의 집합

## 5. 스케줄러
* Long-term schedular(장기 스케줄러)<br>
시작 프로세스 중 어떤 것들을 ready queue로 보내질 결정<br>
degree of Multiprogramming을 제어<br>
time sharing system에는 보통 장기 스케줄러가 없음(무조건 ready.)
* Short-term schedular(단기 스케줄러)<br>
어떤 프로세스를 다음번에 running시킬지 결정<br>
프로세스에 cpu를 주는 문제이고 충분히 빨라야 함(millisecond 단위)
* Medium-term schedular(중기 스케줄러)<br>
여유 공간 마련을 위해 프로세스를 통째로 메모리에서 디스크로 쫒아냄<br>
degree of Multiprogramming을 제어<br>
**최근 트렌드!**

## 6. Thread
![thread](/assets/images/ban-hyokyung-os/thread.png)<br>

Thread의 구성
- program counter
- register set
- stack space

Thread가 동료 Thread와 공유하는 부분
- code section
- data section
- OS resources

Thread의 장점
- 응답성: 하나의 쓰레드가 interrupt하여 대기할 때 다른 쓰레드가 일을 처리한다.
- 자원 공유: 프로세스의 일부분을 공유한다.
- 경제성: creating & CPU switching thread하는데 process일때보다 30배, 5배 정도 차이난다.
- 멀티코어 멀티 쓰레드: 병렬 수행 가능

Thread 실행 위치
: kernel에서, library에서 실행 가능
