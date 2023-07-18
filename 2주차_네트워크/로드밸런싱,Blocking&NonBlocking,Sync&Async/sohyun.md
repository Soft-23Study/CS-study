# 로드밸런싱, Blocking/Non-blocking & Synchronous/Asynchronous

## 로드 밸런싱

[https://gyoogle.dev/blog/computer-science/network/Load Balancing.html](https://gyoogle.dev/blog/computer-science/network/Load%20Balancing.html)

- 여러 CPU / 저장 장치에 컴퓨터 자원들에게 작업을 나누어줌
- 여러 서버에 균등하게 트래픽 분산
- 부하를 나누어줌

### **로드 밸런서가 서버를 선택하는 방식**

- 라운드 로빈(Round Robin) : CPU 스케줄링의 라운드 로빈 방식 활용
    - 서버에 들어온  요청을 순서대로 돌아가면서 배정
    - 여러 대의 서버가 동일한 스펙 갖고 있고 / 서버와의 연결이 오래 지속되지 않는 경우에 활용하기에 적합
- Least Connections
    - 요청이 들어온 시점에 가장 적은 연결 상태를 보이는 서버에 우선적으로 트래픽 배분
    - 연결 개수가 가장 적은 서버 선택
    - 자주 트래픽으로 인해 세션이 길어지는 경우 권장
    - 서버에 분배 된 트래픽들이 일정하지 않은 경우에 적합
- Source
    - IP 해시 방식
    - 클라이언트의 IP 주소를 특정 서버로 매핑하여 요청 처
    - 사용자 IP를 해싱하여 분배 (특정 사용자가 항상 같은 서버로 연결되는 것 보장)

[로드밸런서(Load Balancer)의 개념과 특징](https://m.post.naver.com/viewer/postView.naver?volumeNo=27046347&memberNo=2521903)

### **[#](https://gyoogle.dev/blog/computer-science/network/Load%20Balancing.html#%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3-%E1%84%87%E1%85%A2%E1%86%AF%E1%84%85%E1%85%A5%E1%86%AB%E1%84%89%E1%85%A5-%E1%84%8C%E1%85%A1%E1%86%BC%E1%84%8B%E1%85%A2-%E1%84%83%E1%85%A2%E1%84%87%E1%85%B5)로드 밸런서 장애 대비**

서버를 분배하는 로드 밸런서에 문제가 생길 수 있기 때문에 로드 밸런서를 이중화하여 대비한다.

- Active 상태 : 서버에서 클라이언트에 접속해 데이터 보내는 방식
- Passive 상태 : 클라이언트에서 서버로 접속해 데이터 보내는 방식
- 

---

## Blocking/Non-blocking & Synchronous/Asynchronous

[https://gyoogle.dev/blog/computer-science/network/Blocking,Non-blocking & Synchronous,Asynchronous.html](https://gyoogle.dev/blog/computer-science/network/Blocking,Non-blocking%20&%20Synchronous,Asynchronous.html)
