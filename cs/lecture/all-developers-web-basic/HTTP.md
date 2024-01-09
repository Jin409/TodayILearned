# HTTP 의 특징

## 클라이언트 - 서버 구조

- Request, Response 구조
- 서버가 요청에 대한 결과를 만들어서 응답한다.

## 무상태 프로토콜

- stateful
    - 서버가 이전의 상태를 저장한다.
    - 중간에 다른 점원으로 바뀌면 안된다.
- stateless
    - 서버가 이전의 상태를 저장하지 않는다.
    - 중간에 다른 점원으로 바뀌어도 된다.
    - 갑자기 고객이 증가해도 점원을 대거 투입할 수 있다.
    - `무한히 서버의 증설이 가능해진다.`
      만약, 기존에 대응하던 서버가 장애가 나서 다른 서버로 대체 하더라도 아무런 문제가 나지 않는다.
- 실무에서의 한계
    - 모든 것을 무상태로 설계할 수 없는 경우도 있다.
    - ex) 로그인
    - 그래서 일반적으로 브라우저의 쿠키나 서버의 세션을 이용한다.
    - 무상태의 경우에는 전송하는 데이터의 양이 방대하다.

## 비연결성

요청을 주고 받을 때만 연결을 하고 이후에는 끊어버린다. -> 자원 낭비가 없다.<br>
동시에 연결을 유지하지 않아도 된다.

- 이로 인해 1시간동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작다.
- 서버 자원을 효율적으로 사용할 수 있다.

### 단점

TCP/IP 연결을 매번 새로 맺어야 한다.

### 지속연결

html 페이지 하나를 받을 때까지는 `지속 연결`을 유지한다.

![지속연결없는경우](https://github.com/Jin409/TodayILearned/assets/77621712/329f0486-c098-437d-82d7-24ed40df7f0b)

지속연결이 되지 않는 경우에는 위처럼 필요한 데이터를 모두 받아올 때까지 매번 새로 연결과 종료를 해야 했다.

![지속연결인경우](https://github.com/Jin409/TodayILearned/assets/77621712/aa94f291-00e4-4a6f-b512-74f5e36b750e)

그러나 지속연결을 유지하는 경우에는 html 페이지 하나를 모두 받을 때까지 이를 유지하여 시간을 절약한다.

# HTTP 메시지

## 메시지 구조

![http-메시지-구조](https://github.com/Jin409/TodayILearned/assets/77621712/fa93e285-012b-438e-942b-3255f09bed13)

## 요청 메시지

![요청-메시지](https://github.com/Jin409/TodayILearned/assets/77621712/f1708cee-8678-41a5-8058-1332b4324726)

## 응답 메시지

![응답 메시지](https://github.com/Jin409/TodayILearned/assets/77621712/48f4072c-5c1f-491f-931b-8438842248d9)

## 요청과 응답의 형태

```
요청 형태
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

```
응답 형태
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423
<html>
<body>...</body>
</html>
```

## 시작 라인

### request line (요청하는 경우)

- http 의 메서드 (GET, POST, PUT, DELETE ...)
- request-target (path) 요청 대상
    - 절대 경로로 시작한다.
- http version

### status line (응답하는 경우)

- space 공백
- status-code

## HTTP 헤더

### 용도

- 전송에 필요한 부가정보
- 바디의 크기
- 인증 정보
- 요청 웹 브라우저 정보
- 캐시에 대한 정보
- => 바디 이외의 메타 정보가 모두 들어가 있다.

## HTTP 메시지 바디

- 실제 전송할 데이터
