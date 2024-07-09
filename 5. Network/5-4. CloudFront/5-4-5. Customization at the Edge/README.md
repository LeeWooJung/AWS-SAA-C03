# Customization At the Edge

Amazon CloudFront는 **사용자와 가까운 엣지 로케이션에서 콘텐츠를 제공하여 지연 시간을 최소화하고 성능을 최적화하는 CDN 서비스**임.  

이를 통해 글로벌 사용자에게 더 빠른 응답을 제공할 수 있으며, 엣지 로케이션에서 다양한 맞춤형 작업을 수행할 수 있음.

CloudFront에서 엣지에서의 커스터마이제이션(Customization at the Edge) 방법에는 **CloudFront Functions**와 **Lambda@Edge**가 있음.   

이 두 가지 방법은 다양한 HTTP 요청 및 응답 처리, 사용자 맞춤화, A/B 테스트, 데이터 변환 등에서 사용됨.

또한, **Fully Serverless이며, 사용한 만큼만 지불**하면 됨.

cf) **Edge Function**  
    CloudFront distributions에 삽입되는 작성된 코드를 의미.  
    Latency를 최소화하기 위해 사용자의 가까이에서 실행됨.


## CloudFront Functions

CloudFront Functions는 **CloudFront 엣지 로케이션에서 실행되는 경량 함수(JavaScript)**로, HTTP 요청과 응답을 빠르게 처리할 수 있음. 또한 CloudFront내에서 설정할 수 있음.

High-Scale, Latency-sensitve CDN 커스터마이제이션을 위함.

주로 간단한 요청/응답 변환 및 헤더 조작에 사용됨.

### 특징

* **빠른 실행 시간**: 밀리초 단위로 실행되어 지연 시간이 매우 적음.  

* **경량**: 복잡한 로직보다는 간단한 HTTP 요청/응답 처리를 위해 설계됨.  

* **다양한 트리거**: Viewer Request, Viewer Response 이벤트(두 이벤트를 변환하기 위해 사용됨)에서만 실행 가능.  
    * Viewer Request: CloudFront가 Viewer 요청을 받은 후를 의미.
    * Viewer Response: CloudFront가 Viewer의 응답을 받기 전을 의미.

### 사용 사례

**HTTP 헤더 수정**: 사용자 요청이나 응답에 따라 HTTP 헤더를 동적으로 수정.  

**URL 리디렉션**: 특정 조건에 따라 URL을 리디렉션.

**간단한 사용자 인증**: 간단한 인증 로직을 추가.

## Lambda@Edge

Lambda@Edge는 **CloudFront와 통합된 AWS Lambda의 확장 기능**으로, 엣지 로케이션에서 복잡한 로직을 실행할 수 있음.  

더 복잡하고 상태를 관리해야 하는 작업에 적합함.  

Node.js와 Python으로 작성됨. 또한, 1,000 개 정도의 요청을 1초안에 처리할 수 있음.

### 특징

* **복잡한 로직 처리**: 다양한 AWS 서비스와 연동하여 복잡한 로직을 구현할 수 있음.

* **상태 관리**: 쿠키나 세션 데이터를 이용한 상태 관리 가능.

* **다양한 트리거**: Viewer Request, Viewer Response, Origin Request, Origin Response 모든 이벤트에서 실행 가능.
    * Viewer Request: Viewer로 부터 요청을 CloudFront가 받은 후.
    * Origin Request: CloudFront가 요청을 origin server로 보내기 전.
    * Origin Response: CloudFront가 origin server에서 응답을 받은 후.
    * Viewer Response: Viewer에게 CloudFront가 응답을 보내기 전.

* **작성**: **US-EAST-1**에서만 작성 가능하며, 해당 function은 여러 지역으로 복제됨.

### Use case

**A/B 테스트**: 사용자 그룹에 따라 서로 다른 콘텐츠를 제공하여 A/B 테스트 수행.

**사용자 맞춤화**: 사용자 위치, 디바이스 유형, 브라우저 등 다양한 조건에 따라 맞춤형 콘텐츠 제공.

**데이터 변환**: 이미지나 비디오 콘텐츠를 실시간으로 변환하여 제공.

**실시간 데이터 분석**: 사용자 데이터를 실시간으로 분석하여 인사이트 도출.

## CludFront Function vs. Lambda@Edge

### 특징

|특징|CloudFront Functions|Lambda@Edge|  
|:---|:---:|:---:|  
|Runtime|JavaScript|Python, Node.js|
|처리 가능 요청 수|Millions of Requests/s|Thousands of Requests/s|
|복잡도|낮음(간단한 작업)|높음(복잡한 로직)|
|응답 시간|매우 빠름|비교적 느림|
|최대 실행 시간|< 1ms|5~10 secs|
|최대 메모리|2 MB|128MB ~ 10GB|
|트리거 이벤트|Viewer Request, Viewer Response|Viewer Request, Viewer Response, Origin Request, Origin Response|
|상태 관리|불가|가능|
|네트워크, 파일시스템 액세스|X|O|
|요금|Free Tier 가능, @Edge의 1/6|Free Tier 없음, request와 duration에 따라 다름|

### Use case

* **CloudFront Functions**

    * Cache Key normalization( < 1ms)
        * Transform request attributes(headers, cookies, query strings, etc) to create an optimal Cache key
    * Header manipulation
        * Insert/modify/delete HTTP headers in the request or response
    * URL rewrites or redirects
    * Request authentication & authorization
        * Create and validate user-generated tokens to allow/deny requests

* **Lambda@Edge**

    * Longer execution time(several ms)
    * Adjustable CPU or Memory
    * Code depends on 3rd libraries(AWS SDK to access other AWS services)
    * Network access to use external services for processing
    * File system access or access to the body of HTTP requests