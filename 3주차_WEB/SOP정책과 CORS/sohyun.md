# SOP / CORS

- SOP 정책이란? + CORS 란 무엇이고, 어떻게 해결?

### **SOP(Same-origin policy, 동일 출처 정책)**

- 자바스크립트 엔진 표준 스펙의 보안 규칙
- 하나의 출처에서 로드된 자원이
    - 호스트,프로토콜,포트번호 일치하지 않는 자원과 상호작용하지 못하도록
    - 요청 제한
    - 동일 출처에서만 접근 가능하도록 함
    
    ```
    URL : scheme/host/port
    
    두 URL의 Port(명시한 경우), Protocol, Host가 모두 같아야 Same Origin
    "scheme/host/port 튜플(tuple)" 혹은 그냥 "tuple"이라고 하기도 한다.
    
    ex ) https://naver.com:80
    https는 프로토콜, naver.com은 호스트명 80은 포트다.
    ```
    
- 모든 출처 허용하면 안되는 이유 ?
    
    ```
    https://bank.com 이라는 도메인 사이트가 있다 
    이 사이트의 api 주소는 https://bank.com/api이다. 
    사용자가 은행 사이트에서 로그인을 한 후 인증 토큰을 받았다. 
    
    그런데 사용자가 로그인한 상태에서 https://evil.com사이트에 접속하게 되면, 
    https://evil.com사이트에서 https://bank.com/api로 ajax 요청을 보낼 때 
    유저가 획득한 인증 토큰이 자동으로 첨부되어 사용자인척하면서 요청을 보낼 수 있게 된다.
    
    이렇게 자동으로 쿠키가 첨부되기 때문에 
    보안상의 이유로 브라우저는 HTTP 호출을 동일한 출처로 제한했다.
    ```
    
- 예외 사항
    - 비표준
    1. 신뢰할 수 있는 사이트 
        - 양쪽 도메인 모두가 높음 단계의 보안 수준 가지고 있다면
        - SOP 적용하지 않음
    2. 인터넷 익스플로어
        1. SOP에서 포트 포함하지 않음

**근데 지금은 클라이언트에서 도메인이 다른 서버에서 제공하는 API를 사용하는 일이 많아짐**

**→ 이전 만큼 동일한 도메인 간의 요청만을 할 수는 없어져서 CORS 등장**

### CORS **(Cross-Origin Resource Sharing, 교차 출처 리소스 공유)**

- 웹 어플리케이션은 자신의 출처와 동일한 리소스만 불러옴
- 만약 다른 출처의 리소스를 불러오고 싶다면 ?
    - 다른 출처에서의 올바른 COR 헤더를 포함한 응답을 반환해야함
        
        `타 도메인간 자원 호출을 차단할지 승인할지를 결정하는 것`
        
    
- CORS 기능
    - 한 도메인 또는 Origin의 웹 페이지가 다른 도메인 (도메인 간 요청)을 가진 리소스에 액세스 할 수 있게하는 보안 메커니즘
    - 웹 페이지상에서 자바스크립트 이용하여 **XHR(XMLHttpRequest)를 다른 도메인으로 발생시킬 수있도록 함**
    - 이를 통해 브라우저와 서버간 안전한 CORS(교차 출처 요청 + 리소스 공유) 진행
    
    ```
    XMLHttpRequest(XHR)은 AJAX 요청을 생성하는 JavaScript API
    XHR의 메서드로 브라우저와 서버간의 네트워크 요청을 전송 
    ```
    

