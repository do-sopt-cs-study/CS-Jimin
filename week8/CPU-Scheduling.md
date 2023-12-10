# CPU 스케줄링

- 운영체제는 CPU를 프로세스 간에 교환해서 생산성을 높인다.
- 다중 프로그래밍의 목적은 CPU 이용률을 최대화하는 것이다. 따라서 프로세스가 대기해야 할 경우, 운영체제는 CPU를 그 프로세스로부터 회수해 다른 프로세스에 할당한다.

### CPU - I/O 버스트 사이클 (CPU - I/O Burst Cycle)

- 프로세스 실행은 CPU 실행과 I/O 대기의 사이클로 구성된다.
  CPU Burst로 시작된다. 뒤이어 I/O Burst가 발생하고, 그 뒤를 이어 또 다른 CPU Burst가 발생하며, 이어 또 다른 I/O Burst 등등으로 진행된다. 결국 아래의 그림처럼 마지막 CPU Burst는 실행을 종료하기 위한 시스템 요청과 함께 끝난다.
  ![](https://velog.velcdn.com/images/urjimyu/post/ea602683-6562-41bb-b266-cfa9c4299f85/image.png)

### CPU 스케줄러(CPU Scheduler)

CPU가 유휴 상태가 되면 OS는 레디 큐에 있는 프로세스 중 선택해서 실행하는데, 이때 선택 절차를 CPU 스케줄러로 수행한다. 스케줄러는 실행 준비가 된 메모리 내 프로세스 중에 선택해서 할당해준다. 일반적으로 레디 큐에 있는 레코드들은 프로세스의 프로세스 제어 블록(PCB)들이다.

### 선점 및 비선점 스케줄링 (Preemptive and Nonpreemptive Scheduling)

CPU 스케줄링 결정이 발생하는 네 가지 상황은 아래와 같다.

- 한 프로세스가 실행 상태에서 대기 상태로 전환될 때 (I/O 발생)
- 프로세스가 실행 상태에서 준비 완료 상태로 전환될 때 (인터럽트 발생)
- 프로세스가 대기 상태에서 준비 완료 상태로 전환될 때 (I/O 종료)
- 프로세스가 종료할 때

### 스케줄링 알고리즘 (Scheduling Algorithms)

#### 선입 선처리 알고리즘 (First Come First Served Scheduling, FCFS)

- CPU를 먼저 요청하는 프로세스가 CPU를 먼저 할당받는다.

#### 최단 작업 우선 스케줄링 (Shortest Job First Schduling)

- CPU 버스트 길이가 가장 작은 프로세스부터 순서적으로 CPU 코어를 할당한다.

#### 라운드 로빈 스케줄링 (Round Robin Scheduling, RR)

- 선입 선처리 스케줄링과 유사하지만 시스템이 프로세스들 사이를 옮겨 다닐 수 있도록 선점이 추가된 방식.
- 시간 할당량(time quantum)/타임슬라이스(time slice)라고 하는 작은 단위의 시간을 정의해서 CPU 스케줄러가 준비 큐를 돌면서 한 번에 한 프로세스에 한 번의 시간 할당량 동안 CPU를 할당한다.

#### 우선순위 스케줄링 (Priority Scheduling)

- 가장 높은 우선순위를 가진 프로세스에 할당. 우선순위가 같으면 보통 FCFS 순서로 스케줄.

#### 다단계 큐 스케줄링 (Multilevel Queue Scheduling)

- 우선순위 스케줄링 + 라운드 로빈
- 우선순위가 각 프로세스에 정적으로 할당된다.
- 프로세스는 실행시간 동안 동일한 큐에 남아 있다.
- 일반적으로 프로세스들이 시스템 진입 시에 영구적으로 하나의 큐에 할당된다.

#### 다단계 피드백 큐 스케줄링 (Multilevel Feedback Queue Scheduling)

- 프로세스가 큐 간 이동하는 것을 허용
- Aging, Starvation 예방

---

### References

[[Operating System - Chapter 5] CPU 스케줄링](<https://imbf.github.io/computer-science(cs)/2020/10/18/CPU-Scheduling.html>)
