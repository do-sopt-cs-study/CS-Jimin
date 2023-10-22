### TCP란

![](https://velog.velcdn.com/images/urjimyu/post/74c30a1b-37fd-4816-8425-77daa6f162f7/image.png)

- OSI 7 레이어에서 중간에 위치한 Transport 계층과 관련된 개념으로, 전송 프로토콜 중 하나이다.
  - 프로토콜 : 데이터 교환 방식을 정의하는 규칙 체계

> TCP is [connection-oriented](https://en.wikipedia.org/wiki/Connection-oriented_communication), and a connection between client and server is established before data can be sent.(Wikipedia)

- TCP는 연결 지향형 프로토콜(Connection-oriented protocol)이다.
  즉, 데이터가 전송되기 전에 클라이언트와 서버의 연결이 이루어진다.
  따라서 서버는 클라이언트로부터 연결 요청이 오는지 수신 대기중일 것이다.
- **장점**
  three-way handshake, 재전송, 에러 검출과 같은 절차 덕분에 신뢰성이 높다.

- **단점**
  신뢰성을 높여주는 절차들 때문에 지연시간이 길어진다. 따라서 신뢰성이 필수적인 경우가 아닐 때는 UDP를 사용한다.

- TCP는 네트워크 혼잡 제어를 지원한다. 물론 그럼에도 약점은 존재한다.
  ([도스 공격](https://en.wikipedia.org/wiki/Denial-of-service_attack), [TCP 시퀀스 예측 공격](https://en.wikipedia.org/wiki/TCP_sequence_prediction_attack) 등,,)

> **TCP (Transmission Control Protocol)** is an important network [protocol](https://developer.mozilla.org/en-US/docs/Glossary/Protocol) that lets two hosts connect and exchange data streams. TCP **guarantees the delivery of data and packets in the same order as they were sent.**(MDN)

> TCP's role is to ensure the packets are reliably delivered, and error-free.

- 즉, 양 끝단의 사용자들이 데이터의 신뢰성에 대한 걱정을 할 필요 없도록 IP가 전달하는 패킷이 처음에 보낸 순서에 맞게 에러 없이 안전히 도착했는지 무결성을 보장해주는 역할을 한다.

### TCP의 연결 설정 : 3-way handshake

![](https://velog.velcdn.com/images/urjimyu/post/631f12aa-d8dc-44c4-b7f1-abe96cbde244/image.png)

1. 먼저 송신 측에서 수신 측으로 데이터를 주고 받기 위해 **SYN “initial request”** 패킷을 보낸다. 사람 간 대화로 치면 말문을 여는 느낌!

2. 그러면 서버 측에서(target server) 동의하는 의미로 **SYN-ACK 패킷**을 보낸다. 대화에서 “응 얘기해 봐” 같은 느낌!

3. 동의를 받았으니 이제 수신자는 **ACK 패킷을 서버에 보내** 데이터 보내는 과정에 대해 최종 확인. 이 이후부터 데이터를 보낼 수 있다.

이렇게 세 단계에 걸쳐 서로 확인을 하고 연결 설정하기 때문에 3-way handshaking이라고 표현한다. 서로 연결 설정을 위해 확인하고 승인하는 과정을 handshake🤝으로 표현한 게 귀엽다.

> **SYN(Synchronization) : 동기화
> ACK(Acknowledgement) : 승인**
> 이라는 의미를 생각하면 **데이터를 주고 받기 위한 동기화 요청 → 동기화 승인 → 최종 승인**으로 이해할 수 있다.

### TCP의 연결 해제 설정: 4-way handshaking

![](https://velog.velcdn.com/images/urjimyu/post/33f424cb-0d33-4cb8-843e-08fb416ef00b/image.png)

1. 클라이언트든 서버든 연결을 해제하고 싶은 쪽에서 **FIN을 보내 연결 해제 요청**을 보낸다.

2. FIN을 받으면 **ACK를 보내 해제 요청을 승인**한다는 것을 알린다.

3. 서버에서 **FIN을 보내 다른 쪽에 연결 해제 신호**를 보낸다.

4. 마지막으로 FIN을 수신한 TCP에서 **ACK를 보내서 최종 해제 승인**을 한다.

---

### 📚 참고자료

[TCP 연결 설정과 해제](https://velog.io/@yeseolee/3-Way-4-Way-HandshakeTCP-%EC%97%B0%EA%B2%B0-%EC%84%A4%EC%A0%95%EA%B3%BC-%ED%95%B4%EC%A0%9C)
[TCP 3-Way Handshake Process](https://www.geeksforgeeks.org/tcp-3-way-handshake-process/)
[Why TCP Connect Termination Need 4-Way-Handshake?](https://www.geeksforgeeks.org/why-tcp-connect-termination-need-4-way-handshake/)
[TCP Connection Termination](https://www.geeksforgeeks.org/tcp-connection-termination/)
