# 운영체제란?

![](https://velog.velcdn.com/images/urjimyu/post/ef15f313-4f49-404c-99ab-702b86ab1839/image.png)

- 컴퓨터 자원을 관리하는 주체
- 컴퓨터 자원들을 효율적으로 관리해서 사용자에게 서비스를 제공하는 소프트웨어

- 넓은 의미의 운영체제 : 시스템 소프트웨어 전반
- 좁은 의미의 운영체제 : 제어 프로그램(kernel)

> 커널 - 알맹이라는 의미

- 핵, 관리자 프로그램, 상주 프로그램, 제어 프로그램 등
- OS의 핵심 부분(메모리에 상주)
- 가장 빈번하게 사용되는 기능들 담당
- 프로세스 관리, 메모리 관리 등

## 운영체제 역할

- 컴퓨터라는 복잡한 정보처리 시스템을 제어하고 관리하기 위한 소프트웨어
- 사용자가 컴퓨터 자원을 쉽게 쓸 수 있게 해준다.
- 운영체제는 프로세서에게 처리 작업을 할당하고 관리한다.

- **유저 인터페이스(편리성) 제공**
- **Resource management (효율성)**
  - HW resource(프로세스, 메모리, 입출력)
  - SW resource
- **Process, Thread 관리** : 프로세스에 CPU 배분, 작업 환경 제공
- **시스템 보호(System management)/ 보안**

> 컴퓨터 구조

1. 입출력 장치 : 입력 장치, 출력 장치(키보드, 모니터 등)
2. 중앙처리 장치 : 연산과 제어 기능 수행(CPU)
3. 기억 장치 : 주기억 장치, 보조기억 장치(메모리, 디스크 등)

> 소프트웨어 부분

1. 응용 소프트웨어 : 사용자가 직접 다루는 애플리케이션
2. 시스템 소프트웨어 : 사용자와 하드웨어 연결해주는 프로그램

## 운영체제 기본 원리

### 운영체제 부팅 순서

1. 비휘발성 메모리인 ROM(Read Only Memory)에는 POST(Power On Self-Test)와 부트로더(BootLoader)가 저장되어 있다.
   ![](https://velog.velcdn.com/images/urjimyu/post/ccc2abdd-df92-457e-83b5-c4a125177863/image.png) - POST : 컴퓨터 전원 켜지면 제일 먼저 실행되는 컴퓨터 이상 체크하는 프로그램 - Boot Loader : 운영체제 시동 전 미리 실행되어 커널이 올바르게 시동되는 데 필요한 모든 작업을 마무리하고 OS를 시동시키기 위한 목적의 프로그램. 하드디스크에 저장된 OS 프로그램을 가져와 RAM에 넘겨준다.
2. 인터럽트 : 사용자 입력 이벤트(인터럽트)를 기다리고, 인터럽트가 끝나면 인터럽트가 발생했던 주소를 기억해 돌아가서 다음 명령어를 수행하거나 대기상태로 돌아간다.

### interrupt-driven 방식

![](https://velog.velcdn.com/images/urjimyu/post/b0f7ec8b-9a9d-442d-b07a-98b2a69319bb/image.png)

- OS는 사용자 요청(Event 또는 Interrupt)에 적절한 자원을 분배해 요청을 처리하는 원리로 작동한다.
  > Interrupt 종류

1. H/W interrupt : I/O, 메모리, CPU와 관련 인터럽트.
2. S/W interrupt : 프로그램이 실행중 발생하는`Errors`, 운영체제 Services들에 대한 요청인 `System Call` 등

- S/W 인터럽트의 경우 한 작업이 자원을 계속 점유하는 등의 문제를 예방하기 위한 방법들이 필요하다.
  - Dual-Mode Execution : 유저 모드(사용자에게 인터페이스 제공)와 커널 모드(기기 직접 관리)로 구분해 작업해서 사용자가 문제가 생겼을 때 접근하지 못하게 한다. `System Call`이란 유저모드에 들어온 명령어와 일치하는 커널 모드 명령어를 커널에서 실행해서 결과를 유저 모드에 넘기고 일을 마치는 것을 말한다.
    - Timer : 프로세스별로 유효 시간 부여해서 시간 지나면 종료시키기. 에러 발생해도 CPU를 계속 점유하지 못하도록 할 수 있다.

---

### 참고자료

[[IT 상식사전] 컴퓨터 운영체제의 개념과 역할 | 요즘IT]](https://yozm.wishket.com/magazine/detail/1453/)
[운영체제 OS](https://velog.io/@dddooo9/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C%EB%9E%80-%EC%A0%95%EC%9D%98-%EC%97%AD%ED%95%A0-%EA%B5%AC%EC%A1%B0)
[OS 구조와 원리](https://velog.io/@brian_kim/OS-%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%EA%B5%AC%EC%A1%B0%EC%99%80-%EC%9B%90%EB%A6%AC)
