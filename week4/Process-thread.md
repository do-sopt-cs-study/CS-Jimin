# 프로세스란?

![](https://velog.velcdn.com/images/urjimyu/post/d39c99a3-fd6d-4254-9847-83f776ebb602/image.png)

- 운영체제로부터 자원을 할당받은 **작업의 단위**
- 작업중인 프로그램. 즉, 메모리에 적재되어 CPU 자원을 할당 받아 프로그램이 실행되고 있는 상태를 말한다.
- 프로세스는 다른 프로세스의 메모리에 직접 접근이 불가하다.
- 프로그램이 복잡해지면서 프로세스 하나만으로 프로그램 실행하기에 한계가 생겼다. 이런 한계를 보완하고자 생긴 게 스레드이다.

- 프로세스가 할당 받는 메모리 영역
  **정적 영역**

  1. 코드 영역 : 프로그램 함수 코드들이 CPU가 해석 가능한 기계어 형태로 저장
  2. 데이터 영역 : 전역 변수나 각종 데이터가 모여 있는 영역
     **동적 영역**
  3. 스택 영역 : 지역 변수처럼 함수 종료되면 돌아올 임시 자료 저장하는 독립적인 공간. 함수 호출과 함께 할당되어 함수 호출이 완료되면 소멸한다.

  4. 힙 영역 : 동적 할당되는 데이터를 위한 공간. 생성자, 인스턴스 같은 데이터가 해당된다. 사용자에 의해 메모리 공간이 동적으로 할당/해제된다.
     > stack overflow : 스택 영역을 초과할 때 발생

# 스레드란?

![](https://velog.velcdn.com/images/urjimyu/post/fe4cb453-2dbc-442a-8f69-945486912488/image.png)

- 프로세스가 할당받은 자원을 이용하는 **실행 흐름의 단위**
- 프로세스 자원을 공유하면서 동시 진행되는 작업의 갈래.
- 예를 들어, 크롬 부라우저를 실행하면서 유튜브로 노래도 듣고 온라인 쇼핑도 하는 경우, 크롬 실행이라는 한 프로세스 안에 여러 작업 흐름들, 즉 스레드가 동시에 진행된다.

  > **비동기식 및 병렬 애플리케이션**

  - 애플리케이션이 실행되는 동안 사용자가 다른 작업을 할 수 있게 하는 것.
  - 예) 이메일 보내면서 사용자 이메일 읽는 작업 동시 수행

![](https://velog.velcdn.com/images/urjimyu/post/270d16f5-3ae9-420a-bb5f-9d2c7326f3fb/image.png)

- 이때 스레드는 스택 영역만 할당 받아 복사하고 나머지 영역들은 다른 스레드들과 공유된다. 즉, 각 스레드는 다른 영역은 공유하지만 각자 별도의 stack을 가지고 있다. 따라서 스레드는 각자 독립적인 실행 흐름을 가질 수 있다.

# 프로세스 vs 스레드

- 프로세스는 각각의 메모리 영역을 할당 받기 때문에 다른 프로세스의 변수나 자료에 접근이 불가하다. 반면 스레드는 메모리 힙 메모리 공유가 가능하다.

### 멀티태스킹

- 한 OS 안에서 여러 프로세스가 실행되는 것

### 멀티스레드

- 한 프로세스가 여러 작업을 여러 스레드로 동시 처리하는 것(병행 실행)
- 여러 작업 처리가 동시에 가능하므로 시스템 성능 향상이 가능하다.
  ![](https://velog.velcdn.com/images/urjimyu/post/43cbb9b6-b2dd-4268-8c73-6f796e9b07b6/image.png)

### 멀티스레드의 장점

- **사용자 응답성**이 높아진다
  - 일부 스레드 처리가 지연되어도 다른 스레드는 작업 계속 가능!
- **자원 공유**로 **효율성** 증가
  - 같은 자원을 쓰려는 두 프로세스가 있다면 context switch가 발생한다. 하지만 한 프로세스에 여러 스레드가 한 자원을 동시에 사용 가능하므로 context switch가 발생하지 않는다.(커널 개입 피할 수 있다)
- **경제성**
  - context switch 등에 비해 효율적이다
- **멀티 프로세서 활용**
  - 병렬처리로 성능 향상
- Context-Switching 시 공유하는 메모리만큼 메모리 자원을 아낄 수 있다.

### 멀티스레드의 단점

- 스레드 하나 때문에 모든 프로세스가 종료될 수 있다.
- 동기화 문제 발생 가능성이 있다.
  > 동기화 문제
  - 여러 스레드가 함께 전역 변수를 사용할 때 발생 가능한 충돌
  - 운영체제는 스레드 스케줄링을 자동으로 해주지 않음.

---

### 참고 자료📚

[완전히 정복하는 프로세스 vs 스레드 개념](https://inpa.tistory.com/entry/%F0%9F%91%A9%E2%80%8D%F0%9F%92%BB-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%E2%9A%94%EF%B8%8F-%EC%93%B0%EB%A0%88%EB%93%9C-%EC%B0%A8%EC%9D%B4)
[프로세스와 스레드](https://velog.io/@aeong98/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9COS-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4%EC%99%80-%EC%8A%A4%EB%A0%88%EB%93%9C)
[스레드 이해하기](https://adjh54.tistory.com/167)