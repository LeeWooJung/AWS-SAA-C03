# [AWS Firewall Manager](https://docs.aws.amazon.com/waf/latest/developerguide/fms-chapter.html)

## <img src = "https://github.com/user-attachments/assets/3d271c3d-2f49-40c0-86a1-4e3a1f0737f1" width = "25" height = "25"> AWS Firewall Manager

AWS Firewall Manager는 **조직 전체의 방화벽 규칙과 보안 정책을 중앙에서 관리할 수 있는 서비스**임. 

**AWS Organization**의 모든 계정에 대한 Rule을 관리함.

이를 통해 사용자는 **일관된 보안 태세를 유지하고, 새로운 계정이나 리소스가 추가될 때 자동으로 보안 정책을 적용**할 수 있음.

AWS Firewall Manager에서 적용되는 방화벽 규칙은 **Region Level**임.

## 특징

### 중앙 관리

조직의 여러 계정에 걸쳐 방화벽 규칙을 중앙에서 관리할 수 있음.

### 자동 적용

새로운 계정이나 리소스가 추가될 때 자동으로 보안 규칙을 적용할 수 있음.

### 일관된 보안

모든 리소스에 대해 일관된 보안 규칙을 유지할 수 있음.

### AWS WAF 통합

**AWS WAF(Web Application Firewall)와 통합되어 웹 애플리케이션 보호를 강화**할 수 있음.

WAF - ALB, API Gateways, CloudFront

### AWS Shield 통합

**AWS Shield Advanced와 통합되어 DDoS 보호를 중앙에서 관리**할 수 있음.

Shield Advanced - ALB, CLB, NLB, Elastic IP, CloudFront

### AWS Security Group 관리

**Security Group 규칙을 중앙에서 관리하고 모니터링**할 수 있음.

Security Groups - EC2, ALB, ENI resource in VPC

### AWS Network Firewall 통합

AWS Network Firewall와 통합되어 VPC Level에서의 보호를 강화할 수 있음.

### Amazon Route53 통합

Amazon Route53과 통합되어 DNS Firewall의 기능을 강화할 수 있음

## 구성 요소

* **정책 관리**

    **방화벽 정책을 생성하고 관리하며, 이를 조직의 여러 계정에 적용**함.

* **정책 적용**

    새로 생성된 리소스나 계정에 대해 자동으로 보안 정책을 적용함.

* **정책 모니터링**

    적용된 정책의 상태를 모니터링하고, 규정 준수를 확인함.

* **통합 관리 콘솔**

    AWS Management Console을 통해 모든 정책과 규칙을 중앙에서 관리할 수 있음.

## 장점

* **중앙 집중 관리**

    여러 계정에 걸쳐 보안 정책을 중앙에서 관리할 수 있음.

* **자동화**

    새로운 리소스에 대해 자동으로 보안 규칙을 적용함.

* **통합성**

    AWS의 다양한 보안 서비스와 통합되어 있음.

* **일관성**

    조직 전체에 일관된 보안 정책을 유지할 수 있음.

## 단점

* **복잡성**

    대규모 조직의 복잡한 보안 요구 사항을 관리하기 위해 초기 설정이 복잡할 수 있음.

* **비용**

    추가 비용이 발생할 수 있으며, 조직의 규모에 따라 비용이 증가할 수 있음.

## Use case

* **기업 보안 관리**

    대규모 기업이 조직 전체의 보안 정책을 중앙에서 관리하고 일관된 보안 태세를 유지함.

* **웹 애플리케이션 보호**

    **AWS WAF와 통합하여 웹 애플리케이션을 보호**하고, 중앙에서 WAF 규칙을 관리함.

* **DDoS 보호**

    **AWS Shield Advanced와 통합하여 DDoS 공격으로부터 중앙에서 보호**함.

* **규정 준수 관리**

    보안 규칙을 중앙에서 관리하고, 규정 준수를 확인함.

## Summary

AWS Firewall Manager는 **조직 전체의 방화벽 규칙과 보안 정책을 중앙에서 관리**할 수 있는 서비스임. 

이를 통해 사용자는 일관된 보안 태세를 유지하고, 새로운 계정이나 리소스가 추가될 때 자동으로 보안 정책을 적용할 수 있음. 

AWS Firewall Manager는 AWS WAF, AWS Shield, AWS Security Groups와 통합되어 다양한 보안 요구 사항을 중앙에서 관리할 수 있음.