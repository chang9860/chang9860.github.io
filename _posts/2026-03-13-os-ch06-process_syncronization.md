---
title: "OS CH06 - Process Syncronization"
date: 2026-03-13
categories: [Devlog]
tags: [os, study, ban-hyokyung-os, ch06]
excerpt: "Chapter 6 summary: 데이터의 접근, Race Condition, OS에서의 race condition(3/3), Example of a Race Condition, The Critical-Section Problem, OS에서 race condition(1/3), If you preempt CPU while in kernel mode…, Initial Attempts to Solve Problem, 프로그램적 해결법의 충족조건, Algorithm 1, Algorithm2, Algorithm3(Peterson's Algorithm), Synchronization Hardware, Semaphores 등등"
---

## 1. Race condition
: 공유 데이터에 대해 동시 접근하는 상황<br>
-> 데이터 불일치 문제 발생<br>
ex.
1. kernel 수행 중 인터럽트 발생 시-> 커널 수행 중 인터럽트 발생하지 못하게 한다.
2. 프로세스가 시스템 콜을 하여 커널 수행 중인데 context switch가 일어나는 경우 -> 커널 수행 중에 문맥교환 일어나지 못하게 한다.
3. 여러 cpu가 공유된 메모리에 접근하는 경우 -> 하나가 접근하면 그 데이터를 lock해 다른 cpu가 접근 못하도록 한다. -> critical section problem 발생(접근 통제로 다른 cpu가 일을 하지 못해 자원이 낭비된다.)

## 2. critical problem 문제 해결방법
만족해야할 조건
1. Mutual Exclution: critical section에 오직 하나만 들어가야 한다.
2. Progress: critical section이 비어 있을 때 누군가 요청하면 들어갈 수 있어야 한다.
3. Bounded Waiting: 프로세스가 들어가고 싶다고 요청한 후부터 요청이 수학될 때까지 다른 프로세스가 critical section에 들어가는 횟수가 제한되어야 한다.

Algorithm 1
![Algorithm_1](/assets\images\ban-hyokyung-os\Algorithm1.png)
문제점: 두 프로세스의 진입하려는 시도 횟수가 차이가 날 때 turn을 바꾸지 못하는 문제가 있다.
(Progress 불만족)

Algorithm 2
![Algorithm_2](/assets\images\ban-hyokyung-os\Algorithm2.png)
문제점: 둘 다 2행까지 수행하게 된다면 서로 무한 양보하게 된다.(Progress 불만족)

Algorithm 3(Peterson's Algorithm)
![Algorithm_3](/assets\images\ban-hyokyung-os\Algorithm3.png)
모두 만족하지만 Busy Waiting(=spin lock) 문제가 있음.(계속 CPU와 memory를 쓰면서 대기)

하드웨어적 해결:
test&modify를 atomic하게 한번에 수행할 수 있도록 지원한다면 문제 해결   

## 3. Semaphores
: 2번의 해결법들을 추상화시킴(공유 자원에 동시에 접근할 수 있는 "허용 개수"를 관리하는 변수) 
1. P(S): cpu를 얻거나 대기하는 기능
2. V(S): cpu 반환하는 기능  
기존의 경우 busy-wait 발생

해결방법: Block&Wake up  
block: 프로세스를 wait 큐에 넣는다.
wake up: 프로세스를 ready 큐에 넣는다.   
![semaphore](/assets\images\ban-hyokyung-os\semaphore.png) 
V(S)에서는 <= 0 인 이유: P(S)에서 1을 빼고 시작하기 때문이다.

Two type of Semaphores
1. Counting semaphore: 도메인이 0이상인 정수값이다. 주로 resource counting에 사용(여러 개 접근 가능)
2. Binary semaphore: 0 또는 1 값만 가질 수 있다. 주로 mutual exclusion (lock/unlock)에 사용 (단 하나만 접근 가능) 

## 4. Deadlock and Starvation
Deadlock: 둘 이상의 프로세스가 서로 상대방에 의해 충족되는 event를 무한히 기다리는 현상  
ex. 프로세스 A와 프로세스 B가 P0과 P1 둘 모두를 가지고 작업해야한다고 했을 때 -> 프로세스 A가 P0을 가지고 프로세스 B가 P1을 각각 가지게 되면 서로 무한히 기다리데 된다.  
  
Starvation: 프로세스가 세마포어 ready 큐에서 계속 뒤로 밀려 선택 못 받는 현상

## 5. Classical Problems of Synchronization
1. Bounded-Buffer Problem(Producer-Consumer Problem)
![bounded-buffer-problem](/assets\images\ban-hyokyung-os\bounded-buffer.png)
공유된 buffer에 동시 접근, 또는 buffer가 가득찼는데 더 넣거나 없는데 꺼내려 하는 문제 발생. 생산자와 소비자 모두 행위를 할 때 mutex = 1를 이용하여 lock,unlock을 한다.
2. Readers and Writers Problem
![Readers-writers-problem](/assets\images\ban-hyokyung-os\readers-writers-problem.png)
Reader는 여러명 가능, 문제점: writer가 기다리고 있을 때 reader가 계속 들어오면 starvation 발생 가능.(해결법: 일정 시간이 지나면 writer에게 넘겨지도록)
3. Dining-Philosophers Problem
![philosophers-problem](/assets\images\ban-hyokyung-os\philosophers-problem.png)
젓가락 집기 전 test로 먹을 수 있는 상태인지 확인하고 아니면 대기한다. 자신이 먹는게 끝났다면 이웃에게도 기회를 준다.

## 6. Monitor
모니터 내의 여러 프로세스 중에서 한번에 1개만 실행 가능하다. --> 프로그래머가 동기화 제약 코드 작성 불필요  
condition variable 사용(wait, signal)  
ex. buffer 문제 적용
![monitor-buffer](/assets\images\ban-hyokyung-os\monitor-buffer.png)