# [Amazon Systems Manager](https://docs.aws.amazon.com/ko_kr/systems-manager/latest/userguide/what-is-systems-manager.html)


## <img src = "https://github.com/user-attachments/assets/c805fa4b-76fd-4a7f-ae76-405fedbe078d" width = "25" height = "25"> Amazon Systems Manager(SSM)

Amazon Systems Manager는 AWS에서 제공하는 **통합 관리 서비스로, AWS 리소스 및 온프레미스 서버의 운영을 자동화하고 중앙에서 관리할 수 있도록 지원**함. 

이를 통해 **서버 인프라의 상태를 중앙에서 모니터링하고, 시스템 구성을 유지하며, 보안 및 규정 준수 요구사항을 충족하고 운영 작업을 자동화**하는 데 도움을 줌. 

Systems Manager는 **구성 관리, 패치 관리, 소프트웨어 배포, 운영 데이터 수집 및 분석 등의 다양한 기능을 제공**함.

## 특징

### 통합 관리

AWS 리소스와 온프레미스 서버를 중앙에서 관리할 수 있음.

### 자동화

운영 작업을 자동화하여 반복적인 작업의 효율성을 높임.

### 구성 관리

시스템 구성 상태를 관리하고 유지함.


### 패치 관리

서버와 인스턴스에 대한 **패치 관리를 자동화**함.

### 운영 데이터 수집 및 분석

시스템 상태와 운영 데이터를 수집하고 분석함.

### 보안 및 규정 준수

보안 정책과 규정 준수 요구사항을 충족할 수 있음.

### 원격 명령 실행

원격으로 명령을 실행하고 스크립트를 배포할 수 있음.

## 구성요소

### Run Command

원격 명령 또는 Document, Script를 실행하여 인스턴스를 관리할 수 있음.

Resource Group을 사용하여 다수의 Instances에 Command를 실행할 수 있음.

**SSH**를 사용하지 않음.

실행 결과는 **AWS Console**에 보여지며, **S3와 CloudWatch Logs**에 전송됨.

Command 결과는 SNS로 전송될 수 있음(Notification).

**IAM과 CloudTrail**과 통합되어 Command에 대한 보안 정책을 구성할 수 있음.

**EventBridge**에 의해 명령이 실행될 수 있음.

* **Architecture Example**

    ![run command](https://github.com/user-attachments/assets/1f7a6418-e869-43e4-9047-4ce4e26bc9ef)

### Automation

EC2 Instances와 다른 AWS Resource에서 실행 및 유지보수에 대한 **작업을 간단히**하고 자동화해줌.

예를 들어 Instance 재시작, AMI 생성, EBS Snapshot 등을 자동화함.

**Automation Runbook**을 이용하여 반복적인 작업을 자동화하고 워크플로우를 정의함.

* **Automation Runbook**

    SSM Document로 EC2 Instances 또는 이미 생성된 AWS Resources에 대한 작업을 정의해놓은 것.

사용자가 직접 **AWS Console, AWS CLI/SDK**를 사용하여 Automation을 Trigger 할 수 있음.

또는, **Amazon EventBridge**, **Maintenance Windows**로 Automation을 Trigger할 수 있음.

Rule 수정을 위해 **AWS Config**에 의해 Trigger 될 수도 있음.

### Maintenance Windows

Instances에 실행해야할 것에 대한 **Schedule**을 정의함.

예를 들어, OS Patching, Drivers 업데이트, 소프트웨어 설치 등에 대한 스케쥴을 정할 수 있음.

Schedule, Duration, Set of registered instances, Set of resistered tasks 등을 포함함.

* **Architecture Example**

    ![maintenance windows](https://github.com/user-attachments/assets/200842cd-4619-478a-8758-b0653e4a0519)

### Patch Manager

시스템의 패치(OS Updates, Application Updates, Security Updates) 및 보안 패치를 자동으로 관리함.

EC2 Instances와 On-Premise Servers 모두 지원함.

Linux, Windows, MacOS 모두 지원함.

**Maintenance Windows**를 이용하여 스케쥴링된 Patch를 진행할 수 있고, On-Demand에 따라 Patch를 진행할 수 있음.

### Session Manager

EC2와 On-premise 서버에 안전한 원격 접속을 제공(secure shell).

SSH Access, Bation Hosts, SSH Keys가 필요 없음.

더 나은 보안을 위해 **Port 22**를 사용하지 않음.

Linux, MacOS, Windows 모두 지원함.

S3 또는 CloudWatch Logs에 Log Data를 전송할 수 있음.

* **Architecture Example**

    ![session manager](https://github.com/user-attachments/assets/5f2b6edd-3885-43fc-b58a-14a5a30dac20)

### Parameter Store

구성 데이터를 안전하게 저장하고 관리함.

### OpsCenter

운영 문제를 중앙에서 관리하고 해결할 수 있음.

### Inventory

시스템 구성 데이터를 수집하고 관리함.

### State Manager

인스턴스의 상태를 원하는 구성으로 유지함.

## 아키텍처

### 인스턴스 에이전트

Systems Manager Agent가 설치된 인스턴스에서 시스템 데이터를 수집하고 명령을 실행함.

### AWS Systems Manager

중앙 관리 콘솔을 통해 다양한 구성요소를 설정하고 관리함.

### AWS 서비스 통합

**CloudWatch, Config, IAM 등과 통합하여 모니터링, 보안, 규정 준수를 강화**함.

## Use case

* **패치 관리**

    대규모 서버 인프라에 대한 자동 패치 관리를 통해 보안 강화.

* **구성 관리**

    서버 인프라의 일관된 구성을 유지하고 변경 사항을 자동으로 적용.

* **운영 문제 해결**

    중앙 콘솔을 통해 운영 문제를 신속하게 파악하고 해결.

* **자동화된 배포**

    소프트웨어 및 업데이트를 자동화하여 배포 효율성을 향상.

* **원격 명령 실행**

    원격 명령을 통해 서버 인프라를 관리하고 문제를 해결.

## Summary

Amazon Systems Manager는 **AWS 리소스와 온프레미스 서버를 중앙에서 통합 관리하고 운영 작업을 자동화하는 서비스**임. 

**구성 관리, 패치 관리, 운영 데이터 수집 및 분석, 원격 명령 실행 등의 기능**을 제공하여 운영 효율성을 높이고 보안과 규정 준수를 강화함. 

다양한 AWS 서비스와 통합하여 인프라 관리의 복잡성을 줄이고 운영 비용을 절감할 수 있음. 