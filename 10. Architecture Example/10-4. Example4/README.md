# Example 4

DDoS Resiliency를 위한 Architecture 소개.

![ddos resiliency architecture](https://github.com/user-attachments/assets/7e51f583-d85b-41a4-adc3-e45cdfb77255)


## Edge Location Mitigation

### CloudFront

> [Users] --> [WAF] --> [CloudFront]

Edge에서 Web Application Delivery가 이뤄짐.

SYN floods, UDP reflection 등과 같은 평범한 DDoS 공격을 CloudFront에서 보호함.

### Global Accelerator

> [Users] --> [Global Accelerator]

Edge로부터 Application에 접근할 수 있음.

**Shield**와 통합하여 DDoS Protection을 진행.

Backend가 CloudFront와 호환되지 않을 때 도움이 됨.

### Route53

> [Users] <--> [Route53]

Edge에서 Domain Name Resolution을 진행.

이는 DDos Protection Mechanism임.

## DDoS Mitigation을 위한 방법

### Infrastructure Layer Defense

> [Users] --> [AWS WAF] --> [CloudFront] --> [ELB]

> [Users] <--> [Route53]

많은 양의 Traffic이 EC2 Instance로 넘어가지 않도록 막는 방법.

위와 같이 Global Accelerator, Route53, CloudFront, Elastic Load Balancer를 사용함.

### Use Auto Scaling

> [Auto Scaling Group -- [EC2 instances] ]

DDoS 공격으로 Traffic이 갑자기 증가할 때 Auto Scaling으로 완화할 수 있음.

### Elastic Load Balancer

> [ELB] --> [Auto Scaling Group -- [EC2 Instances]]

Elastic Load Balancer를 사용하여 갑자기 증가하는 Traffic을 EC2 Instances로 분산하여 나눠줄 수 있음.

## Application Layer에서 방어

### Detect & filter malicious web requests

> [Users] --> [WAF] --> [CloudFront]

* **CloudFront**

    정적 콘텐츠를 캐시하고 Edge에서 이를 제공함으로서, 백엔드를 보호할 수 있음.

    특정 지역에서의 접근을 막을 수 있음.

* **WAF**

    CloudFront, ALB 위에서 Request를 Filtering 하고 막을 수 있음.

    Rate-based Rules를 이용하여 특정 bad user와 IPs를 자동으로 막을 수 있음.

    Manage rules를 이용하여 IP reputation 혹은 Anonymous IPs로부터의 공격을 막을 수 있음.

### Sheild Advanced

> [CloudFront] <--> [Shield]

> [WAF] <--> [Shield]

> [ELB] <--> [Shield]

Shield Advanced 에서의 Automatic application layer DDoS mitigation은 AWS WAF rules를 자동으로 생성 및 실행하여 **Layer 7**에서의 공격을 막아줌.

## Attack Surface Reduction

### Hide backend

> [CloudFront] --> [API Gateway]

> [CloudFront] --> [ELB]

CloudFront, API Gateway, ELB를 사용하여 Backend에 있는 EC2 Instances, Lambda 등을 숨김

### Security Groups & Network ACLs

Security Group과 NACL을 사용하여 Subnet 혹은 ENI Level에서 특정 IP로부터의 접근을 Filtering 함.

Elastic IP는 **AWS Sheild Advanced**에 의해 보호됨.

### Protecting API Endpoints

> [API Gateway]

EC2, Lambda 등에 대한 접근을 숨김.

Edge-Optimized Mode 혹은 CloudFront + Regional Mode를 사용함.

WAF와 결합하여 Burst Limit, Header Filtering 등을 할 수 있음.