# google.com 에 접속했을 때 일어나는 일

## [www.google.com](http://www.google.com) 에 접속했을 때 일어나는 일

---

### 요약

1. 사용자가 브라우저에 도메인주소 입력
2. 해당 도메인이름으로 dns 서버에서 서버의 진짜 ip 주소를 찾음
3. 찾은 ip주소로 라우팅 수행 + arp 로 목적지 mac 주소 알아내기
4. 서버에 tcp 3-way handshake 로 연결 수립
5. 클라→서버로 http 요청 전송
6. 서버에서 http 응답
7. 브라우저에서 도착한 http 응답을 출력

[https://gyoogle.dev/blog/web-knowledge/브라우저 동작 방법.html](https://gyoogle.dev/blog/web-knowledge/%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%20%EB%8F%99%EC%9E%91%20%EB%B0%A9%EB%B2%95.html)