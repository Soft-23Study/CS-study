# HTTP 버전 별 특징

---

### HTTP/0.9

- 버전 번호도 없었을 때 (구별하기 위해 0.9 라고 칭함)

- 요청 : 단일 라인으로 구성
- 가능한 메서드는 only GET

- 응답 : 단순하게 파일 내용 자체 / 헤더X / only HTML /  상태코드X
    - 문제 있을 경우 : 파일 내부에 문제에 대한 설명과 함께 보냄

```
GET /myapp.html
```

---

https://hirlawldo.tistory.com/106

### HTTP/1.0

- 버전 정보 전송 시작
- 헤더 도입
- method : GET , HEAD , POST
- connection : 응답 직후 종료

- 요청 :
    - 메타 데이터 전송 허용
    - html 파일 이외의 다른 문서 전송 기능 추가

- 응답
    - 상태 코드가 응답 시작 부분에 붙어 전송됨 (성공/실패 알 수 있음 → 결과에 대한 처리 가능)

- 예시

```
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html
<HTML>
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
```

단점 : 커넥션 관련 

- 모든 요청에 따라 새로운 연결을 열고
- 응답이 전송된 후 즉시 닫아서 새로운 연결을 설정할때 마다 TCP 3-way Handshake 발생

```
TCP/IP 프로토콜을 이용해서 통신을 하는 응용프로그램이 
데이터를 전송하기 전에 
먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정
```

---

### HTTP/1.1

- 오늘 날 가장 많이 사용되는 http 버전
- 응답 속도 빨라지고 대역폭 절약
    - 청크 응답 지원
    - 추가적인 캐시 제어 매커니즘 도입
- Megod : GET, HEAD, POST, PUT, DELETE, TRACE, OPTIONS
- 커넥션  : 재사용 가능
    - 연결을 설정하기 전에 TCP 3-way Handshake 발생. 마지막으로 모든 데이터를 Client로 보낸 후 Server는 더 이상 보낼 데이터가 없다는 메세지를 보내고, 그 이후 연결을 닫는다.
    - 즉,  HTTP1.1은 여러 Request-Response에 대해 동일한 연결을 재사용할 수 있다

```
커넥션 ??
클라이언트와 서버가 http 요청 / 응답 교환 하기 전에 TCP 커넥션 설정해야함 / 
어떻게 열어줄

기존 HTTP 1.0 은 각각 요청/응답에 대해 별도 커넥션을 열었음

1.1 : 지속 커넥션을 사용
```

- 지속 커넥션 관련
    
    [[HTTP] keep alive란? (persistent connection에 대하여)](https://etloveguitar.tistory.com/137)
    

- 단점 : HOLB (Head Of Line Blocking) - 특정 응답 지연
    - Http Pipelining으로 하나의 connection을 통해 다수개의 파일을 Request/Response 받을 수 있지만 첫 번째 Response가 지연되면, 다음 두, 세번째 Response는 첫번째 응답처리가 완료되기 전까지 대기하게 되기 때문에 HOLB가 발생한다.

---

### HTTP/2.0

- HTTP 1.1 프로토콜을 계승해 동일한 API면서 성능 향상에 초점을 맞췄다.

- Stream: 구성된 연결 내에서 전달되는 바이트의 양방향 흐름, 하나 이상의 메시지가 전달 가능하다.
- Message: 논리적 요청 또는 응답 메시지에 매핑되는 프레임의 전체 시퀀스
- Frame:  Http/2.0에서 통신의 최소 단위

- binary framing
    
    
    - test 형식 X
    - 요청 응답 메시지는 프레임 단위로 나누어지고 바이너리 형식으로 인코딩 됨
    - 바이너리 = 컴퓨터가 더 이해하기 쉬움
    - 파싱 , 전송 속도 빨라짐
- multiplex streaming
        
    - Tcp 연결이 성립된후 N개의 스트림을 생성할 수 있
    - 스트림은 파이프와 다르게 양방향 데이터 흐름이 가능하고 각 스트림에는 **고유 식별자**와 **우선순위 정보**가 있습니다.
    - 각 메시지는 하나의 논리적 HTTP 메시지(요청 or 응답)이고 하나 이상의 프레임으로 구성됩니다.
    - 프레임을 전달받은 쪽에서는 프레임의 헤더에 있는 스트림 식별자를 통해 프레임을 재조립하여 요청/응답 메시지를 확인할 수 있습니다.

- 하나의 tcp 커넥션 만으로 해당 휍페이지의 모든 요청과 응답 데이터 전송이 가능하고
- 응답 순서에 무관하게 데이터 처리 가능
