# [S3 CORS](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/cors.html)

## S3 CORS

* [CORS](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/99.%20AWS%20Terms/99-3.%20CORS)는 웹 브라우저가 한 출처(origin)에서 실행 중인 웹 애플리케이션이 다른 출처의 자원에 접근할 수 있도록 허용하는 메커니즘임. 
* **Amazon S3는 이를 지원하여, 다른 출처에서 S3 버킷의 객체에 접근할 수 있도록 설정**할 수 있음.
* **CORS정책**  
  * 서버가 클라이언트가 보낸 요청을 허용할지 여부를 결정하는 규칙 세트.  
  * S3 버킷의 소유자가 CORS 정책을 설정하여, **어떤 출처에서 어떤 메서드로 접근**할 수 있는지 정의함.

### 주요 헤더

* **Access-Control-Allow-Origin**  
허용할 출처를 명시함.
* **Access-Control-Allow-Methods**  
허용할 HTTP 메서드를 명시함.
* **Access-Control-Allow-Headers**  
허용할 요청 헤더를 명시함.
* **Access-Control-Allow-Credentials**  
자격 증명을 포함할 수 있는지 여부를 명시함.
* **Access-Control-Expose-Headers**  
클라이언트가 접근할 수 있는 응답 헤더를 명시함.
* **Access-Control-Max-Age**  
preflight 요청의 결과를 브라우저가 캐시할 시간을 초 단위로 명시함.

### CORS 설정 예시

* S3 콘솔을 통해 버킷의 CORS 정책을 설정할 수 있음.

  ```json
  [
    {
      "AllowedOrigins": ["*"],
      "AllowedMethods": ["GET", "POST"],
      "AllowedHeaders": ["*"],
      "ExposeHeaders": [],
      "MaxAgeSeconds": 3000
    }
  ]

  ```
  위 설정은 모든 출처에서 GET, POST 메서드로 요청할 수 있도록 허용하고, 모든 요청 헤더를 허용함.

## S3 CORS Architecture Example

* **웹 애플리케이션이 S3 버킷에 접근하는 시나리오**  
  * **클라이언트 (브라우저)**  
  예를 들어, `http://webapp-client.s3.amazonaws.com`에서 실행 중인 웹 애플리케이션.
  * **S3 버킷**  
  예를 들어, `http://example-bucket.s3.amazonaws.com`.

  1. **클라이언트에서 요청**  
    클라이언트 애플리케이션이 S3 버킷에 있는 자원에 접근하려고 할 때, CORS 정책에 따라 동작함.

      ```javascript
      fetch('http://example-bucket.s3.amazonaws.com/my-object', {
        method: 'GET',
        credentials: 'include' // 자격 증명을 포함하려면 설정
      })
      .then(response => response.json())
      .then(data => console.log(data))
      .catch(error => console.error('Error:', error));
      ```
  2. **CORS Preflight 요청 (OPTIONS)**  
    브라우저는 실제 요청 전에 OPTIONS 메서드를 사용하여 사전 요청을 보냄.

      ```http
      OPTIONS /my-object HTTP/1.1
      Host: example-bucket.s3.amazonaws.com
      Origin: http://webapp-client.s3.amazonaws.com
      Access-Control-Request-Method: GET
      Access-Control-Request-Headers: content-type
      ```

  3. **S3 버킷의 응답**  
    S3 버킷은 CORS 정책에 따라 응답함.

      ```http
      HTTP/1.1 200 OK
      Access-Control-Allow-Origin: http://webapp-client.s3.amazonaws.com
      Access-Control-Allow-Methods: GET, POST
      Access-Control-Allow-Headers: content-type
      Access-Control-Max-Age: 3000
      ```

  4. **실제 요청**  
    클라이언트가 실제 요청을 보냄.

      ```http
      GET /my-object HTTP/1.1
      Host: example-bucket.s3.amazonaws.com
      Origin: http://webapp-client.s3.amazonaws.com
      ```

  5. **S3 버킷의 응답**  
    S3 버킷은 요청을 처리하고 응답을 반환함.

      ```http
      HTTP/1.1 200 OK
      Access-Control-Allow-Origin: http://webapp-client.s3.amazonaws.com
      Content-Type: application/json
      ```


## Summary

* Amazon S3의 CORS 설정을 통해, **웹 애플리케이션이 다른 출처의 자원에 안전하게 접근할 수 있도록 허용**할 수 있음.  
* 이는 특히 클라이언트 애플리케이션이 S3 버킷의 자원에 접근해야 하는 경우 유용함.  
* 올바른 설정을 통해 보안과 유연성을 동시에 확보할 수 있음.

