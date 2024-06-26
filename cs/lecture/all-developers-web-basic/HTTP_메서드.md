# HTTP 메서드

## HTTP 메서드의 필요성

- 회원을 등록, 조회, 수정하는 API 를 설계한다고 가정해보자
    - create-members, get-members, update-members 이렇게 해야 할까?
- URI 는 `리소스를 식별`하는 역할!
    - 회원을 등록, 조회, 수정하는 API 에서 리소스는 `members`이다.
    - 그렇다면 `행위` 는 누가 식별할까?
        - 이를 HTTP 메서드가 한다.

## HTTP 메서드의 종류

- GET: 리소스 조회
- POST: 요청 데이터 처리, 주로 등록에 사용
- PUT: 리소스를 대체, 해당 리소스가 없으면 생성
- PATCH: 리소스 부분 변경
- DELETE: 리소스 삭제
- HEAD: GET 과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)을 설명(주로 CORS에서 사용)
- CONNECT: 대상 리소스로 식별되는 서버에 대한 터널을 설정
- TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행

## GET

```
GET /search?q=hello HTTP/1.1
Host: www.google.com
```

- 리소스 조회
- 서버에 전달하고 싶은 데이터는 쿼리를 통해서 전달한다.
- 메시지 바디를 사용해서 데이터를 전달할 수 있지만, 지원하는 곳이 많지 않다.

## POST

- 요청 데이터 처리
- 메시지 바디를 통해 서버로 요청 데이터 전달
- 전달된 데이터로 신규 리소스를 등록하거나 프로세스 처리를 한다.

### 요청 데이터를 '처리'한다는 것이 무슨 뜻일까

- 리소스에 URI POST 요청이 오면 데이터를 어떻게 처리할지 리소스마다 따로 정해야 한다.
    - 즉, 정해진 것은 없다.
- ex) 게시판에 post 를 하면, 게시글을 등록하는 처리를 할 수도 있다.
    - 그러나 게시판에 다른 리소스를 post 하면 댓글을 등록하는 것일 수도 있다.

### POST 의 용도

1. 새 리소스 생성
2. 요청 데이터 처리
    - 반드시 새로운 리소스가 생성되지 않아도 된다.
        - ex) 배달 중을 배달 완료로 변경
3. 다른 메서드로 처리하기 애매한 경우
    - 조회를 하고자 하는데, body 가 필요한 경우에도 조회여도 POST 를 사용한다.

## PUT

- 리소스를 대체
    - 리소스가 없으면 생성
- `클라이언트가 리소스를 식별할 수 있다.`
    - 클라이언트가 리소스 위치를 알고 URI 를 지정한다.
    - POST 와의 차이점

### PUT 은 리소스를 완전히 대체한다.

![리소스-대체](https://github.com/Jin409/TodayILearned/assets/77621712/1b30d694-0a73-4073-afa5-6e548178b85c)

- 위처럼, name 와 age 가 있는 상태에서 request body 에 age 만 담는다면 서버에서 갖고 있는 리소스는 age 만 남게 된다.

## PATCH

- 리소스를 부분 변경할 수 있다.

### PATCH 는 부분 변경한다.

![부분-변경](https://github.com/Jin409/TodayILearned/assets/77621712/ff7fabb5-3592-4fd7-b05d-d79991674ed2)

- PATCH 는 부분 변경하기 때문에, age 만 넘기면 age 만 변경된다.

## DELETE

- 리소스 삭제

## HTTP 메서드의 속성

### 안전

- 호출해도 리소스를 변경하지 않는다.

### 멱등

- 한번 호출하든, 100번 호출하든 결과가 똑같다.
    - 멱등한 메서드
        - GET
        - PUT
        - DELETE
    - 멱등하지 않은 메서드
        - POST : 여러번 호출하면 같은 결제가 중복해서 발생할 수 있다.
        - PATCH