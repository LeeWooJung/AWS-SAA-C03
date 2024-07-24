# [CloudWatch Logs](https://docs.aws.amazon.com/ko_kr/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html)

## <img src = "https://github.com/user-attachments/assets/7afdaee7-46fb-475d-8cdb-aaae12596a00" width = "25" height = "25"> CloudWatch Logs

Amazon CloudWatch Logs는 **애플리케이션, 시스템 및 AWS 리소스에서 생성된 로그 데이터를 모니터링, 저장 및 액세스할 수 있도록 지원하는 서비스**임. 

이를 통해 **로그 데이터를 중앙에서 관리하고, 시스템 성능을 분석하며, 문제를 해결**할 수 있음.

## 특징

### 로그 수집 및 저장

다양한 소스에서 생성된 로그 데이터를 수집하고 **중앙 저장소에 안전하게 저장**할 수 있음. 

또한, Expiration Policies(만기 정책)을 정의할 수 있음(Never expire, 1 day to 10 years, ...)

### 암호화

Default로 로그는 **암호화됨**. 

Key를 가지고 **KMS-based encrpytion** 가능.

### 실시간 모니터링

실시간으로 로그 데이터를 모니터링하고 분석할 수 있음.

### 알림 및 경고

**특정 패턴이나 조건이 로그에서 발생하면 알림을 설정**할 수 있음.

### 필터 및 검색

로그 데이터를 **필터링하고 검색하여 원하는 정보를 빠르게 찾을 수 있음**.

### 시각화

로그 데이터를 그래프로 시각화하여 직관적으로 이해할 수 있음.

## 구성요소

* **Log Groups** (로그 그룹)

    관련 **로그 스트림을 그룹화하여 논리적인 단위로 관리**할 수 있음.

    임의이 이름으로 지정되며, 보통 Application을 나타냄.

* **Log Streams** (로그 스트림)

    로그 그룹 내에서 **순차적으로 기록된 로그 이벤트의 흐름**을 나타냄.

    Application, Log files, Containers에 속한 instances를 의미함.

* **Log Events** (로그 이벤트)

    로그 스트림에 저장된 개별 로그 항목으로, **타임스탬프와 메시지**를 포함함.

* **Metric Filters** (메트릭 필터)

    로그 데이터를 기준으로 **특정 조건이 충족되면 메트릭을 생성**할 수 있음.

* **Subscriptions** (구독)

    로그 데이터를 다른 AWS 서비스(Kinesis, Lambda, Amazon S3, OpenSearch 등)로 **실시간으로 전송**할 수 있음.

## CloudWatch Logs의 Sources

* SDK, CloutWatch Logs Agent, CloutWatch Unified Agent

* Elastic Beanstalk

    Application으로 부터 생성된 로그의 모음.

* ECS

    Containers로부터 수집된 로그들.

* AWS Lambda

    Lambda Function의 로그의 모음.

* VPC Flow Logs

    VPC에서 일어난 특정 로그들.

* API Gateway

* CloudTrail based on filter

* Route53

    DNS Query의 로그들.

## 아키텍처

### 로그 수집

애플리케이션, AWS 서비스, 시스템에서 로그 데이터를 수집함.

### 로그 저장

수집된 로그 데이터를 **로그 스트림에 저장하고, 로그 그룹으로 그룹화**함.

다른 AWS 계정에 존재하는 여러 Log Group의 로그를 저장할 수 있음.

### 로그 분석

로그 데이터를 **실시간으로 분석하고, 메트릭 필터를 사용하여 특정 조건에 대한 경고를 설정**함.

### 로그 시각화

로그 데이터를 그래프로 시각화하여 모니터링함.

## Architecture Example

### S3 Export

![s3 export architecture](https://github.com/user-attachments/assets/08ad9bf7-548f-4cbb-ad6c-4d360887cc5f)

Log 데이터는 Export 가능할 때까지 **12시간**정도 걸림.

**CreateExportTask**를 통해 API Call 가능.

Near-real-time, Real-time이 아님.

## 장점

* **중앙 관리**

    다양한 소스에서 생성된 로그 데이터를 중앙에서 관리할 수 있음.

* **실시간 분석**

    실시간으로 로그 데이터를 분석하고 문제를 신속하게 감지할 수 있음.

* **확장성**

    대량의 로그 데이터를 처리할 수 있는 확장성을 제공함.

* **통합**

    다양한 AWS 서비스와 원활하게 통합됨.

## 단점

* **비용**

    대량의 로그 데이터를 장기간 저장할 경우 비용이 증가할 수 있음.

* **보안**

    로그 데이터에 대한 적절한 보안 설정이 필요함.

## Use case

* **애플리케이션 디버깅**

    애플리케이션에서 발생하는 오류와 예외를 추적하여 문제를 해결할 수 있음.

* **보안 모니터링**

    보안 관련 이벤트를 로그에서 모니터링하고 경고를 설정할 수 있음.

* **시스템 성능 분석**

    시스템 성능을 분석하고 최적화하는 데 사용할 수 있음.

* **규정 준수**

    로그 데이터를 통해 규정 준수 요구사항을 충족할 수 있음.

## Summary

Amazon CloudWatch Logs는 **로그 데이터를 중앙에서 관리하고 실시간으로 모니터링, 분석할 수 있는 강력한 도구**임. 

**로그 그룹과 로그 스트림을 통해 데이터를 구조화**하고, **메트릭 필터와 구독을 통해 실시간 알림과 분석을 제공**함. 

다양한 AWS 서비스와의 통합을 통해 확장성과 유연성을 제공하지만, 비용과 보안 측면에서 적절한 관리가 필요함.

