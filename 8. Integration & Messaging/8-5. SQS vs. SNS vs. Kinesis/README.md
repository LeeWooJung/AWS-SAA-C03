# SQS vs. SNS. Kinesis

Amazon SQS, SNS, Kinesis는 모두 AWS에서 제공하는 **메시징 및 스트리밍 서비스로, 데이터 전송 및 처리에서 중요한 역할**을 함.  
이들 서비스는 각각 다른 사용 사례와 요구사항에 맞게 설계되었음.

## Amazon SQS (Simple Queue Service)

Amazon SQS는 메시지 큐 서비스로, 애플리케이션 간 메시지를 **비동기적으로 전송하고 처리**하는 데 사용됨.

### 특징

* **Queue Types**: Standard Queue와 FIFO Queue를 제공함.  
* **Message Ordering**: **FIFO Queue에서 순서 보장**, Standard Queue는 순서 보장 없음.
* **Message Delivery**: Standard Queue는 at-least-once, FIFO Queue는 exactly-once.
* **Scalability**: 자동으로 확장됨.
* **Visibility Timeout**: 메시지가 처리 중일 때 다른 소비자가 볼 수 없도록 함.
* **Long Polling**: 메시지가 도착하면 즉시 알림을 받아 처리함.

### 장점

* 메시지 순서와 중복 방지가 필요한 경우 FIFO Queue를 사용함.
* 높은 처리량이 필요한 경우 Standard Queue를 사용함.

### 단점

* 단순 메시지 전달에는 적합하지만, **복잡한 데이터 스트리밍에는 한계**가 있음.

## Amazon SNS (Simple Notification Service)
Amazon SNS는 메시지 전송 및 푸시 알림 서비스로, **여러 구독자에게 동시에 메시지를 전송**할 수 있음.

### 특징

* **Pub/Sub 모델**: 메시지를 주제로 발행하고, 여러 구독자가 메시지를 수신함.
* **Message Delivery**: 여러 전송 프로토콜(SQS, Lambda, HTTP/S, SMS, Email 등)을 지원함.
* **Fan-out**: 하나의 메시지를 여러 수신자에게 동시에 전송할 수 있음.
* **Filtering**: 주제 구독 시 조건에 따라 메시지를 필터링할 수 있음.

### 장점

* 실시간 알림 및 브로드캐스트 메시지에 적합함.
* 다양한 프로토콜을 통한 메시지 전송 지원.

### 단점

* 메시지 순서를 보장하지 않음.
* 복잡한 데이터 스트리밍에는 적합하지 않음.

## Amazon Kinesis

Amazon Kinesis는 실시간 데이터 **스트리밍 서비스로, 대규모 스트리밍 데이터를 수집, 처리, 분석**할 수 있음.

### 특징

* **Kinesis Data Streams**: 실시간 데이터 스트리밍을 위한 서비스.
* **Kinesis Data Firehose**: 데이터를 실시간으로 로드하는 서비스.
* **Kinesis Data Analytics**: 스트리밍 데이터를 실시간으로 분석하는 서비스.
* **Capacity Mode**: 온디맨드 및 프로비저닝된 용량 모드 제공.
* **Ordering**: 샤드 내에서는 순서를 보장함.

### 장점

* 실시간 데이터 처리 및 분석에 적합함.
* 대규모 스트리밍 데이터의 수집과 처리가 가능함.
* 스트리밍 데이터의 순서를 보장함.

### 단점

* 설정 및 운영이 비교적 복잡함.
* 다른 메시징 서비스에 비해 **비용이 높을 수 있음**.

## Summary

||SQS|SNS|Kinesis|  
|:---:|:---|:---|:---|
|데이터|Consumer가 Pull|Publish/Subscribe|Consumer Pull 혹은 Fan-out|
|메시지 순서 보장|FIFO Queue에서 순서 보장|순서 보장하지 않음|샤드 내에서 순서 보장|  
|확장성|자동 확장|자동 확장|샤드 단위로 수동 확장|  
|Use case|비동기 작업 처리, 작업 큐|알림, 브로드캐스트 메시지|실시간 데이터 스트리밍 및 분석|  
|전송 프로토콜|메시지 큐|HTTP/S, SQS, Lambda, SMS, Email 등|스트리밍 데이터|