- 어떻게 동작하는가 ?
    - simple request
        - 조건
            1. GET 요청, HEAD, POST 중의 한 가지 방식을 사용
            2. POST 방식일 경우 conte-type이 아래 셋 중 하나여야 한다.
                - application/x-www-form-unlencoded
                - multipart/form-data
                - text/plain
                - preflighted request
                
                [*https://sshkim.tistory.com/101*](https://sshkim.tistory.com/101)
                
        - 과정
            1. 요청을 보낸다.
            2. 브라우저는 Host와 같은 헤더를 추가하는 것 외에도 교차 출처 요청에 대해 Origin Request Header를 자동으로 추가한다.
            
            ```
            GET /products/ HTTP/1.1
            Host: api.domain.com
            Origin: https://www.domain.com
            ```
            
            1. 1. 서버에서 `Origin` 리퀘스트 헤더를 확인합니다. Origin 값이 허용되면, `Access-Control-Allow-Origin`요청 헤더 Origin 값으로 설정한다.
            
            ```
            Http/1.1 200 OK
            Access-Control-Allow-Origin: https://www.domain.com
            Content-Type: application/json
            ```
            
            1. 응답을 받은 브라우저는 Access-Control-Allow-Origin 헤더가 탭의 출처와 일치하는지 확인한다. ⇒ 승인 ⇒ 통과된다.
            
    - preflighted request
        - simple request와는 다른 유형의 CORS 요청
        - 브라우저에서 진짜 요청을 보내기 전에 미리 확인 요청을 보냄
        - 이 요청은 `OPTIONS` 메소드를 사용
        
        - 과정
            1. ajax 요청을 보낸다.
            
            ```
            OPTIONS /products/ HTTP/1.1
            Host:api.domain.com
            Origin:https://www.domain.com
            Access-Control-Request-Method: POST
            Access-Control-Request-Headers: Authorization, Content-Type
            
            ```
            
            1. 서버는 허용된 메소드 및 헤더를 지정하여 응답한다.
            
            ```
            HTTP/1.1 200 OK
            Access-Control-Allow-Origin:https://www.domain.com
            Access-Control-Allow-Method: GET, POST, OPTIONS, PUT
            Access-Control-Allow-Headers: Authorization, Content-Type
            Content-Type: application/json
            
            ```
            
            1. 헤더와 메소드가 통과되면, 브라우저는 원래 CORS 요청을 보낸다.
            
            ```
            POST /products/ HTTP/1.1
            Host:api.domain.com
            Authorization: token
            Content-Type: application/json
            Origin:https://www.domain.com
            ```
            
            1. 응답은 Access-Control-Allow-Origin 헤더에 올바른 출처가 있으므로 검사를 통과한다.
    
    [CORS의 기본 개념과 동작 방식(부제: Preflight 요청이란?)](https://velog.io/@wjdwl002/CORS의-기본-개념과-동작-방식부제-Preflight-요청이란)
    

- CORS 해결 ? (= CORS 이슈 해결)
    - CORS는 에러인가?
        - NO
        - 서로 다른 도메인간 리소스를 전달하는 방식을 제어하는 메커니즘
    - CORS 이슈
        - SOP에 의거해 다른 출처의 리소스를 이용하거나 상호작용 하지 못하도록 막았을 때 경고 발생
        - 이를 해결하기 위해 CORS를 사용해 접근을 허용하도록 설정

- CORS 이슈 해결 방법
    - 클라이언트에서 해결
        1. 동일 출처로 이동시킨다 → 말도 안되는 단순
        2. 웹 브라우저 실행 옵션이나 플러그인을 통한 SOP 회피
        3. jsonp 방식으로 json 데이터 가져오기
        
        ```
        jsonnp?
        클라이언트가 아닌 각기 다른 도메인에 상주하는 서버로부터 데이터를 요청하기 위해 사용
        SOP 정책이 적용되지않는 script 태그 이용하여 동작
        https://velog.io/@yesdoing/JSONP%EB%9E%80-jujowt4jy7
        ```
        
    - 서버에서 해결
        1. @CrossOrigin 어노테이션 사용하기 (스프링 어노테이션)
            1. spring mvc 가 지원하는 어노테이션
            2. `@RequestMapping` 주석에 지정된 Http 메소드에 최대 30분을 허용한다. 어노테이션에 속성 값을 넣어 기본 값을 대체할 수 있다.
            - `origins`
                - 허용된 출처, 이 값은 pre-flight 응답과 실제 응답 모두에 access-control-allow-origin헤더에 배치된다.
            - `allowedHeaders`
                - 실제 요청 중에 사용할 수 있는 요청 헤더 목록이다. pre-flight의 응답 헤더인 access-control-allow-header에 값이 사용된다.
            - `allowCredential`
                - 브라우저가 요청과 관련된 쿠키를 포함해야 되는지 여부를 결정한다.
                - 이 값이 true이면, pre-flight 응답에는 값이 true로 설정된 access-control-allow-credentials 헤더가 포함된다.
            
            ```
            @CrossOrigin(origin="*", allowedHeaders = "*")
            @Controller
            public class MainController {
            	@GetMapping(path = "/")
            	public String main(Model model) {
            		return "main";
            	}
            }
            ```
            
        2. CORSFilter 사용
            1. 웹 서버의 모든 리소스의 요청을 가로채서 Cross domain request인지 체크하여 실제 요청 페이지에 전달하기전에 적절한 CORS 정책과 해더들을 적용한다.
        3. 서버에서 Access-Control-allow-origin 헤더 추가
            1. 서버에서 모든 클라이언트에 요청에 대해
            2. cross-origin HTTP 요청을 허가하는 `Access-Control-Allow-Origin:` 헤더 추가
                
                ```
                Access-Control-Allow-Origin
                도메인 간 요청을 할 수 있는 권한이 부여된 도메인을 지정한다.
                Access-Control-Allow-Credentials
                도메인 간 요청에 credential 권한이 있는지 없는지 지정한다.
                Access-Control-Expose-Headers
                노출하기에 안전한 헤더를 나타낸다.
                Access-Control-Max-Age
                pre-flighted 요청이 얼마만큼의 시간동안 캐시되는지
                Access-Control-Allow-Methods
                리소스에 접근할 때 메소드가 허용되는지
                Access-Control-Allow-Headers
                어떤 헤더 필드 네임이 실제 요청에서 사용할 수 있는지 가리킨다.
                ```
                
            3. 단, 전체 호스트에 대한 요청 허용 이므로 보안에 취약
