# 운영체제란? + 운영체제의 역할 + 커널이란? + 시스템 콜이란?

## 운영체제란?

![Untitled](source_seonghoon/Untitled.png)

컴퓨터 시스템의 **하드웨어적인 자원과 소프트웨어적인 자원을 효율적으로 관리**함으로써 사용자가 컴퓨터를 편리하고, 효과적으로 사용할 수 있도록 환경을 제공하는 시스템 소프트웨어

## 운영체제의 목적

**처리 능력 향상, 사용 가능도 향상, 신뢰도 향상, 반환 시간 단축**

- 처리 능력 : 일정 시간 내에 시스템이 처리하는 일의 양
- 반환 시간 : 시스템에 작업을 의뢰한 시간부터 처리가 완료될 때까지 걸린 시간
- 사용 가능도 : 시스템을 사용할 필요가 있을 때 즉시 사용 가능한 정도
- 신뢰도 : 시스템이 주어진 문제를 정확하게 해결하는 정도

## 운영체제의 역할

- 프로세서, 기억장치, 입출력장치, 파일 및 정보 등의 자원을 관리
- 자원을 효율적으로 관리하기 위해 자원의 스케쥴링 기능을 제공
- 사용자와 시스템간의 편리한 인터페이스 제공
- 시스템의 각종 하드웨어와 네트워크를 관리 및 제어
- 데이터를 관리하고, 데이터 및 자원의 공유 기능 제공
- 시스템의 오류를 검사하고 복구
- 자원 보호 기능 제공
- 입출력에 대한 보조 기능 제공
- ~~가상 계산기 능력 제공 (예를 들어..?)~~

## 커널이란?

![Untitled](source_seonghoon/Untitled%201.png)

운영체제 중 **항상 메모리에 올라가 있는 운영체제의 핵심 부분**으로써 하드웨어와 응용 프로그램 사이에서 **인터페이스를 제공**하는 역할을 하며, **컴퓨터의 자원들을 관리**하는 역할을 함

### 가장 큰 목표

컴퓨터의 물리적 자원과 추상화 자원을 관리하는 것

### 커널이 수행하는 작업들

- Task (Process) Management : 물리적 자원인 CPU를 추상적 자원인 Task로 제공
- Memory Management : 물리적 자원인 메모리를 추상적 자원인 Page 또는 Segment로 제공
- File System : 물리적 자원인 디스크를 추상적 자원인 File로 제공
- Network Management : 물리적 자원인 네트워크 장치를 추상적 자원인 Socket으로 제공
- Device Driver Management : 각종 외부 장치에 대한 접근
- Interrupt handling : 인터럽트 핸들링
- I/O Communication : 입출력 통신 관리

![Untitled](source_seonghoon/Untitled%202.png)

커널의 구성요소들이 존재하는 **Kernel Space**가 있고, 그 위에는 사용자로 여겨지는 Process들이 존재하는 **User Space**가 존재한다.

**커널은 항상 컴퓨터 자원만을 바라보고 있기 때문**에, 사용자와의 상호작용은 지원하지 않는다.

이 Kernel Space와 User Space 사이에는 System Call Interface가 존재하는데, User Space의 Task(Process)들이 커널이 관리하는 자원에 접근해야할 필요가 있을 때, **System Call Interface를 통해 Kernel Space의 자원관리자에게 요청이 전달**된다.

### 결론적으로,

**커널**은 사용자가 시스템 콜을 통해 컴퓨터 자원을 사용할 수 있게 해주는 자원 관리

**시스템 콜**은 커널 모드의 기능을 사용자 모드가 사용가능하게 하는 것 (즉, 프로세스가 하드웨어에 직접 접근해서 필요한 기능을 사용할 수 있게 해주는 것)

### 참고

[CS-Study/OS/운영체제란.md at main · Songwonseok/CS-Study (github.com)](https://github.com/Songwonseok/CS-Study/blob/main/OS/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C%EB%9E%80.md)

[[OS] 커널(Kernel)이란 (tistory.com)](https://minkwon4.tistory.com/295)

[[Linux Kernel] 커널의 개념과 리눅스 커널의 구조 (tistory.com)](https://5equal0.tistory.com/entry/Linux-Kernel-%EC%BB%A4%EB%84%90%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%BB%A4%EB%84%90%EC%9D%98-%EA%B5%AC%EC%A1%B0)