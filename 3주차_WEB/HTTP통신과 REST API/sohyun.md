# HTTP 통신 / REST API

HTTP 통신(Request Methods, status code…) + REST API란?

### ****HTTP Request Methods****

- 클라이언트가 웹서버에게 요청하는 목적 및 그 종류를 알리는 수단

1. **GET**
    - 리소스(데이터)를 받기 위함
    - URL(URI) 형식으로 서버 측에 리소스를 요청한다.
2. **HEAD**
    - 메세지 헤더 정보를 받기 위함
    - GET과 유사하지만,
        - HEAD는 실제 문서 요청이 아닌 문서에 대한 정보 요청이다.
        - 즉, Response 메세지를 받았을 때, Body는 비어있고, Header 정보만 들어있다.
3. **POST**
    - 내용 및 파일 전송을 하기 위함
    - 클라이언트에서 서버로 어떤 정보를 제출하기 위해 사용한다.
    - Request 데이터를 HTTP Body에 담아 웹 서버로 전송한다.
4. **PUT**
    - 리소스(데이터)를 갱신하기 위함
    - POST와 유사하나, 기존 데이터를 갱신할 때 사용한다.
5. **DELETE**
    - 리소스(데이터)를 삭제하기 위함
    - 웹 서버측에 요청한 리소스를 삭제할 때 사용한다.
    - 실제로 클라이언트에서 서버 자원을 삭제하도록 하진 않아 비활성화로 구성한다.
6. **CONNECT**
    - 클라이언트와 서버 사이의 중간 경유를 위함
    - 보통 Proxy를 통해 SSL 통신을 하고자할 때 사용한다.
    
    ```
    Proxy ?
    "대리"의 의미
    클라이언트와 Web서버의 중간에 위치하고 있어, 대신 통신을 받아 주는 것이 프록시 서버
    ```
    
7. **OPTIONS**
    - 서버 측 제공 메소드에 대한 질의를 하기 위함
    - 웹 서버 측에서 지원하고 있는 메소드가 무엇인지 알기 위해 사용한다.
8. **TRACE**
    - Request 리소스가 수신되는 경로를 보기 위함
    - 웹 서버로부터 받은 내용을 확인하기 위해 loop-back 테스트를 할 때 사용한다.
9. **PATCH**
    - 리소스(데이터)의 일부분만 갱신하기 위함
    - PUT과 유사하나, 모든 데이터를 갱신하는 것이 아닌 리소스의 일부분만 수정할 때 쓰인다.
    

### ****HTTP status code****

