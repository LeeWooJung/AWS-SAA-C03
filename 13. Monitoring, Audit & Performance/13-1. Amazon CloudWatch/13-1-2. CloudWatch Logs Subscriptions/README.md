# [CloudWatch Logs Subscriptions](https://docs.aws.amazon.com/ko_kr/AmazonCloudWatch/latest/logs/Subscriptions.html)

Amazon CloudWatch Log Subscription은 **로그 데이터를 실시간으로 다른 AWS 서비스로 스트리밍할 수 있는 기능**임. 

이를 통해 **로그 데이터를 다양한 분석 도구로 전달하거나, 실시간 처리를 통해 빠르게 대응**할 수 있음.

## 특징

### 실시간 스트리밍

로그 이벤트가 생성되는 즉시 다른 AWS 서비스로 전달됨.

### 다양한 대상

로그 데이터를 **Amazon Kinesis Data Streams, Amazon Kinesis Data Firehose, AWS Lambda 등**으로 스트리밍할 수 있음.

### 필터링

필터를 사용하여 **특정 로그 이벤트만 스트리밍**할 수 있음.

## 구성요소

* **Log Groups** (로그 그룹)

    로그 구독은 특정 로그 그룹에 대해 설정됨.

* **Subscription Filters** (구독 필터)

    로그 이벤트를 필터링하여 **특정 조건을 만족하는 이벤트만 스트리밍**할 수 있음.

* **Destination** (목적지)

    로그 데이터를 스트리밍할 AWS 서비스.

## 아키텍처

### 로그 수집

애플리케이션이나 시스템에서 로그 이벤트를 CloudWatch Logs에 기록함.

### 로그 구독 설정

**로그 그룹에 구독 필터를 설정하여 특정 로그 이벤트를 필터링**함.

### 로그 스트리밍

필터링된 로그 이벤트를 지정된 AWS 서비스로 스트리밍함.

## 대상 서비스

### AWS Lambda

**실시간 로그 처리**를 위해 사용됨. 

예를 들어, **로그 이벤트를 분석하고, 알림을 트리거하거나, 데이터를 변환**하는 등의 작업을 수행할 수 있음.

### Amazon Kinesis Data Streams

로그 데이터를 **실시간 분석 시스템으로 전달**함. 

예를 들어, 로그 데이터를 실시간으로 처리하고, 데이터베이스에 저장하거나, 분석 대시보드로 전달할 수 있음.

### Amazon Kinesis Data Firehose

로그 데이터를 **S3, Redshift, OpenSearch/Elasticsearch** 등으로 실시간으로 전달하여 저장하거나 분석할 수 있음.

## Architecture Example

### Subscription Filter

![Cloudwatch Logs Subscriptions Architecture](https://github.com/user-attachments/assets/161627b7-4da0-476b-b5dc-f8aff9ac9339)

### Multi-Account & Multi Region

![Multi Account   Multi Region Architecture](https://github.com/user-attachments/assets/e0d26a97-d647-4a34-bc48-bf7f03d372b4)

### Cross-Account Subscription

![Cross-Account Subscription Architecture](https://github.com/user-attachments/assets/35e734be-0d43-4283-a589-57ec22684624)



## 장점

* **실시간 분석**

    로그 데이터를 실시간으로 처리하고 분석할 수 있음.

* **유연성**

    다양한 AWS 서비스와 통합하여 로그 데이터를 처리할 수 있음.

* **필터링**

    특정 로그 이벤트만 선택적으로 스트리밍할 수 있음.

## 단점

* **비용**

    실시간 스트리밍 및 처리에 따른 비용이 발생할 수 있음.

* **복잡성**

    구독 필터 설정 및 대상 서비스와의 통합이 복잡할 수 있음.

* **성능**

    대량의 로그 데이터를 처리할 경우 성능 문제가 발생할 수 있음.

## Use case

* **보안 모니터링**

    실시간으로 보안 로그를 분석하여 위협을 감지하고 대응할 수 있음.

* **애플리케이션 모니터링**

    애플리케이션 로그를 실시간으로 분석하여 성능 문제를 신속하게 해결할 수 있음.

* **규정 준수**

    실시간으로 로그 데이터를 저장하고 분석하여 규정 준수 요구사항을 충족할 수 있음.

## Summary

CloudWatch Log Subscription은 **로그 데이터를 실시간으로 다른 AWS 서비스로 스트리밍**할 수 있는 기능으로, 실**시간 분석 및 처리를 통해 빠르게 대응**할 수 있음. 

**다양한 대상 서비스와의 유연한 통합**을 제공하며, **특정 로그 이벤트를 필터링**하여 선택적으로 스트리밍할 수 있음. 

그러나 비용과 복잡성 측면에서 주의가 필요함.