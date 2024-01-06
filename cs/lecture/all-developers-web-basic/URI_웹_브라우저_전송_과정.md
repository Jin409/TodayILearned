# URI

- 리소스를 식별한다.

![uri](https://github.com/Jin409/TodayILearned/assets/77621712/1f48c3d8-c779-4f6a-8174-0cc1f5f57252)

## URL

- Resource Locator
- 리소스의 위치를 지정

## URN

- Resource Name
- 리소스의 이름을 지정
- URN 은 사실상 보편화되지 않아서 사용되지 않는다.

# URL 의 분석

https://www.google.com/search?q=hello&hl=ko

## URL 의 문법

- scheme://[userinfo@]host[:port][/path][?query][#fragment]

### scheme

- 주로 프로토콜이 들어간다.
- http 는 80, https 는 443, 포트는 생략할 수 있다.

### host

- 호스트 주소

### port

- 포트 번호

### path

- 계층적인 구조로 이루어진다.
- ex) /members/1000

### query

- key=value 형태
- ?로 시작 & 로 추가 가능

### fragment

- html 내부 북마크 등에 사용한다
- 서버에 전송하는 정보는 아니다

# 웹 브라우저의 요청 흐름

## 1. HTTP 요청 메시지 전달

![첫번째흐름](https://github.com/Jin409/TodayILearned/assets/77621712/04ba3fd9-f890-4507-b270-492d11975b8d)

- DNS 서버로 ip 를 조회한다.
- HTTP 요청 메시지를 생성한다.

![HTTP-메시지](https://github.com/Jin409/TodayILearned/assets/77621712/e4898e24-32a0-41d0-88f3-109d18559286)

- 웹 브라우저에서 HTTP 메시지를 생성한다.
- SOCKET 라이브러리를 통해 TCP/IP 연결을 한다. 이 때 3-way handshake 를 한다.
- 전송 계층에서 TCP/IP 패킷을 생성하고 이가 인터넷으로 전달된다.
    - 이때의 전송 데이터는 위와 같이 생성된 HTTP-메시지이다.

## 2. HTTP 응답 메시지 전달

![http-응답-메시지](https://github.com/Jin409/TodayILearned/assets/77621712/f3a0812a-67d2-4ee1-a479-24324464a92a)

- Content-Type 은 아래의 데이터가 어떤 타입으로 작성되었는지 명시한다.

![서버-클라이언트-응답-전달](https://github.com/Jin409/TodayILearned/assets/77621712/c4d3c571-2db6-465e-b44a-56771f0222f3)

- 위처럼 응답이 전달되면 웹 브라우저가 이를 렌더링해서 띄운다