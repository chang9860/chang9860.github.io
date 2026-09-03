---
title: "OS CH05 - CPU Scheduling"
date: 2026-03-12
categories: [Devlog]
tags: [os, study, ban-hyokyung-os, ch05]
permalink: /devlog/os-ch05-cpu_scheduling/
devlog_type: study-note
series: ban-hyokyung-os
series_order: 5
excerpt: "Chapter 5 summary: CPU and I/O Bursts in Program Execution, CPU-burst Time의 분포, CPU Scheduler & Dispatcher, Scheduling Algorithms, Scheduling Criteria, FCFS(First- Come First-Served), SJF(Shortest-Job-First), Example of Non-Preemptive SJF, Example of Preemptive SJF, 다음 CPU Burst Time의 예측, Exponential Averaging, Priority Scheduling, Round Robin(RR), Example: RR with Time Quantum = 20, Turmaround Time Varies With Time Quantum"
---

## 1. CPU Scheduler
:  Ready 상태의 프로세스 중에서 이번에 CPU를 줄 프로세스를 고른다.

## 2. Dispatcher
: CPU의 제어권을 CPU Scheduler가 선택한 프로세스에게 넘긴다.(문맥 교환)<br>  

CPU 스케줄링이 필요한 경우
1. Running -> Blocked(ex. I/O 요청하는 시스템 콜)
2. Running -> Ready(ex. timer interrupt)
3. Blocked -> Ready(ex. I/O 완료 후 인터럽트)
4. Terminated

1,4: nonpreemptive(자발적 반납)
나머지: preemptive(강제로 빼앗음)<br>

## 3. 스케줄링 성능 척도
- 시스템 입장
    * 이용률: cpu가 얼마나 쉬지않고 계속 일했는지
    * 처리량: cpu가 얼마나 많은 작업을 했는지
- 사용자 입장
    * 소요시간, 반환시간: 대기시간 + 실행시간
    * 대기 시간: cpu를 쓰기 위해 기다리는 순간 모두를 합한 시간
    * 응답 시간: 처음 cpu를 받기까지 기다린 시간

## 4. CPU 스케줄링 방법
* FCFS(First-come First-serve): 먼저 온 거 먼저<br>
단점: convoy effect (큰 작업이 먼저 오면 뒤에가 많이 기다려야 함.)

* SJF(Short Job Fisrt): 작업시간이 짧은 거 먼저.
    1. nonpreemptive: 작업이 진행되는 프로세스는 더 이상 빼앗기지 않는다.
    2. preemptive: 작업이 진행중이더라도 더 짧은 프로세스가 오면 빼앗긴다.(SRTF = Short Remaining Time First)<br>  

장점: 전체 기다리는 시간이 가장 짧아진다.  
단점: Starvation: 긴 작업은 계속 뒤로 밀린다.  
해결법: Age(노화): 오래 기다린 프로세스에게 우선권이 간다.

* RR(Round Robin): 현대의 방식으로 동일한 할당 시간을 순서대로 준다.(보통 10~100 millisecond) -> 응답 시간을 줄여준다.<br>
할당 시간이 너무 길면 FCFS처럼 되고 너무 작으면 context switch 오버헤드 발생

* Multilevel Queue: 여러 개의 큐로 된 층으로 나누어 층 간 우선 순위도 부여한다. 각 큐마다 독립적인 스케줄링을 가진다. 
![Multilevel_Queue](/assets/images/ban-hyokyung-os/multilevel_Queue.png)

* Multilevel Feedback Queue
![Multilevel_Feedback_Queue](/assets/images/ban-hyokyung-os/multilevel_feedback_queue.png)
층 간 이동도 가능하게 하여 아래층의 starvation을 없애도록 함.<br>
ex. 처음 들어온 프로세스는 맨 위 큐로 이동하고 한 칸씩 밑으로 내려간다. 이때 밑으로 갈 수록 할당되는 시간을 늘린다. 

## 5. 다양한 스케줄링 방법
* Multiple-Processor Scheduling(cpu 여러개)

* Real-Time Scheduling: 일정 기간 내에 반드시 끝나게 한다. 

* Threading Scheduling: Local Scheduling(사용자 수준의 thread, os는 모름), Global Scheduling(os가 하나하나 thread 조정)으로 나뉜다.

## 6. Algorithm Evaluation
* Queueing models: 확률 분포로 주어지는 arrival rate, service rate 등을 통해 각종 성능지표 계산한다.(자체 내장 알고리즘)

* Implementation(구현) & Measurement(성능 측정): 실제 시스템을 만들고 비교한다.

* Simulation(모의 실험): 알고리즘을 모의 프로그램으로 만들고 입력을 넣어 결과값 비교한다.
