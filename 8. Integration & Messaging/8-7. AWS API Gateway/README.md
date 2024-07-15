# [API Gateway](https://docs.aws.amazon.com/ko_kr/apigateway/latest/developerguide/welcome.html)

## <img src = "https://github.com/user-attachments/assets/a9d82fcf-097b-4f15-93f0-9dabd5cecbbc" width = "30" height = "30"> AWS API Gateway

AWS API Gateway는 개발자들이 **웹 애플리케이션, 백엔드 서비스, IoT 애플리케이션, 모바일 애플리케이션 등에 대한 API를 쉽게 생성, 배포 및 관리할 수 있도록 돕는 서비스**임.  

이를 통해 API 요청을 받아들이고, 요청에 따라 적절한 백엔드 서비스에 전달하며, 응답을 클라이언트에게 반환하는 역할을 함.

## 주요 기능 및 특징

### API 생성 및 배포

RESTful APIs 및 WebSocket APIs를 생성할 수 있음.

AWS 콘솔, CLI, SDK를 통해 **쉽게 API를 생성하고 배포**할 수 있음.

API versioning을 관리함(v1, v2, ...)

Swagger/OpenAPI 정의를 가져와 API를 설정할 수 있음.

### 트래픽 관리

다양한 엔드포인트 유형을 지원 (**Lambda 함수, HTTP 엔드포인트, AWS 서비스 등**).

트래픽을 효과적으로 관리하기 위해 **API 레이트 제한, 스로틀링, 쿼터 설정 가능**.

### 보안 및 인증

**[IAM](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/2.%20Identity%20and%20Access(IAM)) 역할 및 정책**을 통해 API 접근 권한을 제어할 수 있음.

**AWS Cognito**와 통합하여 사용자 인증 및 관리 가능.

**API 키, Lambda Authorizer, JWT**를 통한 인증 지원.

### 모니터링 및 로깅

**Amazon CloudWatch와 통합**되어 API 요청 및 응답을 모니터링하고 로깅할 수 있음.

API 사용량 및 성능에 대한 실시간 모니터링 가능.

X-Ray를 통한 API 호출 추적 및 디버깅 지원.

### 캐싱

API 응답 **캐싱을 통해 응답 시간을 단축**하고 백엔드 서비스의 부하를 줄일 수 있음.

캐시 만료 정책 설정 가능.

### 통합

**AWS Lambda, Step Functions, DynamoDB, S3 등 다양한 AWS 서비스와 통합 가능**.  
AWS Lambda와 API Gateway를 통합하면 관리할 인프라가 없어 개발에 집중할 수 있음.

외부 HTTP 엔드포인트 및 VPC 링크를 통해 온프레미스 리소스와도 통합 가능.

### 개발 및 테스트

API Gateway 콘솔에서 직접 API를 테스트할 수 있는 기능 제공.

**스테이지**를 사용하여 **개발, 테스트, 프로덕션 환경**을 쉽게 관리할 수 있음.

## 아키텍처

### 클라이언트  

모바일 앱, 웹 앱, IoT 디바이스 등 다양한 클라이언트가 API Gateway를 통해 요청을 보냄.

### API Gateway  

클라이언트의 요청을 받아들이고, **인증 및 권한을 확인하며, 라우팅 규칙에 따라 백엔드 서비스로 요청을 전달**함.

### 백엔드 서비스  

AWS Lambda, EC2, ECS, Fargate, DynamoDB, S3 등 다양한 백엔드 서비스가 API 요청을 처리함.

### 모니터링 및 로깅  

CloudWatch와 X-Ray를 통해 API 호출을 모니터링하고, 성능 및 오류를 분석함.

## 장점

### 확장성  

API Gateway는 **자동으로 트래픽을 처리할 수 있는 확장성**을 제공함.

### 보안  

다양한 인증 및 권한 부여 방법을 통해 API 보안을 강화할 수 있음.

### 비용 효율성  

**사용한 만큼 지불하는 요금제로, 초기 비용 없이 API를 쉽게 생성하고 관리**할 수 있음.

### 유연성  

다양한 **AWS 서비스 및 외부 엔드포인트와의 통합**을 지원하여 유연한 아키텍처를 구성할 수 있음.

## 단점

### 복잡성  

다양한 기능과 설정 옵션으로 인해 초기 설정이 다소 복잡할 수 있음.

### 비용  

트래픽이 많은 경우 비용이 증가할 수 있음.

## Integrations

### Lambda Function

AWS Lambda 뒤에 REST API를 쉽게 노출시킬 수 있는 방법임.

* **설정**  
    API Gateway 콘솔에서 새로운 API를 생성하고, 리소스 및 메서드를 정의함.

* **Lambda Integration 선택**  
    통합 유형으로 Lambda를 선택하고, 호출할 Lambda 함수와 연결함.

* **IAM 역할 설정**  
    API Gateway가 Lambda 함수를 호출할 수 있도록 적절한 IAM 역할을 부여함.

* **배포**  
    API를 배포하고, 생성된 엔드포인트를 통해 Lambda 함수를 호출할 수 있음.

### HTTP

Backend에서 HTTP를 노출시킬 수 있는 방법임.  
이 방법을 통해서 rate limiting, caching, user authentications, API Keys 등의 방법을 사용할 수 있음.

* **설정**  
    API Gateway 콘솔에서 새로운 API를 생성하고, 리소스 및 메서드를 정의함.

* **HTTP Integration 선택**  
    통합 유형으로 HTTP를 선택하고, 호출할 외부 HTTP 엔드포인트를 설정함.

* **리퀘스트 및 리스폰스 매핑**  
    요청 및 응답 데이터를 외부 HTTP 서비스와 호환되도록 매핑함.

* **배포**  
    API를 배포하고, 생성된 엔드포인트를 통해 외부 HTTP 서비스를 호출할 수 있음.

* **예시**  
    internal HTTP API on premise,  
    Application Load Balancer

### AWS Service

다양한 AWS Service를 API Gateway를 통해서 노출시킬 수 있는 방법임.  
이 방법을 통해 authentication, deploy publicly, rate control 등을 수행할 수 있음.

* **설정**  
    API Gateway 콘솔에서 새로운 API를 생성하고, 리소스 및 메서드를 정의함.

* **AWS Service Integration 선택**  
    통합 유형으로 AWS Service를 선택하고, 호출할 AWS 서비스와 연결함 (예: DynamoDB, S3).

* **IAM 역할 설정**  
    API Gateway가 해당 AWS 서비스를 호출할 수 있도록 적절한 IAM 역할을 부여함.

* **배포**  
    API를 배포하고, 생성된 엔드포인트를 통해 AWS 서비스를 호출할 수 있음.

* **예시**  
    start an AWS Step Function workflow,  
    post a message to SQS.

* **Architecture Example**

    with Kinesis data streams example

    ![integration aws service architecture](https://github.com/user-attachments/assets/d1cb5d5c-8020-4915-98e7-0463d547f864)


## Summary

AWS API Gateway는 API 생성, 배포, 관리, 보안, 모니터링 등 다양한 기능을 제공하여, 개발자들이 복잡한 백엔드 작업을 단순화하고, 신뢰성 높은 API를 빠르게 개발할 수 있도록 지원하는 서비스임.