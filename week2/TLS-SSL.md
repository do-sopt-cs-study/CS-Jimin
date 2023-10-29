# [CS / 네트워크] TLS/SSL 프로토콜의 역할과 handshake: 암호화된 통신 설정 과정

## TLS, SSL 프로토콜

### TLS, SSL 관계

- WWW(월드 와이드 웹)의 안전한 데이터 통신을 위해 개발되었다.
- 보안상 결점이 있어 이를 보완한 TLS가 나오게 되었다.
- TLS 출시 이후 SSL은 모두 사용되지 않는다.

### 공통점

- 둘 다 데이터 암호화에 사용되는 프로토콜이다.
- 네트워크를 통해 연결된 두 대상을 모두 인증해서 안전한 데이터 교환을 돕는다.
- 디지털 인증서를 사용해서 핸드셰이크를 용이하게 하고 브라우저와 웹 서버간 암호화된 통신을 돕는다.
- HTTP에 SSL, TLS 프로토콜 설정을 통해 보안을 강화하는 것이 HTTPS이다.

### 차이점

- SSL : 명시적 연결
- TLS : 암시적 연결

- 브라우저가 웹사이트 연결 전에 해당 사이트에 SSL/TLS 인증서가 있는지 확인한다.

### TLS 핸드셰이크 과정

![](https://velog.velcdn.com/images/urjimyu/post/92348a44-a441-414f-85a8-6069fa1e9829/image.png)

- 핸드셰이크 단계는 키 교환 알고리즘의 종류 등에 따라 달라질 수 있다. TLS에 사용되는 대표적인 알고리즘인 RSA 키 교환 알고리즘은 현재는 안전하지 않은 것으로 간주되지만 1.3 이전의 TLS 버전에서는 사용되었다.

#### 단계

1. 클라이언트의 'hello' 메시지 송신
   핸드셰이크를 시작한다. 메시지에는 클라이언트가 지원하는 TLS 버전, 지원되는 암호 모음 및 일련의 랜덤 바이트(client random)가 포함되어 있다.

2. 서버의 'hello' 메시지
   서버는 클라이언트 hello 메시지에 대한 응답으로 서버의 SSL 인증서, 서버가 선택한 암호 모음 및 서버가 생성한 또 다른 임의 바이트 문자열(server random)이 포함된 메시지를 전송한다.
3. 인증
   클라이언트는 서버의 SSL 인증서를 발급한 인증 기관과 함께 확인한다. 이것은 명시되어 있는 서버가 실제 서버가 맞는지 확인하고, 클라이언트가 도메인의 실제 소유자와 상호 작용하고 있는 게 맞는지 확인하는 절차이다.
4. premaster secret
   클라이언트는 "premaster secret"이라고 불리는 임의의 바이트 문자열을 하나 더 전송한다. premaster secret은 공개키로 암호화되어 서버에서 비밀키로만 복호화가 가능하다. 이때 암호화에 쓰이는 공개키는 서버의 SSL 인증서에서 가져온다.
5. 비밀 키 사용
   서버가 premaster secret을 복화한다.
6. 세션 키 생성
   클라이언트와 서버 모두 클라이언트 랜덤, 서버 랜덤, premaster secret에서 세션 키를 생성한다. 각자 생성한 세션 키는 서로 일치해야 한다.
7. 클라이언트 준비
   클라이언트는 세션 키로 암호화된 "완료" 메시지를 보낸다.
8. 서버 준비 완료
   서버는 세션 키로 암호화된 "완료" 메시지를 보낸다.
9. 보안 대칭 암호화 달성
   핸드셰이크가 완료되고 세션 키를 사용해서 통신이 계속된다.

---

### 참고자료

[cloudflare learning center](https://www.cloudflare.com/learning/ssl/what-happens-in-a-tls-handshake/#:~:text=A%20TLS%20handshake%20is%20the,and%20agree%20on%20session%20keys.)
[aws docs](https://aws.amazon.com/ko/compare/the-difference-between-ssl-and-tls/)
