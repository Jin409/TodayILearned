# 한번에 둘 이상의 데이터를 전달해야 한다면?

화상통화를 하며 게임을 하고 있다고 가정해보자
화상통화를 위한 데이터인지, 게임을 위한 데이터인지 알 수 없다.

# PORT

## 역할

같은 IP 내에서 프로세스를 구분한다.

![포트의-역할](https://github.com/Jin409/TodayILearned/assets/77621712/4701eb20-9245-470d-88e9-8a7f5feced3f)

- 클라이언트가 10010 포트로, 도착지는 웹 브라우저로 하여 80포트로 요청을 전송
- 웹 브라우저에서는 80포트로 들어온 요청에 대한 응답을 10010 포트로 전송

# DNS

## IP 의 불편한 점

- 기억하기 어렵다
- 변경 가능성이 있다.

## DNS 사용

- DNS 서버에 IP 주소를 등록할 수 있다.

![DNS-사용](https://github.com/Jin409/TodayILearned/assets/77621712/9afd9d5f-ca1f-4324-a482-683fcff84939)

위처럼, 클라이언트가 google.com 에 대한 ip 를 DNS 서버에 요청하면 이를 DNS 서버가 알려준다.
이에 대한 응답을 얻고 클라이언트는 google.com 의 서버로 요청을 보낼 수 있다.




