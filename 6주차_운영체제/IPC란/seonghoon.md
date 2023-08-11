# IPC란?

[[OS/운영체제] IPC란? - 정의, 종류, 방법 (velog.io)](https://velog.io/@yanghl98/OS%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-IPC%EB%9E%80)

## IPC의 종류

### File

파일을 통해 데이터를 주고 받는 것

### Shared Memory

커널에서 관리하는 공유되는 공통의 메모리 공간 (물론 가상메모리)

메모리 자체를 공유하므로 불필요한 오버헤드가 발생하지 않음 → 모든 IPC중에서 가장 빠르다.

다만, 상대방이 데이터를 언제 보낼지 받는 쪽에서는 모르기 때문에, 수시로 확인하는 busy waiting을 함 (자원 낭비가 크다)

### Pipe (Anonymous Pipe)

단방향 통신, 부모 프로세스 → 자식 프로세스에게 일방적으로 통신하는 기법

### FIFO (Named Pipe)

부모와 자식 프로세스간의 관계가 아니더라도 다른 프로세스끼리 통신이 가능함

읽기/쓰기가 동시에 가능하지 않으므로, 양방향 통신을 위해서는 두개의 FIFO파일이 필요함

### Message Queue

메세지마다 id를 부여하여, 어떤 프로세스 간이라도 통신이 가능

### Socket

네트워크로 연결된 컴퓨터 간 통신에 주로 사용되는 수단, 물론 같은 컴퓨터 내의 프로세스끼리도 통신 가능

다만, 파이프와 비교하면 초기화할 내용도 많고 시스템 자원도 많이 사용하므로, 같은 컴퓨터 내에서 소켓으로 통신하는 것은 비효율적이다.

양방향 통신.

Shared Memory → 대기가 없는 통신 (non-blocking, asynchronous)

Pipe, Socket → 대기가 있는 통신 (blocking, synchronous)

### 참고

[[운영체제] IPC 기법 (velog.io)](https://velog.io/@redgem92/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-IPC-%EA%B8%B0%EB%B2%95#:~:text=IPC%20%EC%A2%85%EB%A5%98%201%201.%20File%20%EC%82%AC%EC%9A%A9%20%ED%85%8D%EC%8A%A4%ED%8A%B8%20%ED%8C%8C%EC%9D%BC,%EC%8B%9C%EA%B7%B8%EB%84%90%20%28Signal%29%20...%206%206.%20%EC%86%8C%EC%BC%93%20%28Socket%29%20)

책:: 쉽게 배우는 운영체제 - 조성호