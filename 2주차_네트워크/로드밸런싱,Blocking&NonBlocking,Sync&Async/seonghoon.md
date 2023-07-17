# 로드밸런싱, Blocking/Non-blocking & Synchronous/Asynchronous

## 로드밸런싱

- 네트워크 또는 서버에 가해지는 부하를 분산시키는 기술을 뜻함
- 로드 밸런서라는 장치는 서버들 또는 네트워크 허브 사이에 위치함
- round robin, random access 등등 여러 기법이 있음

## Blocking/Non-blocking & Synchronous/Asynchronous

### blocking/non-blocking은 제어권 관점

blocking은 호출한 함수가 호출 당한 함수에게 제어권을 넘겨주지만, non-blocking은 호출한 함수가 계속해서 제어권을 가지고 있는다.

### synchronous/asynchronous는 시간 관점

synchronous는 두 함수의 시작시간과 종료시간에 대해 순서가 맞춰져야 한다는 특징이 있고, 반면 asynchronous는 모든 순서가 완전히 보장될 필요가 없다.

![Untitled](source_seonghoon/Untitled%206.png)

일반적인 케이스는 (blocking + synchronous), (non-blocking + asynchronous) 가 함께 작동하는 경우이다.

이해하기 힘든 케이스는 non-blocking + synchronous), (blocking + asynchronous) 의 경우이다.

### Non-blocking + Synchronous

![https://blog.kakaocdn.net/dn/UfY6o/btq5AO095mD/ptMoKptCTDas7C0O8oCY2k/img.jpg](https://blog.kakaocdn.net/dn/UfY6o/btq5AO095mD/ptMoKptCTDas7C0O8oCY2k/img.jpg)

출처 : https://velog.io/@hotdari90/Async-Sync-Blocking-Non-Blocking

이처럼 제어권을 가진 함수가 계속해서 “너 끝났어?”를 물어본다. 호출된 함수가 완료되어야만 다른 작업을 수행한다.

### Blocking + Asynchronous

![https://blog.kakaocdn.net/dn/kJBBc/btq5uvWUR6Q/Jd2we9JAEwwiwqUIiPWwbK/img.jpg](https://blog.kakaocdn.net/dn/kJBBc/btq5uvWUR6Q/Jd2we9JAEwwiwqUIiPWwbK/img.jpg)

출처 : https://velog.io/@hotdari90/Async-Sync-Blocking-Non-Blocking

이처럼 제어권을 호출한 함수에게 넘겨주었으므로, 그 함수가 제어권을 넘겨줘야(callback 되어야) 다시 실행된다.

굳이 async라는 특성이 보이지 않으므로, 잘 쓰이지 않는 케이스라고 한다.

다만, 환경이 다른 두 프로그램을 혼합해서 사용하면서 겪게 되는 희귀한 경우가 있다고 한다. ex) MySQL + Node.js

### 참고사이트

[[CS지식] Non Bloking VS Asynchronous / 논블로킹 vs 비동기 (tistory.com)](https://programming119.tistory.com/238)