- 링크 참고
    
    [https://gyoogle.dev/blog/web-knowledge/HTTP status code.html](https://gyoogle.dev/blog/web-knowledge/HTTP%20status%20code.html)
    

### REST API ?

- REST를 기반으로 만들어진 API

- ****REST (Representational State Transfer)****
- 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든 것
    - method
        - GET / POST /PUT /DELETE ~~(/PATCH 등?)~~
    - Resource 자원
        - http://myweb/users와 같은 URI
        - 모든 것을 Resource (명사)로 표현하고, 세부 Resource에는 id를 붙임
    - message
        - 메시지 포맷이 존재
        - 형태 : JSON , XML 등
    - 방식 예
    
    ```
    HTTP POST, http://myweb/users/
    {
    	"users" : {
    		"name" : "terry"
    	}
    }
    ```
    
- (정리) REST API 란 ?
    - HTTP URL을 통해 자원을 명시하고 HTTP Method를 활용하여 해당 URL에 대해 CRUD 적용

### **REST의 특징**

1. Server-Client(서버-클라이언트 구조)
    1. 자원이 있는 서버와 자원을 요청하는 클라이언트로 구성 / 둘은 서로 상호작용
    2. 클라이언트와 서버가 나누어져 있으므로 독립적 진화 가능
    
2. Stateless(무상태)
    1. session과 같은 저장소에 상태 정보 저장 안함
    2. request 만 메세지로 처리 → 구현 단순
    
3. Cacheable (캐시 처리 가능)
    1. 요청에 대한 서버의 응답에 데이터가 캐시 가능한지 불가능한지 여부가 명시되어 있게
    - 보통 HTTP Header에 **cache-control** 헤더를 이용한다
    
4. Layered System (계층화)
    1. 서버는 계층화된 시스템 아키텍처를 사용
        1. 자원의 representation을 요청하는 클라이언트와 응답을 보내는 서버 사이에 중간 단계로 보안 계층, 캐싱 계층 등 여러 서버 계층이 있는 형태.
        2. 구조상 유연성 줄 수 있음
        3. PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 된다.
    2. 단 , 클라이언트는 일반적으로 최종 서버에 연결되어 있는지 중간에 연결되어 있는지 알 수 없는 상태이다. ⇒ 클라이언트는 REST API 서버만 호출
    
5. Uniform Interface(인터페이스 일관성)
    1. 자원에 대한 요청 통일하고 한정적인 인터페이스로 수행
    2. 컴포넌트 인터페이스에 일반성의 원칙을 적용 → 단순화 / 상호작용의 가시성 향상
    
    ```
    일반성의 원칙 ? 
    이미 만들어진 것에 대해 생각할 필요 없이, 단지 재사용하기만 하면 된다는 원칙
    ```
    
    c. HTTP 표준에만 따른다면 모든 플랫폼에 사용이 가능
    
    - 요청하는 클라이언트가 어떤 플랫폼인지상관없이, 특정 언어나 기술에 종속받지 않는 특징을 의미한다
    

### rest 장점 ?

`면접관이 물어본다면 가장 좋을 것 같은 답변`

- 보기 좋다
    - URL만 보고 어떤 자원에 접근할 것인지, 메소드를 보고 어떤 행위를 할지 알 수 있기 때문에, 개발을 할때 용이
- 자원을 아낄 수 있다.
    - 1개의 URI로 4개의 행위(CRUD)를 명시할 수 있기 때문에, 굉장히 효율적입니다.
- stateless한 상태를 유지할 수 있다.
    - REST API의 가장 큰 특징으로, 다양한 브라우저와 모바일에서 통신할 수 있도록 합니다.
    - 클라이언트가 서버에 종속적이지 않아도 되기때문에, scale out한 상황에서도 용이합니다.

### rest 단점 ?

- method 형태가 제한적
- 표준이 없으니 딱히 정의가 없음

### REST API

- REST API란 REST의 원리를 따르는 API를 의미합니다.
- 설계 규칙을 지켜 작성하면 됨
- 설계 규칙
    
    ### **REST API 설계 예시**
    
    **1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.**
    
    > Bad Example http://khj93.com/Running/Good Example  http://khj93.com/run/
    > 
    
    **2. 마지막에 슬래시 (/)를 포함하지 않는다.**
    
    > Bad Example http://khj93.com/test/  Good Example  http://khj93.com/test
    > 
    
    **3. 언더바 대신 하이폰을 사용한다.**
    
    > Bad Example http://khj93.com/test_blogGood Example  http://khj93.com/test-blog
    > 
    
    **4. 파일확장자는 URI에 포함하지 않는다.**
    
    > Bad Example http://khj93.com/photo.jpg  Good Example  http://khj93.com/photo
    > 
    
    **5. 행위를 포함하지 않는다.**
    
    > Bad Example http://khj93.com/delete-post/1  Good Example  http://khj93.com/post/1
    > 

### RESTFUL

- rest의 원리따르는 시스템
- REST의 원리를 사용 + REST API 설계 규칙을 올바르게 지킨 시스템
- ⇒ RESTFUL

```
CRUD 기능을 POST로 처리하는 데 API 혹은 URL 규칙을 올바르게 지키지 않았다면 

REST API 를 사용하였지만 RESTFUL 하지 못하
```

면접 질문 답변 스타일로 정리

- RESTFUL API 란 뭔가요?
    - **웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일**

[https://khj93.tistory.com/entry/네트워크-REST-API란-REST-RESTful이란](https://khj93.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-REST-API%EB%9E%80-REST-RESTful%EC%9D%B4%EB%9E%80)
