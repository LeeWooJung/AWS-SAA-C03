# [AWS IAM Identity Center](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)

## <img src = "https://github.com/user-attachments/assets/50836b32-b35e-472b-a21e-2b86a00331a9" width = "20" height = "20"> Identity Center

AWS Identity Center(**AWS Single Sign-On**)는 AWS에서 **사용자와 그룹을 중앙에서 관리하고, 사용자가 다양한 AWS 계정 및 애플리케이션에 한 번의 로그인(SSO)을 통해 접근할 수 있도록 하는 서비스**임. 

이를 통해 보안과 편의성을 동시에 제공함.

## 특징

### 통합 인증

사용자는 **하나의 로그인 자격 증명을 통해 여러 AWS 계정 및 애플리케이션에 접근**할 수 있음.

### 사용자 및 그룹 관리

AWS 관리 콘솔에서 사용자 및 그룹을 쉽게 생성하고 관리할 수 있음.

### 다중 계정 관리

**여러 AWS 계정을 중앙에서 관리하고, 사용자에게 각 계정에 대한 접근 권한을 할당**할 수 있음.

### 애플리케이션 통합

AWS 애플리케이션 외에도 다양한 **SAML 2.0 지원 애플리케이션**과 통합할 수 있음.

### 규정 준수

중앙 집중식 인증 및 접근 제어를 통해 규정 준수 요구 사항을 충족할 수 있음.

## 구성요소

* **사용자 및 그룹**

    AWS Identity Center에서 사용자와 그룹을 생성하고 관리할 수 있음.

* **SSO 포털**

    사용자가 로그인하여 다양한 AWS 계정 및 애플리케이션에 접근할 수 있는 포털.

* **정책 및 권한**

    **IAM 역할과 정책**을 사용하여 사용자 및 그룹의 접근 권한을 정의함.

* **디렉토리 통합**

    **Microsoft Active Directory와 같은 온프레미스 디렉토리 서비스와 통합 가능**함.

* **Identity Providers**

    IAM Identity Center에 설치되어 있는 Identity Store.

    3rd Party로 **Active Directory**(AD), OneLogin, Okta 등이 있음.

## 아키텍처

AWS Identity Center는 **AWS 계정, 애플리케이션, 디렉토리 서비스와 통합**되어 작동함. 

중앙 관리 콘솔을 통해 사용자 및 그룹을 생성하고, SSO 포털을 통해 다양한 서비스에 접근할 수 있음.

### Architecture Example

![architecture](https://github.com/user-attachments/assets/388f8616-b49b-4414-ae96-8418eccded08)

## Fine-grained Permissions & Assignments

Fine-grained Permissions & Assignments는 **AWS IAM Identity Center**(AWS Single Sign-On)에서 제공하는 기능으로, **사용자의 세부적인 권한을 제어하고, 특정 자원에 대해 세밀한 접근 권한을 부여하는 것**을 의미함. 

이를 통해 **사용자에게 필요한 최소한의 권한만 부여할 수 있으며, 보안 및 관리 효율성을 높일 수 있음**.

### Multi-Account Permissions

AWS Organization에 속한 AWS Account 간의 접근을 제어함.

**Permission Sets**: AWS 서비스에 대한 접근을 정의하기 위해 User 혹은 Group에 할당된 하나 혹은 여러 개의 IAM Policies 집합.

### Application Assignments

많은 **SAML 2.0** business 애플리케이션에 SSO로 접근하는 방법.

Required URLs, Certificates, Metadata를 제공함.

### Attribute-Based Access Control(ABAC)

IAM Identity Center Identity Store에 저장된 **사용자의 특징**(Cost center, title, locale 등)에 기반하여 세분화된 접근 권한을 제공함.

딱 한 번 접근을 허용하고, 사용자의 특성을 바꾸어 그 후에는 접근이 불가능하도록 할 수 있음.

## 장점

* **편리성**

    한 번의 로그인으로 여러 AWS 계정 및 애플리케이션에 접근할 수 있어 사용자 편의성이 높아짐.

* **보안**

    중앙에서 접근 권한을 관리하므로 보안이 강화됨.

* **효율성**

    다중 계정 및 애플리케이션에 대한 접근 권한을 중앙에서 관리할 수 있어 관리 효율성이 높아짐.

* **규정 준수**

    중앙 집중식 관리로 규정 준수 요구 사항을 쉽게 충족할 수 있음.

## 단점

* **복잡성**

    초기 설정 및 디렉토리 통합이 복잡할 수 있음.

* **비용**

    대규모 조직에서 모든 사용자를 관리할 때 비용이 증가할 수 있음.

* **의존성**

    AWS Identity Center의 가용성에 의존함.

## Use case

* **대규모 조직**

    여러 AWS 계정을 사용하는 대규모 조직에서 중앙 집중식으로 사용자 및 그룹을 관리할 때.

* **보안 요구 사항**

    보안 규정 준수를 위해 사용자 접근 권한을 세밀하게 관리할 때.

* **효율적인 관리**

    여러 계정 및 애플리케이션에 대한 접근 권한을 효율적으로 관리하고자 할 때.

## Summary

AWS Identity Center는 **중앙 집중식으로 사용자 및 그룹을 관리하고, 여러 AWS 계정 및 애플리케이션에 대한 접근을 한 번의 로그인으로 제공하는 서비스**임. 

이는 사용자 편의성과 보안을 동시에 제공하며, 대규모 조직에서의 접근 권한 관리를 효율적으로 할 수 있도록 도움을 줌. 

초기 설정이 복잡할 수 있지만, 중앙 집중식 관리와 규정 준수 측면에서 큰 장점을 제공함.