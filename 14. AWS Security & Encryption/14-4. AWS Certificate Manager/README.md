# [AWS Certificate Manager](https://aws.amazon.com/ko/certificate-manager/)

## <img src = "https://github.com/user-attachments/assets/e6d5f084-d953-4405-8311-71f1016f8434" width = "25" height = "25"> AWS Certificate Manager

AWS Certificate Manager (ACM)은 **SSL/TLS 인증서를 쉽게 프로비저닝, 관리 및 배포할 수 있도록 도와주는 AWS 서비스**임. 

ACM을 사용하면 **웹 애플리케이션과 서버 간의 안전한 통신을 보장**(in-flight encryption, HTTPS)할 수 있으며, **인증서 발급 및 갱신 과정을 자동화하여 관리 부담을 줄일 수 있음**(운영 오버헤드 감소).

**Public, Private TLS certificates** 모두 지원함. Public TLS certificates의 경우 무료로 사용할 수 있음.

**EC2에 사용할 수 없음**.

## 특징

### 자동화된 인증서 발급 및 갱신

ACM은 SSL/TLS 인증서를 **자동으로 발급하고 갱신해줌으로써 수동 관리의 부담을 줄여줌**.

### 무료 공용 인증서

ACM을 통해 **무료로 공용 SSL/TLS 인증서를 발급**받을 수 있음.

### 손쉬운 배포

ACM 인증서는 **Elastic Load Balancer (ELB), Amazon CloudFront, API Gateway 등 AWS 서비스에 손쉽게 배포**할 수 있음.

### 안전한 저장 및 관리

인증서는 안전하게 **AWS 관리하에 저장되고 갱신**됨.

## 구성요소

* **인증서**

    SSL/TLS 인증서로, 도메인 간의 안전한 통신을 보장함.

* **도메인 검증**

    도메인 소유권을 검증하기 위해 **DNS 또는 이메일 검증을 사용**할 수 있음.

* **갱신**

    ACM은 만료 전에 인증서를 자동으로 갱신함.

## 장점

* **자동화**

    인증서 발급 및 갱신 과정이 자동화되어 관리 부담이 줄어듦.

* **무료 인증서**

    공용 SSL/TLS 인증서를 무료로 제공함.

* **안전성**

    인증서를 안전하게 저장하고 관리할 수 있음.

* **손쉬운 통합**

    AWS 리소스와 손쉽게 통합하여 배포할 수 있음.

## 단점

* **AWS 전용**

    ACM 인증서는 **AWS 외부 리소스에는 사용할 수 없음**.

* **제한된 제어**

    자동화된 기능으로 인해 세부 설정에 대한 제어가 제한적일 수 있음.

## Use case

* **웹 애플리케이션 보안**

    **ELB, CloudFront, API Gateway 등을 사용하는 웹 애플리케이션의 SSL/TLS 인증서를 관리**할 때.

* **자동 갱신 필요**

    주기적인 인증서 갱신이 필요한 경우 ACM을 통해 자동으로 갱신하여 보안 위험을 줄일 때.

* **도메인 검증**

    도메인 소유권 검증이 필요한 경우 ACM을 통해 쉽게 검증할 때.

## Architecture Example

### Importing Public Certificates

![importing public certificates](https://github.com/user-attachments/assets/f08d8936-efde-4552-b2c1-24397a491b94)

### Integration with ALB

![Integration with ALB](https://github.com/user-attachments/assets/a181302f-9cf8-4403-9aa2-bf1c66fd7e01)


## Summary 

AWS Certificate Manager (ACM)은 SSL/TLS 인증서를 쉽게 관리하고 배포할 수 있도록 도와주는 서비스임. 

자동화된 인증서 발급 및 갱신, 무료 공용 인증서 제공, AWS 리소스와의 손쉬운 통합 등의 장점을 가지고 있음. 

AWS 전용 서비스이므로 외부 리소스에는 사용할 수 없으나, AWS 환경에서 보안 통신을 구현하고자 할 때 매우 유용함.