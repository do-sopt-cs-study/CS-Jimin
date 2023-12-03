# 인터럽트(Interrupt)

- CPU가 명령을 차례로 수행할 때 중간에 끼어들어서 어떤 일을 수행하는 것을 말한다. 처리기 처리율을 높이기 위해 사용된다.
  - 예를 들어 입출력 장치들은 처리기보다 훨씬 느리기 때문에 프로그램이 긴 시간 정지될 수 있다. 이런 경우에 인터럽트를 사용하면 입출력 연산을 기다리는 동안 다른 명령을 처리할 수 있다.

## 인터럽트 부류

- 프로그램
- 타이머
- 입출력
- 하드웨어 실패

## 인터럽트 종류

### 1. 내부 인터럽트(=소프트웨어 인터럽트) / Trap

- CPU 내부에서 발생, 잘못된 명령 혹은 데이터 사용 시 발생
- 동기적
  - **프로그램 검사 인터럽트 Program check interrupt** : 프로그램적 오류( 0으로 나누기, over/under flow, 예외 등)
  - **시스템 콜 인터럽트 System call interrupt**

### 2. 외부 인터럽트(=하드웨어 인터럽트)

- 비동기적
  - **I/O(입출력) 인터럽트** : 입출력 작업이 종료되거나 오류에 의해 정지. 키보드, 마우스 등
  - **Power fail(전원 이상) 인터럽트** : 전원이 이상현상에 의해 공급 중단
  - **Machine check(기계 착오) 인터럽트** : CPU의 기능이 잘못됨
  - **External(외부) 인터럽트** : 외부 장치로부터 인터럽트/`^C` 키 발생/타이머

## 인터럽트 과정

1. 인터럽트 발생 장소, 원인 파악(Interrupt handling)
2. 인터럽트 서비스 할 것인지 결정
3. 인터럽트 서비스 루틴 호출(Interrupt service)

# 시스템 콜(System Call)

- 운영체제에 요청하는 함수들(운영체제로 진입하는 함수) = System call
- 커널 영역의 기능을 사용자 모드가 사용 가능하게, 즉 **프로세스가 하드웨어에 직접 접근해서 필요한 기능을 사용할 수 있게** 한다.

## 시스템 콜 유형

- **프로세스 제어**
  - 끝내기(end), 중지(abort)
  - 적재(load), 실행(execute)
  - 프로세스 생성(create process)
  - 프로세스 속성 획득과 설정(get process attribute and set process attribute)
  - 시간 대기(wait time)
  - 사건 대기(wait event)
  - 사건을 알림(signal event)
  - 메모리 할당 및 해제 : malloc, free
- **파일 조작**
  - 파일 생성(create file), 파일 삭제(delete file)
  - 열기(open), 닫기(close)
  - 읽기(read), 쓰기(write), 위치 변경(reposition)
  - 파일 속성 획득 및 설정(get file attribute and set file attribute)
- **장치 조작**
  - 장치를 요구(request devices), 장치를 방출release device)
  - 읽기, 쓰기, 위치 변경
  - 장치 속성 획득, 장치 속성 설정
  - 장치의 논리적 부착(attach) 또는 분리(detach)
- **정보 유지보수**
  - 시간과 날짜의 설정과 획득(time)
  - 시스템 데이터의 설정과 획득(date)
  - 프로세스 파일, 장치 속성의 획득 및 설정
- **통신과 보호**
  - 통신 연결의 생성, 제거
  - 메시지의 송신, 수신
  - 상태 정보 전달
  - 원격 장치의 부착 및 분리

---

### Reference

[[운영체제] 시스템 콜과 인터럽트](https://latter2005.tistory.com/43)
[운영체제 04 : 시스템 콜 (시스템 호출, System Call)](https://luckyyowu.tistory.com/133)
운영체제 - 내부구조 및 설계원리 8판(전광일 외)
