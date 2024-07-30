# [VPC Flow Logs](https://docs.aws.amazon.com/whitepapers/latest/aws-privatelink/what-are-vpc-endpoints.html)

## <img src = "https://github.com/user-attachments/assets/5de77c08-6981-4b69-ac5d-f3d273459eeb" width = "25" height = "25"> VPC Flow Logs

AWS의 VPC Flow Logs는 **VPC 내에서 발생하는 네트워크 트래픽에 대한 정보를 캡처하고 저장하는 기능**임. 

ELB, RDS, ElastiCache, Redshift, WorkSpaces, NAT Gateway, Transit Gateway 등의 AWS에서 관리되는 Interface에서 생성된 Network 정보도 캡처할 수 있음.

VPC Flow Logs는 **VPC, 서브넷 또는 네트워크 인터페이스 레벨에서 생성**될 수 있음. 

이를 통해 네트워크 트래픽을 모니터링하고 분석하여 보안 및 운영상의 문제를 해결할 수 있음.

캡처된 로그는 **Amazon CloudWatch Logs, Amazon S3, 또는 Amazon Kinesis Data Firehose에 저장**할 수 있음.

S3에 저장된 로그를 **Athena를 이용하여 Query** 혹은 CloudWatch Logs에 저장된 로그를 **CloudWatch Insights**, **Metric Filter**와 **CloudWatch Alarm**을 사용하여 사용 패턴이나 악의적인 행동 등을 분석할 수 있음.

이를 통해 네트워크 트래픽의 소스와 목적지, 프로토콜, 포트 번호, 패킷 크기, 수락/거부 상태 등 다양한 정보를 확인할 수 있음.



## 특징

### 네트워크 트래픽 모니터링

VPC 내의 **네트워크 트래픽을 모니터링하여 이상 징후를 감지하고 분석**할 수 있음.

### 세분화된 로깅

VPC, 서브넷, 네트워크 인터페이스 레벨에서 로그를 생성할 수 있어 세분화된 트래픽 분석이 가능함.

### 다양한 저장소 옵션

**CloudWatch Logs, S3, Kinesis Data Firehose 등 다양한 저장소 옵션을 제공**함.

### 자동화된 캡처

트래픽 로그를 자동으로 캡처하고 저장하여 **관리 오버헤드를 줄일 수 있음**(운영 오버헤드 감소).

### 보안 및 컴플라이언스

보안 감사 및 규정 준수 목적으로 네트워크 트래픽 로그를 저장하고 분석할 수 있음.

## 구성요소

* **VPC**

    네트워크 트래픽 로그를 캡처할 VPC.

* **서브넷**

    로그를 캡처할 서브넷.

* **네트워크 인터페이스**

    로그를 캡처할 개별 네트워크 인터페이스(ENI).

* **Flow Logs 설정**

    로그 캡처를 위한 Flow Logs 설정.

* **로그 그룹**

    로그를 저장할 CloudWatch Logs 그룹.

* **S3 버킷**

    로그를 저장할 Amazon S3 버킷.

* **Kinesis Data Firehose 스트림**

    로그를 전달할 Amazon Kinesis Data Firehose 스트림.

## 아키텍처

### 로그 생성

VPC, 서브넷 또는 네트워크 인터페이스에서 발생하는 트래픽에 대한 로그를 생성함.

### 로그 저장

생성된 로그를 CloudWatch Logs, S3, 또는 Kinesis Data Firehose에 저장함.

### 로그 분석

저장된 로그를 사용하여 네트워크 트래픽을 분석하고 이상 징후를 감지함.

### 경고 및 알림

**CloudWatch Alarms 등**을 통해 이상 징후에 대한 경고 및 알림을 설정할 수 있음.

## Architecture Example

![vpc flow logs architecture](https://github.com/user-attachments/assets/49d270c1-91e8-46db-a7bf-da73de6ed76c)


## Use case

* **보안 모니터링**

    VPC 내의 보안 위협을 식별하고 대응하기 위해 트래픽 로그를 분석함.

* **성능 최적화**

    네트워크 성능 문제를 식별하고 최적화하기 위해 트래픽 로그를 사용함.

* **규정 준수**

    규정 준수를 위해 네트워크 활동 로그를 저장하고 분석함.

* **트러블슈팅**

    네트워크 문제를 진단하고 해결하기 위해 트래픽 로그를 사용함.

## Summary

AWS의 VPC Flow Logs는 **VPC 내에서 발생하는 네트워크 트래픽에 대한 정보를 캡처하고 저장하는 기능**임. 

이를 통해 **네트워크 트래픽을 모니터링하고 분석하여 보안 및 운영상의 문제를 해결**할 수 있음. 

VPC, 서브넷 또는 네트워크 인터페이스 레벨에서 로그를 생성할 수 있으며, CloudWatch Logs, S3, Kinesis Data Firehose 등 다양한 저장소 옵션을 제공함. 

**실시간 모니터링, 보안 강화, 운영 효율성 향상 등의 장점**이 있지만, **비용 증가, 복잡성 증가, 성능 영향 등의 단점**도 존재함. 

주요 사용 사례로는 보안 모니터링, 성능 최적화, 규정 준수, 트러블슈팅 등이 있음.