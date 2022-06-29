---
layout: post
title: CS Study 05 - Thread & CPU scheduling
---

# Thread

Processor : Program을 실행하는 하드웨어 유닛, SW 측면에서는 데이터 포맷을 변환하는 역할을 한다.<br>
Process : 연속적으로 실행되고 있는 프로그램, 작업의 목록, scheduling의 대상<br>
Program : 하드 디스크 등에 저장되어 있는 코드와 리소스의 집합 파일.<br>
Thread : Process 의 단위

독립된 메모리 영역을 할당받는 Process는 1개 이상의 Thread를 가진다. 그 할당받은 자원을 사용하는 하나 하나의 실행의 단위가 Thread이다.

Thread는 독립된 Stack과 PC register를 가지지만 code, data, heap은 공유한다. -> Java의 method<br>
Process는 완전히 독립적이다. -> Java의 File

### Stack

- 함수 호출 시 전달되는 인자
- 리턴할 주소값
- 함수 내에 저장되는 변수

등등을 담는다. 독립적으로 함수를 호출하므로 각 Thread 마다 독립적인 공간을 갖는다.

### PC Register

CPU 레지스터의 한 종류로, 다음에 인출될 명령어의 주소를 가진다. Thread의 명령어가 어디까지 실행되었는지 저장한다고 보면 된다. CPU를 계속 사용하는 것이 아니라 할당 받은 후 스케줄러에 의해 다시 선점되므로 현재 실행 위치를 각 Thread 마다 저장해야 하기에 독립적인 공간을 갖는다.

## Multi-Tasking vs. Multi-Thread vs. Multi-Process

멀티 태스킹 : CPU 1개, Process 여러개<br>
멀티 쓰레드 : CPU 1개, Process 1개, Thread 여러개<br>
멀티 프로세스 : CPU 여러개, Program 1개, Process 여러개<br>

멀티 태스킹의 경우 여러 프로세스가 동시에 실행되는 것 처럼 보이나 실제로는 CPU 스케줄링에 의해 번갈아 실행되는 중이다.<br>
멀티 쓰레드의 경우 단일 프로세스를 여러 Threaad로 나누어 하나의 프로그램에서 여러가지 작업을 동시에 처리할 수 있다.<br>
멀티 프로세스의 경우 하나의 프로그램을 여러 Process로 나누어 각 Process가 하나씩의 작업을 처리한다. 프로세스 간의 공유는 IPC(Inter-Process Communication)으로 이루어진다.<br>

- Context Switching(문맥 교환) : 현재까지의 작업 상태를 저장하고 다음 작업에 필요한 데이터등을 읽어온다.

### Multi-Thread

Process 하나의 메모리 영역(code, data, heap)을 공유하므로 Thread 간 통신 비용이 적고 Context Switching도 빠르다. 그러나 공유에 대한 단점으로 하나의 Thread에만 문제가 발생해도 Process 전체에 영향을 끼치고, 동기화 문제가 발생한다. 이외에도 Process를 생성하여 자원을 할당하는 System-call이 줄어들어 자원을 효율적으로 관리할 수 있다.

### Multi-Process

여러 Process가 독립된 메모리를 사용하기 때문에 하나의 Process에 문제가 생겨도 다른 Process에는 영향을 주지 않는다. 대신 그만큼 Context Switching 발생 시 cache에 있는 모든 데이터를 리셋하고 다시 불러오기 때문에 많은 시간이 소요되며, IPC가 어렵다. Multi-thread에 비해 많은 메모리 공간/CPU 시간을 잡아먹는다.

## Scheduling

OS가 CPU의 자원을 어떤 Process에게 할당해 줄지 일정을 짜는 것.

### non-preemptive(비 선점형 방식) vs. preemptive(선점형 방식)

어떤 Process가 현재 실행중으로 CPU를 점유하고 있는 경우, 해당 Process가 끝날 때까지 다른 Process가 CPU를 사용하지 못하면 `비 선점형`, 다른 Process가 중간에 기존의 Process를 중지키시고 CPU를 점유할 수 있으면 `선점형` 방식으로 나뉜다.
비 선점형의 경우 순차적으로 처리하므로 Context Switching이 적지만 긴급하게 처리되어야 할 Process가 빠르게 처리되지 못할 수 있다. 이에 반해 선점형 방식은 언제든 필요에 따라 급하게 처리해야 할 Process 처리가 가능하지만 그만큼 Context Switching이 자주 발생할 수 있다.
현대 운영체제는 선점형 방식을 채택한다.

비 선점형 방식 : FCFS(First Come First Service), SJF(Shortest Job First), Priority(비 선점형)<br>
선점형 방식 : Round Robin, SRT(Shortest Remaining Time), 다단계 Queue, Priority(선점형)

### 비 선점형 방식

#### First Come First Service

먼저 온 것을 먼저 처리한다.

Ready Queue가 존재하고, 도착한 순서대로 CPU에 할당한다. 순서대로 실행되므로 작업 완료 시간을 예측하기 쉽지만, 길게 실행되는 Process가 있다면 그 뒤에 오는 Process들은 모두 오래 기다리게 될 수 있다(convey effect).

#### Shortest Job First

실행시간이 짧으면 먼저 CPU에 할당한다.

평균 대기시간이 가장 짧지만, 실행 시간이 긴 Process는 계속 뒤로 밀려나는 '기아(Starvation)' 현상이 발생한다. 작업 완료 시간을 예측할 수 없기 때문에, 과거에 실행했던 시간을 바탕으로 추측한다.

#### Priority

각 Process에게 우선순위를 매겨 차례대로 처리한다.

SJF에서의 Starvation 해결법 : 대기 시간이 길어지면 우선 순위를 높인다.<br>
이 외에도 제한 시간, 기억 장소 요청량, 사용 파일 수, 프로세스의 중요성 등 다양한 요인에 의해 우선순위가 결정된다.<br>
우선순위가 높으면 Ready Queue의 head에 들어가게 된다. 이 때 기존의 Process를 끝내고 다음 Process가 실행되면 비 선점형 Priority, 기존의 Process를 중지하고 새로 들어온 Process가 CPU를 선점하면 선점형 Priority로 구분된다.

### 선점형 방식

#### Round Robin

FCFS + Time Quantum

Time Quantum : Process 마다 CPU 사용 시간에 제한을 둔다. 제한 시간이 끝나면 해당 Process는 Ready Queue의 가장 뒤로 밀린다.<br>
Time Quantum 이 너무 작으면 Context Switching이 자주 일어나고, 너무 크면 프로세스가 대부분 거의 다 실행되기에 FCFS와 다른게 없다.

#### Shortest Remaining Time

SJF의 선점형 버젼.

현재 CPU를 점유중인 Process의 남은 처리 시간보다 짧은 Process가 들어오면 그 Process가 CPU를 점유한다.<br>
평균 대기시간이 짧지만, 종료 시간이 예측하기 어렵고 기아 현상을 전혀 해결하지 못한다.

#### 다단계 Queue

우선순위를 가지는 Ready Queue 여러개를 사용한다.

각 Ready Queue 마다 우선순위가 있고, 해당 우선 순위는 운영체제로 부터 부여받는다. 각 Ready Queue의 스케줄링 알고리즘이 같을 필요는 없다. 대신 높은 우선순위를 가진 Ready Queue의 작업이 모두 끝나야지만 낮은 우선순위를 가진 Ready Queue의 작업이 시작된다.<br>
우선 순위에 따라 각각 다양한 스케줄링이 가능하지만 Queue 마다 Process 이동이 되지 않으므로 유연성은 떨어진다.
