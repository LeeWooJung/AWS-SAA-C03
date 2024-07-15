# Security

AWS API Gateway는 다양한 **보안 기능을 통해 API를 보호하고, 접근 제어를 관리하며, 데이터 무결성과 기밀성을 유지**할 수 있게 해줌.  

주요 보안 기능에는  **데이터 암호화**, **네트워크 보안**, **모니터링 및 로깅**, **인증 및 권한 부여**가 포함됨.

## 데이터 암호화

### 전송 중 암호화  

API Gateway는 **SSL/TLS를 사용하여 클라이언트와의 모든 데이터 전송을 암호화**함.  

이를 통해 데이터가 전송 중에 도청되거나 조작되는 것을 방지함.

### 저장 중 암호화  

API Gateway에서 **캐시된 데이터는 Amazon CloudFront를 통해 암호화**됨.  

CloudFront는 Amazon S3와 같은 다른 AWS 서비스와 연동되어 데이터 저장 시 암호화를 제공함.

## 네트워크 보안

### VPC Integration  

Private 엔드포인트를 사용하여 API를 VPC 내부에서만 접근 가능하게 설정할 수 있음.  

이를 통해 인터넷을 통한 접근을 차단하고, **VPC 내의 보안 그룹과 네트워크 ACL을 활용**할 수 있음.

### AWS WAF (Web Application Firewall)

**AWS WAF**를 통해 API Gateway에 대한 웹 공격을 방어할 수 있음.  

WAF를 사용하여 SQL 인젝션, 크로스 사이트 스크립팅(XSS) 등의 공격을 차단할 수 있음.

## 모니터링 및 로깅

### CloudWatch Logs  

API Gateway는 Amazon CloudWatch Logs와 통합되어 API 요청 및 응답 로그를 기록함. 

이를 통해 **API 호출 내역을 모니터링하고, 문제를 디버깅**하며, 보안 이벤트를 분석할 수 있음.

### CloudTrail  

AWS CloudTrail을 통해 **API Gateway의 관리 작업을 추적**할 수 있음.  

이를 통해 누가 언제 어떤 작업을 수행했는지에 대한 기록을 남길 수 있음.

### X-Ray  

AWS X-Ray를 사용하여 **API 요청의 추적과 분석을 수행**할 수 있음.  

이를 통해 API 호출의 성능과 오류를 분석하고 최적화할 수 있음.

## 인증 및 권한 부여

### IAM Policies  

AWS Identity and Access Management (IAM)를 사용하여 **API Gateway에 대한 액세스를 제어**할 수 있음.  

이를 통해 특정 IAM 사용자, 그룹 또는 역할에 대해 API에 대한 권한을 부여하거나 제한할 수 있음. 특히, 내부 애플리케이션에서 유용함.

### Lambda Authorizers  

**Lambda 함수를 사용하여 사용자 정의 인증 로직을 구현**할 수 있음.  

이는 토큰 기반 인증, **OAuth, OpenID Connect 등을 지원**함.

### Cognito User Pools  

Amazon Cognito를 사용하여 **사용자 인증을 관리**할 수 있음. 예를 들어, 외부 유저를 확인할 수 있음. 

Cognito User Pools를 통해 사용자 등록, 로그인 및 자격 증명 관리를 간편하게 처리할 수 있음.

### API Key  

API 키를 사용하여 API 요청을 인증할 수 있음. 

API 키는 주로 **사용량 추적 및 제한**을 위해 사용됨.

### Resource Policies  

API Gateway 리소스 정책을 사용하여 **특정 IP 주소, VPC 엔드포인트, 또는 AWS 계정에서의 접근을 제한**할 수 있음.

### With ACM

Custom Domain Name HTTPS에 대한 보안을 ACM과 통합하여 쉽게 할 수 있음.

* **강화된 보안**

    ACM을 통해 **SSL/TLS 인증서를 생성하고 관리**함으로써 API 트래픽이 암호화됨. 이는 전송 중 데이터의 무결성과 기밀성을 보장함.  

    **인증서 갱신이 자동**으로 이루어지므로 인증서 만료로 인한 보안 위협을 방지할 수 있음.

* **유연한 도메인 관리**

    커스텀 도메인 이름을 사용하여 **API 엔드포인트를 쉽게 식별하고 접근**할 수 있음. 이는 브랜드 일관성을 유지하고 API 사용자 경험을 향상시킴.

    여러 API를 하나의 커스텀 도메인 이름 아래에 배치하여 관리가 용이함.

* **통합 관리**

    ACM과 API Gateway 간의 통합을 통해 **인증서 관리가 간소화**됨. ACM에서 생성한 인증서를 API Gateway 콘솔에서 직접 선택하여 사용할 수 있음.

    **Route 53과의 통합을 통해 도메인 네임 시스템(DNS) 설정이 자동으로 관리**됨. **Alias 레코드, CNAME**을 사용하여 API Gateway 엔드포인트와 쉽게 연결할 수 있음.

* **높은 가용성**

    AWS의 글로벌 인프라를 통해 **높은 가용성**을 제공함. API Gateway와 ACM은 여러 AWS 리전에 걸쳐 분산되어 있어, 트래픽 증가나 장애 상황에서도 안정적으로 서비스를 제공할 수 있음.

    Route 53의 지리적 분산과 결합하여 도메인 네임 해석이 빠르고 안정적임.

* **쉽고 간편한 설정**

    AWS Management Console을 통해 직관적인 인터페이스로 쉽게 설정할 수 있음. **복잡한 인증서 설정 과정을 단순화**하여 빠르게 배포할 수 있음.

    개발자는 인프라 관리보다는 애플리케이션 개발에 더 많은 시간을 투자할 수 있음.

* **주의점**

    Edge-Optimized Endpoint를 사용할 때는 Certificate는 **us-east-1**에 존재해야 함.

    Regional Endpoint를 사용할 때는 Certificate는 사용하는 **API Gateway와 같은 Region에 존재**해야 함.

## Summary

AWS API Gateway는 다양한 보안 기능을 통해 API를 안전하게 보호하고, 접근을 제어하며, 데이터를 암호화하여 무결성과 기밀성을 유지함.  

이를 통해 개발자들은 보안에 대한 걱정 없이 API를 설계하고 배포할 수 있었음.