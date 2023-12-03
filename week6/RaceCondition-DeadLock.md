# 레이스 컨디션 Race Condition

- 멀티쓰레드 또는 멀티 프로세스 환경에서 공유자원에 동시에 접근할 때, 의도치 않은 결과를 낳는 것. 이를 방지하기 위해서는 공유자원에 대한 동기화가 필요하다.

하지만 이 동기화로 인해 교착 상태가 발생할 수 있다는 문제가 있다.

# 교착 상태(Deadlock)

- 다수의 스레드 또는 프로세스가 서로 깨워주기를 기다리면서, 모두 대기하고 있는 상태

- deadlock state : 프로세스가 발생 가능성이 없는 이벤트를 기다릴 때, 시스템 내에 데드락에 빠진 프로세스 가 있는 경우
- **데드락 vs 기아 상태**
  - 데드락 : 가능성 제로인 자원/이벤트 기다릴 때
  - 기아상태 : 운이 없어서 계속 기다리는 상태
- **자원의 분류**에는 하드웨어 vs 소프트웨어로 나누는 기준 외에도 다양한 기준으로 분류할 수 있는데, 데드락을 이해하기 위해서는 선점 가능 여부와 재사용 여부를 기준으로 자원을 분류해볼 수 있다.

  - **선점 가능 여부** - preemptible : 누군가 CPU, 자원을 뺏어갈 수 있다. - non-preemptible : 선점 당하면 데이터가 날라가는 중요한 문제가 발생.
    => 데드락은 Non-preemptable 한 자원에 대해서 발생한다.

  - **재사용 가능 여부에 따른 분류** : 두 종류의 자원 모두 non-preemptable 하기 때문에 데드락이 발생 가능하다.
    - SR(serially-reusable Resources) : 시스템 내 항상 존재, 사용 끝나면 다른 프로세스가 사용 가능
      - 프로세서, 디스크, 프로그램, 메모리 등
    - CR(Consumable Resources)
      - 한 프로세스 사용 후 사라지는 자원
      - interrupts, signals, messages, IO buffers, etc.

## Deadlock 해결 방법

**1. 데드락 예방 Deadlock Prevention **

- 필수 요건을 전부 충족하는 상태가 되지 않도록 만든다.

**2. 데드락 회피 Deadlock Avoidence**

- 자원 요청이 있을 때, 데드락 발생 가능하면 거절, 그렇지 않으면 할당하는 방법
- 시스템의 모든 자원을 파악해야하고, 프로세스가 어떤 자원을 얼만큼 필요로하는지 미리 파악해야한다.

**3. 데드락 탐지 & 복구 Deadlock Detection & Recovery**

- deadlock 이 발생했는지를 주기적으로 확인. 발생한 경우 자원을 회수/프로세스 종료 등 조치를 취한다.
- 교착상태는 매우 드물게 발생하기 때문에 overhead 가 크다.

**4. Ignore**

- 교착 상태는 매우 드물게 발생하기 때문에 그냥 데드락 무시하는 게 오히려 효율적일수도..!

### **데드락 발생 필요 요건 4가지** (전부 만족해야만 교착 상태 발생)

1. **자원의 특성**
   1. exclusive use of resources(공유자원의 상호 배제)
   2. Non-preemptible resources
2. **프로세스의 특성**
   1. Hold and wait(Partial allocation)
      - 프로세스가 한 자원을 잡고 있으면서 다른 자원을 요청
   2. Circular wait(순환 대기)

### 1. 데드락 예방 Deadlock prevention

- 데드락 필요 요건 4개 중 하나만 없애도 예방 가능
- exclusive use of resources ⇒ 모든 자원 공유 허용 ⇒ 현실적으로 불가능
- Non-preemptible resources ⇒ 다 쓸 때까지 반납 안 한다는 특성인데 내가 선점하고 있어도 쓸 수 있게 한다는 게 현실적으로 거의 불가능하다. 자원 모두 반납하고 작업 취소하는 방법도 있긴 하지만 낭비가 발생하고 비현실적이다.
- Hold and wait(Partial allocation) ⇒ Hold and wait 조건 제거. 내 일이 다 끝낼 때까지 절대 못 한다. 하지만 이런 방식은 자원 낭비가 발생하고 무한 대기 현상 발생 가능하다.
- Circular wait ⇒ 서로 물고 물리는 관계를 만들지 말자.
  - 자원 순서 번호 부여.
  - 프로세스는 순서 증가 방향으로만 지원 요청 가능
  - 자원 낭비 발생(내가 쓸 수 있는 자원이 있는데도 요청 불가)

### 2. 데드락 회피 Deadlock Avoidence

- 지켜보다가 발생할 것 같으면 예방하자
- 시스템을 항상 safe state로 유지(안전한 상태로). safe sequence 존재하는지 확인(데드락 상태가 되지 않을 수 있는 상태가 있음을 보장)
  - safe state: 모든 프로세스가 정상 종료 가능한 상태
  - unsafe state
    - 반드시는 아니고 데드락 상태일 가능성이 있다.
- **가정**
  - 프로세스 수 고정
  - 자원 종류&수 고정
  - 프로세스가 요구하는 자원, 최대 수량 알고 있다
  - 프로세스는 자원 사용 후 꼭 반납해야 한다.
  ⇒ 실용적이진 않다.
- 장점 : 데드락 발생 막을 수 있음
- 단점
  - High overhead : 항상 시스템 감시해야 하므로.
  - Low resource utilization : safe state를 유지하기 위해 실제로 사용하지 않는 자원 발생
  - 즉 실용적이지 않다.

### 3. 데드락 탐지 & 복구 Deadlock Detection & Recovery

#### 데드락 탐지 Deadlock detection

- **Resource Allocation Graph(RAG)** - 그래프 모델 확장해서 이용
  => 그래프 이용해서 데드락 발생 여부 탐지

## 데드락 복구 Deadlock recovery

1. **process termination**
   - 데드락 상태에 있는 프로세스 중 일부 종료
   - 여러 애들 중 누구를 종료시킬지 결정하는 게 termination cost model
     - **Lowest-termination cost process first**
       - 종료 비용이 가장 적은 걸 종료
         - low overhead, simple
         - 불필요한 프로세스 종료 가능성 높음
     - **Minimum cost recovery**
       - 최소 비용 찾기
       - 복잡, high overhead
   - 강제 종료된 프로세스를 이후 재시작
2. **resource preemption**

   - 데드락 해결 위해 선점할 자원 선택 (누구를 뺏어올까)
   - 선정된 자원 가지고 있는 프로세스에서 자원 뺏음
   - 자원 뺏긴 프로세스는 강제 종료 → 데드락 아닌 프로세스가 종료될 수 있다
   - 누구 꺼 뻇어올지 정하기 위한 preemption cost model이 필요하다.

3. **Checkpoint-restart method**

- 프로세스 수행 중 체크포인트마다 context 저장
- 급종료되면 rollback(강제 종료 후 재시작)할 수 있도록

---

### References

[운영체제 강의](https://www.youtube.com/watch?v=EdTtGv9w2sA&list=PLBrGAFAIyf5rby7QylRc6JxU5lzQ9c4tN) 보고 정리했던 필기
[[전공생이 설명하는 OS] 동기화 - (5) Deadlock
출처: https://letsmakemyselfprogrammer.tistory.com/113 [척척석사:티스토리]](https://letsmakemyselfprogrammer.tistory.com/113)
