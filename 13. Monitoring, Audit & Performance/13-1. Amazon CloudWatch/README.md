# [Amazon CloudWatch](https://docs.aws.amazon.com/ko_kr/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)

## <img src = "https://github.com/user-attachments/assets/2ad4b869-6904-420d-b25e-4a25d7b88633" width = "25" height = "25"> Amazon CloudWatch

Amazon CloudWatch는 **AWS 리소스와 애플리케이션을 모니터링하는 서비스**임. 

CloudWatch는 **로그, 메트릭, 이벤트 데이터를 수집**하고, 이를 통해 **시스템의 성능 모니터링, 운영 문제 해결, 리소스 최적화를 지원**함.

## 특징

### 실시간 모니터링

AWS 리소스와 애플리케이션의 **실시간 성능 데이터를 수집하고 시각화**할 수 있음.

### 자동화된 경고

**특정 조건을 충족하면 자동으로 경고를 발생**시킬 수 있음.

### 광범위한 데이터 수집

다양한 AWS 서비스의 메트릭과 로그를 수집하여 **중앙에서 관리**할 수 있음.

### 확장성

**수집된 데이터의 양에 상관없이 확장**할 수 있음.

### 통합

**AWS 서비스와의 강력한 통합**을 제공하며, 다양한 서드파티 도구와도 연동 가능함.

## 구성요소

* **Metrics** (메트릭)

    리소스와 애플리케이션의 성능 데이터를 수집하여 저장함.

* **Alarms** (알람)

    메트릭 데이터를 기반으로 특정 조건이 충족되면 경고를 발생시킴.

* **Logs** (로그)

    애플리케이션 및 시스템 로그 데이터를 수집하고 분석할 수 있음.

* **Events** (이벤트)

    시스템 이벤트를 캡처하고 처리하여 자동화된 대응을 가능하게 함.

* **Dashboards** (대시보드)

    사용자 정의 가능한 대시보드를 통해 시각적으로 데이터를 모니터링할 수 있음.

## 아키텍처

CloudWatch는 **AWS 리소스에서 데이터를 수집하여 중앙화된 저장소에 저장**함. 

수집된 **데이터는 메트릭, 로그, 이벤트로 구분되며, 이를 기반으로 대시보드와 알람을 설정**할 수 있음. 

### 데이터 수집

AWS 리소스에서 메트릭, 로그, 이벤트 데이터를 수집함.

### 저장

수집된 데이터를 중앙 저장소에 저장함.

### 분석 및 시각화

저장된 데이터를 분석하고 시각화함.

### 알림 및 대응

특정 조건이 충족되면 알람을 통해 경고를 보내고, 이벤트를 통해 자동화된 대응을 수행함.


## 장점

* **실시간 모니터링**

    실시간으로 리소스와 애플리케이션의 성능을 모니터링할 수 있음.

* **자동화된 알람**

    특정 조건이 충족되면 자동으로 경고를 발생시켜 문제를 신속하게 대응할 수 있음.

* **확장성**

    데이터 양에 관계없이 확장 가능함.

* **통합**

    다양한 AWS 서비스와의 원활한 통합을 제공함.

## 단점

* **복잡성**

    초기 설정과 구성 작업이 다소 복잡할 수 있음.

* **비용**

    많은 양의 데이터를 수집하고 저장할 경우 비용이 증가할 수 있음.

## Metric

CloudWatch 메트릭은 **AWS 리소스의 성능 데이터를 나타내는 시간 경과에 따른 데이터 포인트**임. 

* Metric은 관찰해야하는 변수를 의미함(CPUUtilization, NetworkIn/Out, ...)

* Metric은 Namespaces에 속함.

* Dimension은 Metric의 속성임(intance id, environment, ...)

* 하나의 Metric 당 최대 30개의 Dimensions을 가질 수 있음.

* Metric에는 Timestamps가 있음.

* CloudWatch Custom Metrics를 생성할 수 있음.

### 수집 방법

* **AWS 서비스에서 기본 제공 메트릭**

    EC2 인스턴스, RDS 인스턴스 등 대부분의 AWS 서비스는 기본적으로 CloudWatch에 메트릭을 전송함.

* **사용자 정의 메트릭**

    사용자가 애플리케이션에서 생성한 메트릭을 CloudWatch에 전송할 수 있음.

## Metric Streams

CloudWatch Metric Streams는 **메트릭 데이터를 스트리밍하여 실시간 분석과 모니터링을 가능하게 하는 기능**임(Near-real-time delivery and Low Latency). 

이를 통해 메트릭 데이터를 **Kinesis Data Firehose, Kinesis Data Streams, S3, 3rd party service provider 등 다양한 대상으로 실시간 전송**할 수 있음.

### Architecture Example

![CloudWatch Metric Architecture](https://github.com/user-attachments/assets/19329705-c845-41f2-889d-95aff041a8ba)

## Summary

Amazon CloudWatch는 **AWS 리소스와 애플리케이션의 성능을 모니터링하고 최적화하는 강력한 도구**임. 

다양한 기능과 강력한 통합을 제공하지만, 초기 설정과 관리가 다소 복잡할 수 있음. 

**실시간 모니터링과 자동화된 경고 기능을 통해 시스템의 안정성과 성능을 유지하는 데 중요한 역할**을 함.






