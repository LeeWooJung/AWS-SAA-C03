# [Kinesis Data Analytics](https://docs.aws.amazon.com/kinesisanalytics/latest/dev/what-is.html)

## <img src = "https://github.com/user-attachments/assets/3f0bcd83-1746-4b12-911c-4d8f3b5914fc" width = "30" height = "30"> Kinesis Data Analytics

Amazon Kinesis Data Analytics는 **스트리밍 데이터를 실시간으로 처리하고 분석할 수 있는 서비스**임. 

이 서비스를 사용하여 스트리밍 데이터를 분석하고, 유용한 통찰을 실시간으로 얻을 수 있음.

[Kinesis Data Streams](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-4.%20AWS%20Kinesis/8-4-1.%20Kinesis%20Data%20Streams)와 [Kinesis Data Firehose](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-4.%20AWS%20Kinesis/8-4-2.%20Kinesis%20Data%20Firehose)에서 얻은 데이터를 **SQL**을 사용하여 실시간으로 분석함.

스트리밍데이터에 대한 정보를 풍부하게 하기 위해 [Amazon S3](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3)로부터 reference를 얻어옴.

## 특징

### 실시간 처리

실시간 스트리밍 데이터를 분석할 수 있음.

### 자동 확장(Automatic Scaling)

데이터 양에 따라 자동으로 확장되어 처리 성능을 유지함.

### 내장 함수

**데이터 변환, 필터링, 집계 등을 위한 다양한 내장 함수를 제공**함.

### 통합

Kinesis Data Streams, Kinesis Firehose 등과 쉽게 통합됨.

## 구성요소

* **SQL 애플리케이션**

    스트리밍 데이터를 **SQL을 사용하여 처리하고 분석하는 애플리케이션**.

* **Apache Flink 애플리케이션**

    더 복잡한 스트리밍 데이터 처리를 위해 Apache Flink를 사용하는 애플리케이션.

* **Input**

    Kinesis Data Streams 또는 Kinesis Firehose에서 **데이터를 수집**함.

* **Output**

    결과 데이터를 **다른 AWS 서비스로 보낼 수 있음** (예: S3, Redshift, OpenSearch/Elasticsearch, Kinesis Data Streams, Kinesis Data Firehose 등).

## 아키텍처

### 데이터 수집

Kinesis Data Streams 또는 Kinesis Firehose를 통해 실시간 데이터를 수집함.

### 데이터 처리

Kinesis Data Analytics를 통해 **실시간으로 데이터를 처리하고 분석**함.

### 데이터 저장

분석된 데이터를 S3, Redshift, Elasticsearch 등으로 저장함.

### 데이터 시각화

분석된 데이터를 QuickSight 등으로 시각화하여 인사이트를 도출함.

## 장점

* **실시간 데이터 처리**

    실시간으로 데이터를 처리하고 분석할 수 있음.

* **유연성**

    SQL 또는 Apache Flink를 사용하여 다양한 스트리밍 데이터 처리가 가능함.

* **자동 확장성**

    데이터 양에 따라 자동으로 확장되어 높은 처리 성능을 유지함.

* **통합성**

    다양한 AWS 서비스와 쉽게 통합됨.

## 단점

* **복잡성**

    복잡한 스트리밍 데이터 처리를 위해 Apache Flink를 사용하는 경우, 초기 설정과 관리가 어려울 수 있음.

* **비용**

    실시간 데이터 처리는 비용이 많이 들 수 있음.

## Use case

* **실시간 로그 분석**

    실시간으로 로그 데이터를 분석하여 이상 징후를 탐지하고, 문제를 신속히 해결함.

* **실시간 데이터 스트리밍 분석**

    소셜 미디어 데이터, 클릭스트림 데이터 등을 실시간으로 분석하여 유용한 인사이트를 도출함.

* **IoT 데이터 분석**

    IoT 장치에서 수집된 데이터를 실시간으로 분석하여 상태 모니터링 및 예측 유지보수를 수행함.

## Kinesis Data Analytics for Apache Flink

Kinesis Data Analytics for Apache Flink는 **Apache Flink를 사용하여 실시간 스트리밍 데이터를 처리하고 분석**할 수 있는 **완전 관리형 서비스**임. 

Apache Flink는 고성능 분산 스트리밍 데이터 처리 프레임워크로, Kinesis Data Streams 등과 통합하여 사용 가능함.

Apache Flink Application을 관리형 AWS Cluster에서 사용할 수 있음.

* provisioning compute resources, parallel computation, automatic scaling 가능.

* Checkpoints 와 Snapshot을 활용하여 Application Backup 가능.

* Apache Filnk 프로그래밍 features 사용 가능.

* **Kinesis Data Firehose**에서 나온 데이터는 사용하지 않음. 대신, **Kinesis Analytics for SQL**을 사용.

### 구성 요소

* **애플리케이션**

    Apache Flink를 사용하여 작성된 데이터 처리 애플리케이션.

* **데이터 소스**

    Kinesis Data Streams, Amazon MSK, Kafka 등에서 데이터를 수집함.

* **데이터 싱크**

    S3, DynamoDB, OpenSearch/Elasticsearch 등으로 처리된 데이터를 저장함.

* **Apache Flink 클러스터**

    애플리케이션을 실행하는 Flink 클러스터로, 관리형 서비스에서 자동으로 생성 및 관리됨.

## Summary

Kinesis Data Analytics는 **스트리밍 데이터를 실시간으로 처리하고 분석**할 수 있는 서비스임. 

주요 구성요소로는 **SQL 애플리케이션, Apache Flink 애플리케이션, Input 및 Output**이 있으며, 아키텍처는 데이터 수집, 처리, 저장, 시각화로 구성됨. 





