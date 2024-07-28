# [AWS Directory Services](https://docs.aws.amazon.com/ko_kr/directoryservice/latest/admin-guide/what_is.html)

AWS Directory Services는 **AWS 클라우드에서 디렉토리 기반의 작업을 수행할 수 있도록 지원하는 관리형 서비스**임. 

이는 **기존의 온프레미스 Active Directory와의 통합을 용이**하게 하고, 새로운 디렉토리 기반 애플리케이션을 클라우드에서 쉽게 배포 및 관리할 수 있게 함.

## 특징

### 다양한 디렉토리 옵션

**AWS Managed Microsoft AD, AD Connector, Simple AD** 등 다양한 디렉토리 서비스를 제공함.

### 관리형 서비스

AWS에서 디렉토리의 설치, 유지 관리, 백업을 관리하여 **운영 부담을 줄임**.

### 통합성

**온프레미스 Active Directory와 쉽게 통합 가능**함.

### 보안 및 규정 준수

AWS의 보안 및 규정 준수 기능을 통해 데이터 보안을 강화할 수 있음.

## 구성요소

* **AWS Managed Microsoft AD**

    **완전 관리형 Microsoft Active Directory 서비스로, 온프레미스 AD와의 완벽한 통합을 지원**함.

    AD를 AWS에서 생성하고, **locally User를 관리**하며 MFA 사용 가능.

    On-premise AD와 **Trust** 연결을 생성하여 연결

* **AD Connector**

    **온프레미스 AD를 AWS 서비스와 연결하여 사용하도록 돕는 프록시(Directory Gateway) 서비스**임.

    MFA를 사용 가능하며, User는 **On-premise AD에서 관리함**.

* **Simple AD**

    기본적인 디렉토리 서비스가 필요한 소규모 환경을 위해 제공되는 **경량 디렉토리 서비스**임.

    **On-premise AD와 연결될 수 없음**.

* **Amazon Cognito User Pools**

    웹 및 모바일 앱에서 사용자 디렉토리를 관리할 수 있도록 지원함.

## 아키텍처

### AWS Managed Microsoft AD

AWS 클라우드에서 도메인 컨트롤러를 설정하고 관리하며, **온프레미스 AD와의 트러스트를 통해 통합 관리가 가능**함.

### AD Connector

**온프레미스 AD와 AWS 클라우드 간의 디렉토리 요청을 프록시로 처리**하여, 온프레미스 리소스를 AWS 클라우드에서 활용할 수 있게 함.

### Simple AD

AWS 클라우드에서 경량의 LDAP 호환 디렉토리 서비스로 작동함.

## Connect With IAM Identity Center

### Directory Service

IAM Identity Center와 **AWS Managed Microsoft AD**를 직접 연결

### Self-Managed Directory

1. AWS Managed Microsoft AD를 사용하여 **Two-way Trust Relationship**을 구축함.

    > [IAM Identity Center] <-> [AWS Managed Microsoft AD] <-> [Active Directory] 

    와 같이 연결할 수 있음.

2. AD Connector를 사용하여 Proxy 연결.

    > [IAM Identity Center] <-> [AD Connector] <-> [Active Directory]

    와 같이 연결할 수 있음.


## 장점

* **관리의 용이성**

    AWS에서 디렉토리 관리 작업을 수행하므로 운영 부담이 줄어듦.

* **확장성**

    필요에 따라 쉽게 확장 가능함.

* **온프레미스 통합**

    온프레미스 AD와의 통합을 통해 일관된 디렉토리 관리 가능함.

* **보안**

    AWS의 보안 기능을 활용하여 안전하게 디렉토리를 관리할 수 있음.

## 단점

* **비용**

    사용량에 따른 비용이 발생할 수 있음.

* **제한된 기능**

    일부 고급 기능은 지원되지 않을 수 있음.

* **복잡성**

    기존 온프레미스 인프라와의 통합 설정이 복잡할 수 있음.

## Use case

* **하이브리드 클라우드 환경**

    온프레미스 AD와 AWS 클라우드를 통합하여 **일관된 디렉토리 관리가 필요할 때 사용**함.

* **웹 및 모바일 애플리케이션**

    **사용자 인증 및 디렉토리 관리를 위해 Amazon Cognito User Pools를 활용**할 수 있음.

* **기업 네트워크**

    클라우드 기반의 디렉토리 서비스를 통해 글로벌 기업 네트워크를 관리함.

## Summary

AWS Directory Services는 **AWS 클라우드에서 디렉토리 기반 작업을 수행**할 수 있도록 지원하는 관리형 서비스임. 

**AWS Managed Microsoft AD, AD Connector, Simple AD** 등 다양한 옵션을 제공하며, 온프레미스 AD와의 통합, 보안 및 규정 준수, 확장성 등의 특징을 가짐. 

하이브리드 클라우드 환경, 웹 및 모바일 애플리케이션, 기업 네트워크 등 다양한 사용 사례에서 활용됨. 

이 서비스는 관리의 용이성, 확장성, 보안 등의 장점을 제공하지만, 비용과 복잡성 등의 단점이 있을 수 있음.