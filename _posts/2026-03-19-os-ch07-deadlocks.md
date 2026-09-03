---
title: "OS CH07 - Deadlocks"
date: 2026-03-20
categories: [Devlog]
tags: [os, study, ban-hyokyung-os, ch07]
excerpt: "Chapter 7 summary: 교착상태(deadlock), The Deadlock Problem, Deadlock 발생의 4가지 조건, Resource-Allocation Graph(자원할당그래프), Deadlock Prevention, Deadlock의 처리 방법, Deadlock Avoidance, Resource Allocation Graph algorithm, Banker's Algorithm, Example of Banker's Algorithm, Deadlock Detection and Recovery, Deadlock Ignorance"
---

## 1. Deadlock(교착상태)
: 프로세스들이 서로 가진 자원을 기다리며 block된 상태

## 2. Deadlock 발생의 4가지 조건
1. Mutual exclusion: 자원 하나에 하나으 프로세스만 사용 가능
2. No preeption: 강제로 자원을 빼앗기지 않음
3. Hold and Wait: 다른 자원을 기다릴 때 기존 자원을 보유한 채 대기
4. Circular wait: 자원을 기다리는 프로세스 간 사이클이 형성되어야 함

## 3. 자원할당 그래프
![자원할당_그래프](/assets\images\ban-hyokyung-os\Graph.png)
사이클이 없다면: deadlock 아님  
사이클이 있다면: 자원당 instance가 하나면 deadlock이고 여러 개면 deadlock 가능성 있음(자원의 instance들이 모두 사이클에 관여하고 있으면 deadlock)

## 4. Deadlock의 처리 방법
1. **Deadlock Prevention**  
자원 할당 시 Deadlock 발생의 4가지 조건 중 한가지를 만족되지 않게 하는 법
* Mutual Exclusion: 항상 성립해야함.
* Hold and Wait: 프로세스가 자원을 요청할 때 다른 자원을 가지고 있지 않는다.(방법1: 프로세스 시작 시 필요한 모든 자원을 할당하는 법, 방법2: 자원 요청 시 기존 자원 모두 내려놓고 요청) 
* No Preemption: 모든 필요한 자원을 얻을 수 있는 경우에만 프로세스 시작됨.
* Circular Wait: 모든 자원 유형에 할당 순서를 정한다. -> 1을 얻어야 2,3을 순서대로 얻을 수 있음.   
  
문제점: starvation 문제 등 효율적이지 못함.

2. **Deadlock Avoidance**   
자원 할당 시 Deadlock 형성 가능성이 없는 경우에만 할당

3. **Deadlock Detection and recovery**
Deadlock 탐지 및 발생 시 제거하는 방법
4. **Deadlock Ignorance**  
Deadlock 발생에 신경 안 쓰고 발생 시 사용자가 직접 프로세스 종료.