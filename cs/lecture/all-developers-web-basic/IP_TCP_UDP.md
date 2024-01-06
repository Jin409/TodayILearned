# IP (인터넷 프로토콜)

![IP-주소-부여](https://github.com/Jin409/TodayILearned/assets/77621712/1deaf3e8-12e6-41e9-b450-c9a9cc921151)

## 역할

- 지정한 IP 주소로 데이터를 전달
- 패킷이라는 단위로 전달한다.

## 패킷의 구조

![패킷의-구조](https://github.com/Jin409/TodayILearned/assets/77621712/cfa5f524-3b55-4583-acc6-09f9d9304c6e)

패킷의 구조는 위와 같이 전송 데이터를 출발지 / 도착지 IP 감싸고 있는 형태이다.

## 패킷 전달

![클라이언트의-패킷-전달](https://github.com/Jin409/TodayILearned/assets/77621712/2125cf17-affa-48f7-8cb9-48871a3e1002)

클라이언트는 패킷을 목적지(서버의 IP) 를 노드끼리 서로 통신하여 찾으며 계속 전달한다.

![서버의-패킷-전달](https://github.com/Jin409/TodayILearned/assets/77621712/a4537544-1cbf-4ee7-90cb-4e2857324506)

서버는 패킷을 클라이언트까지 응답 데이터를 넣어 전달한다.

## IP 프로토콜의 한계

### 1. 비연결성

- 패킷을 받을 대상이 없거나 서비스 불능 상태여도 전송한다.

### 2. 비신뢰성

- 패킷이 중간에 소실되는 경우
- 패킷의 순서가 뒤섞이는 경우
  ![패킷-전달-순서-문제](https://github.com/Jin409/TodayILearned/assets/77621712/709a506b-2904-4195-afc8-388380ba44b8)

### 3. 프로그램 구분

- 같은 IP 를 사용하는 서버에서 애플리케이션이 둘 이상인 경우

# TCP + UDP

- IP 프로토콜 위에서 전송계층에서 동작한다.

## TCP

[IP 프로토콜의 한계](#ip-프로토콜의-한계) 를 극복해준다.

### 인터넷 프로토콜 스택의 4계층

![인터넷-프로토콜-스택의-계층](https://github.com/Jin409/TodayILearned/assets/77621712/b1aab3d0-a4fd-432c-8798-e80ca4333ed5)

![프로토콜-계층](https://github.com/Jin409/TodayILearned/assets/77621712/2941e44d-aa21-4d50-b5d0-03fd69dc81f4)

IP 패킷에서 전송 계층으로 이동하며 `TCP 세그먼트`가 만들어진다.
여기서 TCP 세그먼트는 `TCP 헤더 + IP 패킷`이다.

![TCP/IP-패킷-정보](https://github.com/Jin409/TodayILearned/assets/77621712/f58633ce-c464-4e59-9ae1-96d7ced3f356)
TCP 세그먼트는 전송을 제어하고, 순서를 기록하고 검증 정보를 담기 때문에 IP 프로토콜의 한계를 극복할 수 있게 된다.

### TCP 의 특징

1. 연결지향

- IP 프로토콜의 비연결성과 대조된다.
- 연결할 수 있는지 확인하고 전송한다.

2. 데이터 전달 보증

- 데이터 전송하고 그 이후에 잘 받았다는 사인을 보낸다.

3. 순서 보장
   ![패킷-순서-보장](https://github.com/Jin409/TodayILearned/assets/77621712/3e5923f7-355f-4e6e-9450-2b91b7f23040)

- 패킷1,2,3 으로 와야 하는데 3부터 왔기 때문에 서버는 1 이후를 다 버리고 클라이언트 측에 2부터 다시 보낼 것을 요청한다.

## TCP 3 way handshake

![3-way](https://github.com/Jin409/TodayILearned/assets/77621712/b3fec125-a5ea-4e2f-b442-161a1671835e)

1. 클라이언트 -> 서버로 Synchronized 연결 요청
2. 서버 -> 클라이언트로 ACK (요청 수락) + 연결 요청 보냄
3. 클라이언트 -> 서버로 요청 수락 보냄

이렇게 연결이 되고 나서 데이터를 전송한다.

## UDP

- IP 와 거의 같다.
- IP 와의 차이점 : `PORT`
- UDP + 애플리케이션 계층에서 추가적으로 작업하면 된다.

### 최근 각광받는 이유

- HTTP/3 에서 3-way hanshake 과정을 줄이기 위해서 UDP 를 사용

