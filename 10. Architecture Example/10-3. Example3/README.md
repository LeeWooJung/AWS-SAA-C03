# Example 3

## 요구 사항

다음 요구 사항을 만족하는 Big Data Ingestion Pipeline

* Ingestion pipeline이 완전 Serverless 이길 원함.
* Real-time으로 데이터를 수집하기를 원함.
* Data를 변경(transform)하길 원함.
* SQL을 사용하여 변경된 데이터를 Query하길 원함.
* Query 결과로 얻어진 report는 S3에 저장되길 원함.
* 수집된 Data는 warehouse로 load 되고, dashboard를 만들길 원함.

## 아키텍처 구성

### Data Producer

* 데이터를 생성하는 Application, IoT Device 등을 의미함.

### Amazon Kinesis Data Streams

* 실시간으로 데이터를 수집하고 스트림함.
* Data Producer로부터 데이터를 **실시간**으로 수집.

### Amazon Kinesis Data Firehose

* 실시간으로 수집된 데이터를 **S3**로 near real-time으로 전송함.
* Lambda의 도움을 받아 데이터를 변경(transformation)함.

### Amazon S3

* 변환된 데이터를 저장함.
* 데이터가 저장되면 SQS로 알림(Trigger)

### Amazon SQS

### AWS Lambda

* Kinesis Data Firehose를 도와 데이터를 변경(Transformation)함.
* SQS를 구독하고, 데이터를 소비하며 Amazon Athena를 trigger함.

### Amazon Athena

* 주어진 데이터를 쿼리하고, 결과(report)를 S3에 저장함.
* **Serverless SQL Service**임.

### Amazon QuickSight

* 대시보드 생성 및 데이터 시각화를 제공함.
* S3 및 Redshift에 저장된 데이터를 기반으로 대시보드를 생성하고, 시각화를 제공함.

### Amazon Redshift

* **데이터 웨어하우스**로 데이터를 로드 및 저장함.

## 아키텍처

![bigdata ingestion pipeline architecture](https://github.com/user-attachments/assets/95f380bf-4444-471c-a245-da99be468ee9)