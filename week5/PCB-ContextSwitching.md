# 1. PCB(Process Control Block)

> 프로세스 정보를 저장하는 자료 구조
> 프로세스 메타데이터들을 저장해 놓는 곳으로, 한 PCB 안에는 한 프로세스의 정보가 담긴다.

#### Process Metadata

- CPU에서 스케줄링으로 프로세스를 관리할 때, 각 프로세스에 대한 특징인 메타데이터를 저장한다. 프로세스가 생성(initialized or installed)되면 이 메타데이터들이 저장되는 곳이 바로 PCB이다.
- 한 PCB에는 한 프로세스에 대한 메타데이터가 저장된다.

- Process ID
- Process State
  (i.e. new, ready, running, waiting or terminated)
- Process Priority
- CPU Registers
- Owner
- CPU Usage
- Memeory Usage

![](https://velog.velcdn.com/images/urjimyu/post/7be095b0-bdb5-46ed-83b1-7ddd692a7335/image.png)

그리고 이렇게 PCB에 저장된 프로세스 정보는 `Context Switching`에서 중요한 역할을 한다.

# 2. Context Switching

> 프로세스 또는 스레드의 상태를 저장하여 나중에 복원하거나 실행을 재개할 수 있도록 하는 과정
> 쉽게 말해 다른 task로 교체하기 위해 현재 task 상태 정보를 저장한 후에 다음에 실행할 task 상태 정보를 읽어오는 것을 말한다.

- 컴퓨터가 여러 태스크(Process, Thread)를 번갈아 수행 가능하도록 한다.

#### Context Switching이 발생하는 경우

1. 멀티태스킹 Multitasking
2. 인터럽트 Interrupt handling
3. 유저/커널 모드 전환 User and kernel mode switching

#### Context Switching 과정

1. 현재 실행 중인 프로세스 상태 정보 PCB에 저장
2. 다음 순서로 실행할 프로세스 정보를 PCB에서 복원해서 업데이트
3. 실행 중인 프로세스 교체

---

### References

[Wikipedia - Context Switch](https://en.wikipedia.org/wiki/Context_switch)
[Context Switching이란?](https://nesoy.github.io/articles/2018-11/Context-Switching)
[PCB와 Context Switching](https://gyoogle.dev/blog/computer-science/operating-system/PCB%20&%20Context%20Switching.html)
[PCB와 컨텍스트 스위칭(Context Switching)](https://jerryjerryjerry.tistory.com/181#google_vignette)
