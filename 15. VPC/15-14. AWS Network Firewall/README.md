# [AWS Network Firewall](https://aws.amazon.com/ko/network-firewall/)

## <img src = "https://github.com/user-attachments/assets/557cabc5-1043-4874-8b85-6a964d26128d" width = "25" height = "25"> Network Firewall

AWS Network Firewall은 Amazon Web Services에서 제공하는 **관리형 네트워크 보안 서비스**임. 

이는 **전체 VPC 내에서 트래픽을 모니터링하고 제어할 수 있도록 도와주는 고성능 네트워크 방화벽**임. 

AWS Network Firewall은 **Stateful 및 Stateless 패킷 필터링, 고급 네트워크 보안 기능, 그리고 중앙 관리 및 모니터링 기능, 위협 탐지 및 차단 기능을 제공**함.

**Layer 3부터 Layer 7까지** 모두 보호할 수 있음.

VPC 내의 모든 Traffic을 감시할 수 있음.

* VPC에서 다른 VPC로의 Traffic
* Internet으로의 Outbound Traffic
* Internet에서의 Inbound Traffic
* Direct Connect, Site-to-Site VPN 과의 In/Outbound Traffic

내부적으로 AWS Network Firewall는 **AWS Gateway LoadBalancer**를 사용함.

## 특징

### Stateful Inspection

**트래픽의 상태를 기반으로 필터링 규칙**을 적용하여 더 정교한 보안을 제공함.

### Stateless Inspection

각 **패킷을 독립적으로 검사**하여 빠른 트래픽 필터링을 가능하게 함.

### 고급 네트워크 보안

서명 기반 탐지, 침입 방지 시스템(IPS), URL 필터링 등의 고급 보안 기능을 제공함.

### 유연한 규칙 관리

사용자가 정의한 보안 규칙을 통해 트래픽을 허용하거나 차단함.

### 중앙 관리 및 모니터링

AWS Management Console, AWS CLI, 및 API를 통해 중앙에서 방화벽 규칙을 관리하고 모니터링할 수 있음.

### 완전 관리형 서비스

AWS가 인프라 관리를 담당하여 사용자는 보안 정책 설정 및 관리에 집중할 수 있음(운영 오버헤드 감소).

## 구성요소

* **방화벽** (Firewall)

    네트워크 트래픽을 모니터링하고 제어하는 기본 구성 요소임.

* **방화벽 정책** (Firewall Policy)

    **Stateful 및 Stateless 규칙을 정의**하여 방화벽이 트래픽을 처리하는 방식을 결정함.

* **방화벽 규칙 그룹** (Rule Group)

    특정 트래픽 유형에 대한 필터링 규칙을 모아둔 그룹임.

* **알림 및 로깅**

    AWS CloudWatch 및 Amazon S3를 통해 방화벽 이벤트를 로깅하고 모니터링함.

## 아키텍처

### 방화벽 생성

AWS Management Console에서 새로운 Network Firewall을 생성함.

### 방화벽 정책 설정

**Stateful 및 Stateless 규칙**을 포함하는 방화벽 정책을 생성함.

### 방화벽 규칙 그룹 구성

특정 트래픽 유형에 대한 필터링 규칙을 정의함.

### 트래픽 라우팅

**VPC 서브넷의 트래픽을 Network Firewall로 라우팅하여 모든 트래픽이 방화벽을 통과**하도록 설정함.

### 모니터링 및 로깅

CloudWatch 및 S3, CloudWatch Logs, Kinesis Data Firehose를 통해 방화벽 활동을 모니터링하고 로그를 분석함.

## Use case

* **애플리케이션 보호**

    웹 애플리케이션 및 데이터베이스 앞에 Network Firewall을 배치하여 외부 위협으로부터 보호함.

* **규정 준수**

    데이터 보호 규제 요구 사항을 충족하기 위해 트래픽 모니터링 및 로깅 기능을 활용함.

* **멀티 VPC 환경**

    **여러 VPC 간의 트래픽을 중앙에서 제어하고 모니터링하여 보안을 강화**함.

* **침입 탐지 및 방지**

    Stateful 및 Stateless 규칙을 사용하여 악성 트래픽을 탐지하고 차단함.

## Summary

AWS Network Firewall은 사용자 **VPC 내의 네트워크 트래픽을 모니터링하고 제어할 수 있는 고성능 네트워크 보안 서비스**임. 

이를 통해 네트워크 보안을 강화하고, 다양한 보안 규칙을 유연하게 적용하며, **중앙에서 관리**할 수 있음. 

고급 네트워크 보안 기능과 완전 관리형 서비스로 보안 관리의 효율성을 높이고, 다양한 사용 사례에 적용할 수 있음.