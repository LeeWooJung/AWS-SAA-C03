# [Hosted Zones](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/hosted-zones-working-with.html)

## Hosted Zones

### 설명

* Amazon Route 53에서 **Hosted Zone**은 도메인 이름과 관련된 모든 DNS 레코드를 관리하는 리소스를 의미.  
* Hosted Zone은 **도메인에 대한 DNS 설정을 정의하며, 도메인 이름을 IP 주소로 변환하는 역할**을 함.

### 기능

1. **DNS 레코드 관리**  
    * Hosted Zone은 도메인과 관련된 다양한 DNS 레코드를 포함.  
    * A 레코드, CNAME 레코드, MX 레코드, TXT 레코드, NS 레코드 등이 포함.
    * 각 레코드는 **도메인 이름과 IP 주소 간의 매핑을 정의하거나 이메일 서버, 서비스 등의 다른 도메인 리소스를 지정**.

2. **도메인 네임 공간 관리**  
    * Hosted Zone은 도메인의 네임스페이스를 정의.  
    * 예를 들어, "example.com" 도메인에 대한 Hosted Zone은 "www.example.com", "mail.example.com" 등 **하위 도메인에 대한 DNS 설정을 관리**.

3. **공용 및 사설 Hosted Zone**  
    * **Public Hosted Zone**  
    인터넷에서 **접근 가능한 도메인 이름에 대한 DNS 설정을 관리**. 예를 들어, 웹사이트를 호스팅하는 경우 Public Hosted Zone을 사용.
    * **Private Hosted Zone**  
    **Amazon VPC (Virtual Private Cloud) 내부에서만 접근 가능한 도메인 이름에 대한 DNS 설정을 관리**. 내부 애플리케이션 및 리소스를 위해 사용됨.

4. **DNS 쿼리 처리**  
    * Hosted Zone은 도메인에 대한 DNS 쿼리를 처리. Route 53 네임 서버는 도메인에 대한 쿼리를 수신하고, Hosted Zone에 정의된 레코드에 따라 응답함.

### 구성 요소

* **SOA 레코드**  
특정 도메인에 대한 기본 정보와 네임 서버의 권한을 정의.
* **NS 레코드**  
도메인의 권한 있는 **네임 서버를 지정**. 이러한 네임 서버는 도메인에 대한 DNS **쿼리를 처리**.
* **다양한 DNS 레코드**  
A, AAAA, CNAME, MX, TXT, SRV 등 여러 유형의 DNS 레코드를 포함하여 도메인의 네트워크 트래픽을 관리하고 서비스 연결을 설정함.

### 생성 예시

* Amazon Route 53 콘솔이나 API를 통해 Hosted Zone을 생성할 수 있음.  
* 예를 들어, "example.com" 도메인에 대한 **Public Hosted Zone**을 생성하면 다음과 같은 설정이 이루어짐.

    * **SOA 레코드**  
    도메인의 기본 정보를 포함.
    * **NS 레코드**  
    Route 53 네임 서버의 주소를 포함하여 도메인의 네임 서버를 정의.
    * **A 레코드**  
    "example.com"을 특정 IP 주소로 매핑.
    * **CNAME 레코드**  
    "www.example.com"을 "example.com"으로 매핑.

### 상호 작용

* **DNS 쿼리**  
클라이언트가 도메인에 대한 DNS 쿼리를 보내면, Route 53 네임 서버가 Hosted Zone에 정의된 레코드에 따라 응답.
* **레코드 업데이트**  
도메인 소유자는 Route 53 콘솔 또는 API를 통해 Hosted Zone에 새로운 레코드를 추가하거나 기존 레코드를 수정할 수 있음.
* **모니터링 및 로깅**  
Route 53은 DNS 쿼리 로그를 제공하여 도메인에 대한 트래픽을 모니터링하고 분석할 수 있도록 함.

### 요금
* 하나의 hosted zone 당 한 달에 0.50 달러를 지불.

## Public Hosted Zone Architecture

![public hosted zone](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/4547f7ff-2f21-41df-9ef2-8e73eec002cc)

## Private Hosted Zone Architecture

![private hosted zone](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/0a9021fa-816c-4a64-88b9-39ac338c017d)