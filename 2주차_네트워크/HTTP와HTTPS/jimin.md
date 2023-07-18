# HTTP & HTTPS

## HTTP & HTTPS

---

### HTTP (HyperText Transfer Protocol)

- 암호화 과정 X
- 패킷 가로채기/수정이 가능
- 보안에 취약

### HTTPS (HyperText Transfer Protocol Secure)

- 암호화 과정 ⇒ 패킷 암호화
- `SSL(Secure Socket Layer)` 을 활용
    - SSL 이란? ⇒ 인터넷을 통해 전달되는 정보를 보호하기 위해 개발한 통신 규약
    - http 는 본래 tcp 와 직접 통신했지만, https 에서 http 는 ssl 과 통신하고 ssl 이 tcp 와 통신
- 보안에 강함

### 모든 사이트를 https 로 하지 않는 이유는?

- 암호화 과정으로 인한 속도 저하 때문