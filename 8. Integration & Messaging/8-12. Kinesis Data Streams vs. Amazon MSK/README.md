# Kinesis Data Streams vs. Amazon MSK

## 개념 및 목적

### Kinesis Data Streams

AWS에서 제공하는 실시간 데이터 스트리밍 서비스로, 데이터를 빠르게 수집, 처리, 분석할 수 있도록 설계됨. 

주로 로그, IoT 데이터, 이벤트 데이터 등 실시간 데이터 스트리밍에 사용됨.

### Amazon MSK

Apache Kafka를 관리형으로 제공하는 서비스로, Kafka 클러스터를 쉽게 생성, 운영할 수 있도록 지원함. 

Kafka의 다양한 기능을 활용하여 데이터 스트리밍을 관리하고 처리하는 데 사용됨.

## 아키텍처 및 구성 요소

### Kinesis Data Streams

* **Shard**

    데이터 스트림을 구성하는 기본 단위로, 각 샤드는 읽기 및 쓰기 용량이 정해져 있음.

* **Producer**

    데이터를 스트림으로 보내는 역할.

* **Consumer**  
    
    스트림에서 데이터를 읽어가는 역할.

* **Kinesis Client Library** (KCL)

    컨슈머 애플리케이션 개발을 용이하게 하는 라이브러리.

### Amazon MSK

* **Broker**

    Kafka 클러스터를 구성하는 서버.

* **Topic**

    데이터를 카테고리별로 나누어 저장하는 단위.

* **Partition**

    토픽 내에서 데이터를 분산 저장하는 단위.

* **Producer**

    데이터를 Kafka 토픽으로 보내는 역할.

* **Consumer**

    Kafka 토픽에서 데이터를 읽어가는 역할.

* **Zookeeper**

    클러스터 상태 관리 및 메타데이터 조정.


## 관리 및 설정

### Kinesis Data Streams

AWS가 완전 관리형으로 제공하며, 사용자는 **샤드 수와 읽기/쓰기 용량을 설정**할 수 있음.

자동으로 샤드를 확장 및 축소할 수 있음.

### Amazon MSK

Kafka 클러스터의 프로비저닝, 유지 관리, 패치, 모니터링 등을 자동화하여 제공하지만, 사용자는 **Kafka의 다양한 설정을 직접 관리**할 수 있음.


## 성능 및 확장성

### Kinesis Data Streams

**샤드를 통해 수평 확장이 가능**하며, 각 샤드의 용량에 따라 성능이 결정됨. 

실시간 처리에 최적화됨.

### Amazon MSK

**Kafka의 파티션을 통해 수평 확장**이 가능하며, 고성능 데이터 스트리밍을 지원함. 

다양한 배치 및 실시간 처리 요구사항을 충족할 수 있음.


##  생태계 및 도구

### Kinesis Data Streams

AWS에서 제공하는 **Kinesis Firehose, Kinesis Analytics 등과 통합하여 데이터 수집, 처리, 분석을 용이**하게 함.

### Amazon MSK

Kafka의 다양한 오픈소스 도구 및 커뮤니티 지원을 활용할 수 있으며, **Kafka Connect, Kafka Streams 등과 통합**하여 데이터 파이프라인을 구성할 수 있음.

## Summary

|Feature|Kinesis Data Streams|Amazon MSK|
|:---:|:---|:---|
|Message Capacity|1 MB message size limit|1MB default, configure for higher(ex. 10MB)|
|Data Streams|Shards|Kafka Topics with Partition|
|Data Split/Merge|Shard Splitting & Merging|Can only add partitions to a topic|
|TLS Encryption|TLS In-flight encryption|PLAINTEXT or TLS In-flight encryption|
|KMS Encryption|KMS at-rest encryption|KMS at-rest Encryption|
|Data store|x|Can keep data into EBS for a long time|