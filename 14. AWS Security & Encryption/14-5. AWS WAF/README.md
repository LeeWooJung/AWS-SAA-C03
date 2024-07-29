# [AWS WAF](https://docs.aws.amazon.com/ko_kr/waf/latest/developerguide/waf-chapter.html)

## <img src = "https://github.com/user-attachments/assets/f2e5999a-0551-4c27-a57a-abedf5f6b694" width = "25" height = "25"> AWS Web Application Fire

AWS WAF는 **웹 애플리케이션을 다양한 인터넷 위협으로부터 보호하는 웹 애플리케이션 방화벽 서비스**(Layer 7, HTTP)임. 

이를 통해 **웹 트래픽을 모니터링하고, 지정된 보안 규칙을 적용하여 공격을 차단**할 수 있음.

## 주요 특징

### 관리형 규칙 (Managed Rules)

AWS WAF는 공통 웹 취약점 (예: OWASP Top 10)에 대해 **사전에 정의된 규칙 세트를 제공**함.

### 사용자 정의 규칙 (Custom Rules)

특정 요구사항에 맞춰 사용자 정의 규칙을 생성할 수 있음.

### 실시간 가시성

웹 요청에 대한 **실시간 가시성을 제공하여, 보안 위협을 신속히 감지하고 대응**할 수 있음.

### IP 블록/허용 목록

특정 IP 주소를 블록하거나 허용할 수 있는 기능을 제공함.

### 호환성

**Amazon CloudFront, Application Load Balancer(ALB), API Gateway, AppSync GraphQL API, Cognito User Pool** 등 다양한 AWS 서비스와 통합 가능함.

## 구성 요소

* **웹 ACL** (Web Access Control List)

    트래픽에 적용할 규칙의 집합을 정의함.

    CloudFront를 제외한 다른 곳에서 **ACL은 Regional** 서비스임.

* **규칙** (Rules)

    특정 조건을 기반으로 트래픽을 허용, 차단, 또는 모니터링함. 

    * **IP Set**
        
        10,000 개의 IP 주소에 대한 규칙을 정의할 수 있음. 

        더 많은 IP 주소에 대한 규칙을 정의하고 싶으면 Multiple Rules를 사용해야 함.

    * 일반적인 Attack에 존재하는 **HTTP headers, HTTP body, URI strings** 등을 방지할 수 있는 규칙. 이는 **SQL 인젝션**, **Cross-site Scripting(XSS)** 등을 방지함.

    * Country를 막기 위해, Size constraints, **geo-match** 규칙이 있음.

    * **DDoS**를 막기 위해 Rate-based rules(to count occurrences of events)가 있음.

* **규칙 그룹** (Rule Groups)

    **여러 규칙을 그룹으로 관리**할 수 있음. 
    
    AWS Managed Rules 또는 사용자 정의 규칙 그룹을 포함할 수 있음.

    Web ACL에 추가하기 위해 규칙 그룹을 **재사용**할 수 있음.

* **조건** (Conditions)

    규칙에서 사용하는 조건으로, **IP 주소, HTTP 헤더, URI 문자열, SQL 코드** 등을 포함함.

## 아키텍처

AWS WAF는 **트래픽이 웹 애플리케이션에 도달하기 전에 규칙을 적용하여 보호**함. 

### 트래픽 수신

트래픽이 CloudFront, ALB, 또는 API Gateway에 도달함.

### 규칙 적용

웹 **ACL에서 정의된 규칙을 순차적으로 평가**함.

### 조치 수행

규칙에 따라 트래픽을 허용, 차단, 또는 모니터링함.

## Fixed IP with Load Balancer

WAF는 **Network Load Balancer**를 지원하지 않음. [Network Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-3.%20Network%20Load%20Balancer)는 Layer 4에서 작동하기 때문.

Fixed IP에 WAF를 적용하기 위해서는 [Global Accelerator](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-5.%20Global%20Accelerator)를 사용하고 WAF를 [ALB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-2.%20Application%20Load%20Balancer)와 연결해야 함.

### Architecture Example

![fixed ip architecture](https://github.com/user-attachments/assets/6cc62c00-5bed-41d2-a4ba-12e2c27826f6)


## 장점

* **확장성**

    AWS의 인프라를 활용하여 높은 확장성을 제공함.

* **관리형 규칙**

    AWS와 파트너사가 제공하는 관리형 규칙을 통해 빠르고 간편하게 보호할 수 있음.

* **통합성**

    AWS의 다른 서비스와 원활하게 통합됨.

* **실시간 모니터링**

    **실시간으로 트래픽을 모니터링하고 분석**할 수 있음.

## 단점

* **복잡성**

    복잡한 규칙 세트를 구성하는 데 시간이 걸릴 수 있음.

* **비용**

    사용량과 규칙 수에 따라 비용이 발생함.

## Use case

* **DDoS 보호**

    IP 블록/허용 목록을 사용하여 **DDoS 공격을 완화**함.

* **OWASP Top 10 보호**

    **SQL 인젝션, XSS 등 공통 웹 취약점으로부터 애플리케이션을 보호**함.

* **API 보호**

    API Gateway와 통합하여 API 요청을 필터링하고 보호함.

* **컴플라이언스**

    **보안 규정을 준수하기 위한 필수 보호 계층**으로 사용됨.

## Summary

AWS WAF는 웹 애플리케이션을 인터넷 위협으로부터 보호하는 강력한 **방화벽 서비스**임. 

관리형 규칙과 사용자 정의 규칙을 통해 유연하게 설정할 수 있으며, **다양한 AWS 서비스와 통합하여 웹 트래픽을 실시간으로 모니터링하고 보호**할 수 있음. 

**높은 확장성과 실시간 가시성을 제공**하여, 다양한 보안 요구사항을 충족할 수 있음.