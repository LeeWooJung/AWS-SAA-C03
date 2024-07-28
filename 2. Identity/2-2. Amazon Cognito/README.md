# [Amazon Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)

## <img src = "https://github.com/user-attachments/assets/305c51dd-4986-4c60-90c0-e3fb57b6e714" width = "20" height = "20"> Cognito

Amazon Cognito는 **사용자의 인증, 권한 부여 및 사용자 관리 기능을 제공**하는 AWS의 서비스임.  

이 서비스를 통해 **웹 및 모바일 애플리케이션의 사용자 등록, 로그인, 접근 제어 등을 간편하게 관리**할 수 있음.


## 주요 기능 및 특징

### 사용자 풀(User Pools)

사용자 풀은 **애플리케이션의 사용자 디렉토리**로, 사용자를 등록하고 인증하는 데 사용됨.

API Gateway, ALB와 같이 쓰일 수 있음.

사용자 풀을 통해 **사용자가 직접 가입하고 로그인할 수 있으며, 소셜 아이덴티티 제공자(Google, Facebook, Amazon 등)를 통해 인증**할 수도 있음.

**다중 인식 인증(MFA), 사용자 계정 확인 및 복구, 사용자 속성 관리 등의 기능을 제공**함.

### 연합된 신원(Federated Identities, Identity Pools)

연합된 신원 기능을 통해 **사용자들이 소셜 아이덴티티 제공자 또는 SAML 기반의 기업 디렉토리를 통해 인증**할 수 있음.

이를 통해 **단일 사용자 ID로 여러 애플리케이션과 서비스에 접근**할 수 있도록 함.

연합된 신원 기능을 사용하면 Cognito는 사용자에게 **임시 보안 자격 증명을 제공하여 AWS 리소스에 안전하게 접근**할 수 있도록 함.

사용자 풀과 함께 쓰여서 identity provider 역할을 할 수 있음.

### 호스트된 UI 및 SDK

Cognito는 사전 구축된 사용자 인터페이스(UI)를 제공하여 **사용자 등록, 로그인, 비밀번호 복구 등의 기능을 쉽게 구현**할 수 있음.

또한, iOS, Android, JavaScript 등의 플랫폼에서 사용할 수 있는 SDK를 제공하여 **애플리케이션에 쉽게 통합**할 수 있음.

### 보안 및 규정 준수

사용자 풀은 **비밀번호 정책, MFA, 계정 확인 및 복구, 이상 탐지 등의 보안 기능을 제공**함.

사용자 데이터는 전송 중 및 저장 중 암호화되며, AWS Identity and Access Management(IAM)와 통합되어 세밀한 접근 제어를 지원함.

Amazon Cognito는 **GDPR, HIPAA 등 주요 규정 준수를 지원**함.

### 확장성 및 고가용성

Amazon Cognito는 AWS의 인프라를 기반으로 하여 **자동으로 확장되고 높은 가용성을 제공**함.

수백만 명의 사용자를 지원할 수 있으며, **트래픽 증가에 따라 자동으로 확장**됨.

### 커스터마이징 가능성

사용자 풀의 호스트된 UI를 커스터마이징하여 **브랜드에 맞는 사용자 경험을 제공**할 수 있음.

**Lambda 트리거를 사용하여 사용자 등록, 로그인, 토큰 생성 등의 이벤트에 대한 커스텀 로직을 추가**할 수 있음.

사용자 속성 및 그룹을 사용하여 세밀한 접근 제어를 설정할 수 있음.

### API 통합

Amazon Cognito는 **다양한 API를 통해 애플리케이션과 통합**할 수 있음.  

사용자 관리, 인증, 토큰 생성, 사용자 속성 업데이트 등의 작업을 API를 통해 수행할 수 있음.

**AWS AppSync, API Gateway 등과 연동하여 GraphQL 및 RESTful API와 통합**할 수 있음.

## Use case

### 웹 및 모바일 애플리케이션 사용자 관리

사용자 등록, 로그인, 비밀번호 복구 등의 기능을 간편하게 구현할 수 있음.

**소셜 로그인 및 연합된 신원을 통해 사용자 경험을 향상**시킬 수 있음.

### 보안 강화를 위한 MFA 및 이상 탐지

다중 인식 인증(MFA)을 통해 **추가적인 보안 계층**을 제공함.

**이상 탐지**를 통해 비정상적인 로그인 시도를 식별하고 대응할 수 있음.

### 기업 환경에서의 SSO(Single Sign-On)

SAML 기반의 **기업 디렉토리와 연동**하여 **단일 사용자 ID로 여러 애플리케이션에 접근**할 수 있도록 함.

연합된 신원을 통해 다양한 아이덴티티 제공자와 통합할 수 있음.

## User Pools Example

* **Use case**  
    웹 혹은 모바일 애플리케이션을 위한 **서버리스** 사용자 데이터베이스를 생성. 

* **인증 예시**  
    * Simple login: User name(or e-mail) / password combinations
    * Password reset
    * Email & Pthon Number Verification
    * Multi-factor authentication(MFA)
    * Fedrated Identities: users from Facebook, Google, SAML etc.

### Architecture Example

**With API Gateway**

![user pools architecture1](https://github.com/user-attachments/assets/216461d6-11f5-431b-8a73-621489a89010)

**With ALB**

![user pools architecture2](https://github.com/user-attachments/assets/52e17a39-01a9-48e4-b696-b507594eadb8)


## Identity Pools(Federated Identites) Example

User에 대한 Identities를 가져와서 AWS에 임시 증명하는 방법.

User의 Identity는 Cognito User Pools, 3rd party logins 등이 존재.

이를 이용하면 **API Gateway 혹은 직접** AWS Service에 접근할 수 있음.

### Architecture Example

**With 3rd party logins**

![Identity Provider architecture](https://github.com/user-attachments/assets/c508e8c7-7a1f-4f0e-a1a2-4f416e98ddfe)

## Summary 

Amazon Cognito는 **사용자 인증, 권한 부여, 사용자 관리 기능을 제공하여 애플리케이션의 보안과 사용자 경험을 향상시킬 수 있는 강력한 도구**임.  

이를 통해 개발자는 사용자 관리에 대한 부담을 줄이고 애플리케이션의 핵심 기능 개발에 집중할 수 있음.