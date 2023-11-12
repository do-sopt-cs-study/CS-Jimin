# 프로세스의 주소 공간

![](https://velog.velcdn.com/images/urjimyu/post/8ec05132-b447-44de-ad10-3529496672e9/image.png)

**정적 영역**

1.  Text(Code) 영역 - 프로그램 함수 코드들이 CPU가 해석 가능한 기계어 형태로 저장 - 프로그램이 수정되지 않도록 ReadOnly 상태로 되어 있다.

2.  Data 영역

    - 전역 변수 등 프로그램이 사용할 수 있는 데이터를 저장하는 영역
    - 전역 변수 참조 코드가 존재하면, 컴파일 후 data 영역을 참조한다.
      프로그램 시작 시 할당되고 프로그램 종료 시 소멸
    - 초기화되지 않은 변수는 BSS 영역에 저장

> BSS(Block Stated Symbol)

    - 초기값 없는 전역변수, 배열, 정적 변수가 저장되는 영역
    - 초기화되지 않은 변수는 프로그램 실행 시 영역만 잡아주고 값은 저장할 필요가 없기 때문에 BBS에 저장한다.

**동적 영역**

3. Stack 영역

- 지역 변수, 매개 변수처럼 함수 종료되면 돌아올 임시 자료 저장하는 독립적인 공간.
- 함수 호출과 함께 할당되어 함수 호출이 완료되면 소멸한다.
- 메모리의 높은 주소에서 낮은 주소 방향으로 할당.
- stack은 Heap 영역에 위치한 실제 Object의 참조를 갖고 있다. - 생성과 동시에 크기가 정해지기 때문에 Heap 영역과 무관하게 크기 제한을 가져서 stack overflow 같은 현상이 발생하기도 한다.

> stack overflow
> stack 영역을 초과할 때 발생
> (재귀 함수가 너무 깊게 호출되거나 함수가 지역변수를 과다하게 가지고 있을 때 등)

4.  Heap 영역

- 런타임에 크기가 결정된다.
- 동적 할당되는 데이터를 위한 공간. 생성자, 인스턴스 같은 데이터가 해당된다. 사용자에 의해 메모리 공간이 동적으로 할당/해제된다.
- 메모리의 낮은 주소에서 높은 주소의 방향으로 할당.

# 프로세스의 주소 공간 관리

- 메모리는 한정되어 있기 때문에 프로세스는 메모리를 절약하려고 한다.이런 맥락에서 데이터 공유를 통해 메모리 사용량을 줄이기 위해 주소 공간이 나뉘어져 있다고 이해할 수 있다.

## Code 영역

- 프로그램 함수 코드들이기 때문에 결국 프로그램 자체에서는 모두 같은 내용이라서 따로 관리해 공유하면 메모리 사용량을 줄일 수 있기 때문이다.

## Data, Stack 영역

- 이 두 영역들을 구분해 사용하는 이유는 역할을 분배하기 위함이다.

- Stack 영역 => 함수 흐름 관리
- Data 영역 => 전역 변수, static 변수 관리

- 선입선출 구조를 가진 stack은 데이터를 임의로 꺼낼 수 없다. 하지만 전역 변수는 어디서도 접근 가능해야 하기 때문에 Data에서 따로 관리해준다.
- 스레드는 각자 독립된 Stack을 가지며 Data 영역은 공유한다. 이를 통해 메모리 절약이 가능해지는 것이다.

---

## 참고자료📚

[[운영체제] 프로세스 주소 공간](https://velog.io/@klm03025/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EC%A3%BC%EC%86%8C-%EA%B3%B5%EA%B0%84)
[[운영체제] 프로세스 주소공간](https://velog.io/@klloo/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EC%A3%BC%EC%86%8C%EA%B3%B5%EA%B0%84)