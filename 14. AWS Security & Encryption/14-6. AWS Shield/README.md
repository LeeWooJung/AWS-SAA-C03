# [AWS Shield](https://aws.amazon.com/ko/shield/)

## <img src = "https://github.com/user-attachments/assets/d7c71d10-097f-4adc-a073-4b3f529e6d09" width = "25" height = "25"> AWS Shield

AWS Shield는 **AWS의 DDoS(Distributed Denial of Service) 공격 방어 서비스**임. 

AWS Shield는 **두 가지 주요 계층, 즉 AWS Shield Standard와 AWS Shield Advanced로 제공**됨.

## AWS Shield Standard

AWS Shield Standard는 **모든 AWS 고객에게 자동으로 제공되며, 추가 비용 없이 DDoS 보호 기능을 기본적으로 제공**함.

SYN/UDP Floods, Reflection attacks와 Layer3, Layer4 attack과 같은 공격에 대한 보호를 제공함.

### 특징

* **기본 DDoS 보호**

    **네트워크 및 전송 계층에서의 일반적인 DDoS 공격으로부터 보호**s함.

* **자동 적용**

    **모든 AWS 서비스에 자동으로 적용되므로 설정이나 관리가 필요 없음**.

* **통합 보안**

    AWS CloudFront, Route 53, 및 Elastic Load Balancing(ELB)과 같은 AWS 서비스에 통합됨.

## AWS Shield Advanced

AWS Shield Advanced는 **더 높은 수준의 DDoS 보호를 제공하며, 추가적인 비용이 발생**함. 

주로 고급 보호 기능이 필요한 애플리케이션에 사용됨.

DDoS mitigation service를 선택적으로 제공함(한 기업, 한 달 당 $3,000의 요금).

**Amazon EC2, ELB, Amazon CloudFront, AWS Global Accelerator, Route53**에 대한 복잡한 공격을 보호해줌.

### 특징

* **실시간 공격 탐지**

    **실시간으로 DDoS 공격을 탐지하고 대응**함.

* **상위 레이어 보호**

    **애플리케이션 계층(Layer 7)까지 보호**함.

* **비용 보호**

    DDoS 공격으로 인해 발생할 수 있는 스케일링 비용을 보호해줌.

* **24/7 DDoS 대응 팀**

    AWS DDoS Response Team(DRT)과 24시간 365일 연락하여 지원을 받을 수 있음.

* **포괄적인 대시보드**

    AWS 관리 콘솔을 통해 **공격 대시보드를 제공하여, 실시간 모니터링 및 보고 기능을 제공**s함.

* **WAF 통합**

    **AWS WAF와 통합**되어 더 정교한 보호를 제공함.

## 구성 요소

* **자동 탐지 및 대응**

    AWS Shield는 모든 DDoS 공격을 자동으로 탐지하고 대응함.

* **알림**

    **CloudWatch와 통합되어 공격 발생 시 알림**을 받을 수 있음.

* **리포트**

    공격 후 상세한 보고서를 제공함.

* **DRT(DDoS Response Team) 지원**

    **AWS Shield Advanced 사용자에게 DRT의 지원을 제공**하여, 복잡한 공격에 대응함.

## 아키텍처

AWS Shield는 **AWS 인프라의 네트워크 계층과 전송 계층에 위치**하여, DDoS 공격이 발생하면 트래픽을 분석하고 필터링하여 정상적인 트래픽만 애플리케이션으로 전달함. 

AWS Shield Advanced는 추가적인 분석 계층과 지원을 제공함.


## 장점

* **자동 보호**

    기본적인 보호가 자동으로 제공됨.

* **통합성**

    AWS 서비스와 긴밀히 통합됨.

* **실시간 대응**

    실시간으로 공격을 탐지하고 대응함.

* **고급 기능**

    AWS Shield Advanced를 통해 더 높은 수준의 보호와 지원을 제공함.

## 단점

* **비용**

    AWS Shield Advanced는 추가 비용이 발생함.

* **제한된 보호**

    AWS Shield Standard는 기본적인 보호만 제공하므로, 고급 보호가 필요한 경우 Advanced로 업그레이드해야 함.

## Use case

* **웹 애플리케이션 보호**

    CloudFront와 통합하여 웹 애플리케이션을 DDoS 공격으로부터 보호함.

* **DNS 보호**

    **Route 53을 통해 DNS 공격으로부터 보호**함.

* **엔터프라이즈 애플리케이션 보호**

    AWS Shield Advanced를 통해 중요한 엔터프라이즈 애플리케이션을 보호함.

## Summary

AWS Shield는 **AWS 인프라를 통해 DDoS 공격으로부터 애플리케이션을 보호**하는 서비스임. 

AWS Shield Standard는 기본적인 보호를 자동으로 제공하며, AWS Shield Advanced는 더 높은 수준의 보호와 지원을 제공함. 

두 가지 계층 모두 AWS의 다양한 서비스와 통합되어 있어, 사용자에게 포괄적인 DDoS 보호를 제공함.