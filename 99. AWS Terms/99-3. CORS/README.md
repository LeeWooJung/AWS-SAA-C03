# CORS

## Cross-Origin Resource Sharing

* **CORS**는 웹 브라우저가 한 출처(origin)에서 실행 중인 웹 애플리케이션이 **다른 출처의 자원에 접근할 수 있도록 허용**하는 메커니즘.  
* 출처는 프로토콜, 도메인, 포트 번호로 구성됨. 예를 들어, http://example.com과 https://example.com은 서로 다른 출처로 간주됨.

### CORS의 필요성

* 웹 애플리케이션이 보안상의 이유로 동일 출처 정책(Same-Origin Policy)을 따름.  
* 동일 출처 정책은 한 출처에서 로드된 문서나 스크립트가 다른 출처의 자원에 접근하지 못하도록 제한함.  
* 하지만 실제 애플리케이션 개발 시, **다른 출처의 API나 자원에 접근해야 하는 경우가 많음**.  
* 이때 CORS를 사용하여 이러한 제한을 완화할 수 있음.

### 작동 방식

* CORS는 서버와 클라이언트 간의 **HTTP 헤더**를 사용하여 작동함.  
* 클라이언트가 다른 출처의 자원에 접근하려고 할 때, 서버는 특정 HTTP 헤더를 통해 이 요청을 허용할지 여부를 결정.

### 주요 헤더

* **Request Headers** (클라이언트 -> 서버)  
    * **Origin**  
    요청을 보낸 출처를 나타냄.
    * **Access-Control-Request-Method**  
    실제 요청에서 사용할 HTTP 메서드를 나타냄 (preflight 요청 시).
    * **Access-Control-Request-Headers**  
    실제 요청에서 사용할 헤더들을 나타냄 (preflight 요청 시).

* **Response Headers** (서버 -> 클라이언트)  
    * **Access-Control-Allow-Origin**  
    요청을 허용할 출처를 지정함.  
    예: * (모든 출처 허용) 또는 특정 도메인 (http://example.com).
    * **Access-Control-Allow-Methods**  
    허용할 HTTP 메서드를 지정함.  
    예: GET, POST, PUT, DELETE.
    * **Access-Control-Allow-Headers**  
    허용할 요청 헤더를 지정함.
    * **Access-Control-Allow-Credentials**   
    자격 증명(쿠키, HTTP 인증)을 포함할지 여부를 지정함.
    * **Access-Control-Expose-Headers**  
    클라이언트가 접근할 수 있는 응답 헤더를 지정함.
    * **Access-Control-Max-Age**  
    preflight 요청의 결과를 브라우저가 캐시할 시간을 초 단위로 지정함.

### CORS 요청 종류

* **Simple Requests** (단순 요청)  
    * GET, POST, HEAD 메서드 중 하나를 사용.
    * 요청 헤더가 Accept, Accept-Language, Content-Language, Content-Type 중 하나를 포함.
    * Content-Type이 application/x-www-form-urlencoded, multipart/form-data, text/plain 중 하나일 때.
    * 서버는 **Access-Control-Allow-Origin** 헤더를 통해 요청을 허용할지 여부를 응답함.

* **Preflight Requests** (사전 요청)  
    * 클라이언트가 실제 요청을 보내기 전에 **OPTIONS 메서드**를 사용하여 서버에 허가를 요청함.
    * 서버는 Access-Control-Allow-Methods, Access-Control-Allow-Headers 등을 포함한 응답을 보냄.
    * 클라이언트는 응답을 확인하고 실제 요청을 보낼지 결정함.

* **Credentialed Requests** (자격 증명 요청)  
    * 자격 증명(쿠키, HTTP 인증 정보)을 포함하는 요청.
    * 서버는 Access-Control-Allow-Credentials를 true로 설정하여 자격 증명을 허용함.
    * Access-Control-Allow-Origin이 *일 경우, 자격 증명을 포함할 수 없음.

### 서버 응답 헤더 예시
```javascript
app.use((req, res, next) => {
  res.header("Access-Control-Allow-Origin", "http://example.com"); // 허용할 출처
  res.header("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE"); // 허용할 메서드
  res.header("Access-Control-Allow-Headers", "Content-Type"); // 허용할 헤더
  res.header("Access-Control-Allow-Credentials", "true"); // 자격 증명 허용
  next();
});
```

### 장점

* **보안 유지**  
동일 출처 정책을 유지하면서도 필요한 경우 다른 출처의 자원에 접근 가능.
* **유연성**  
서버 측 설정을 통해 특정 출처에만 자원 접근을 허용 가능.

### 단점

* **설정 복잡성**  
다양한 옵션과 헤더 설정으로 인해 복잡할 수 있음.
* **브라우저 지원**  
CORS는 주로 최신 브라우저에서 지원됨. 구형 브라우저에서는 제대로 동작하지 않을 수 있음.