# [Amazon OpenSearch](https://docs.aws.amazon.com/ko_kr/opensearch-service/latest/developerguide/what-is.html)

## <img src = "https://github.com/user-attachments/assets/54d16903-477a-4fad-9cf6-8345a3321299" width = "25" height = "25"> Amazon OpenSearch

Amazon OpenSearch는 Elasticsearch 및 Kibana 혹은 Opensearch 대시보드를 기반으로 하는 **관리형 서비스**로, **실시간 로그 분석, 검색, 모니터링, 데이터 시각화 등의 작업**을 수행할 수 있는 플랫폼임. 

기존의 **Amazon Elasticsearch Service를 대체**하며, 다양한 데이터 소스에서 데이터를 수집, 인덱싱, 분석, 시각화할 수 있음.

OpenSearch를 이용하면 primary key 혹은 index만을 이용해 쿼리하는 DynamoDB와 달리 **어떤 field든 찾을 수 있고, 부분적으로 일치하는 부분 조차도 찾을 수 있음**.

OpenSearch를 다른 Database를 보충하는 용도로 사용하는 것이 흔함.

두 가지 모드를 제공함(**managed cluster, serverless cluster**)

SQL을 지원하지는 않지만 plugin을 통해서 사용할 수 있음.

## 특징

### 실시간 데이터 처리

**실시간 로그, 지표, 이벤트 데이터를 수집하고 분석**할 수 있음(AWS IoT, Kinesis Data Firehose, CloudWatch Logs).

### 분산 아키텍처

**데이터 분산 저장 및 분산 검색을 지원**하여 확장성이 높음.

### 강력한 검색 기능

복잡한 쿼리, 필터링, 집계 작업을 효율적으로 수행할 수 있음.

### 보안 기능

**IAM 정책 & Cognito, VPC 지원, TLS 암호화, AWS KMS** 통합 등의 다양한 보안 옵션을 제공함.

### 데이터 시각화

Kibana 혹은 OpenSearch 대시보드를 사용하여 데이터의 시각화 및 대시보드를 쉽게 생성할 수 있음.

## 구성요소

* **도메인**

    OpenSearch 클러스터의 논리적 단위로, 하나 이상의 OpenSearch 노드를 포함함.

* **노드**

    **데이터를 저장하고 검색 요청을 처리하는 단위**임.  
    
    마스터 노드, 데이터 노드, 클라이언트 노드로 나눌 수 있음.

* **인덱스**

    데이터를 **저장하는 구조적 단위**로, RDBMS의 테이블과 유사함.

* **샤드**

    **인덱스를 분산 저장하기 위한 단위**로, 각 샤드는 독립적인 인덱스로 동작함.

* **복제본**

    고가용성과 데이터 보호를 위해 샤드의 복사본을 유지함.

## 아키텍처

Amazon OpenSearch는 **다중 노드 클러스터 아키텍처를 채택**하여 **데이터 분산 저장 및 처리, 고가용성, 확장성**을 보장함. 

사용자는 도메인을 생성하고, 데이터와 메타데이터를 인덱싱하며, OpenSearch 노드를 통해 검색 및 분석 작업을 수행함. 

Kibana 혹은 OpenSearch 대시보드를 통해 데이터를 시각화할 수 있음.

## Architecture Example

### with CloudWatch Logs

![Opensearch with CloudWatchLogs](https://github.com/user-attachments/assets/0646f171-898d-458a-ae49-9ad15826976a)

### with DynamoDB

![OpenSearch with DynamoDB architecture](https://github.com/user-attachments/assets/54d59555-1473-4c57-9040-6d447eeae60c)

### with Kinesis Family

![OpenSearch with Kinesis architecture](https://github.com/user-attachments/assets/46b2714c-48ec-49fb-ada1-dd84a7474a2f)

## 장점

* **관리형 서비스**

    AWS에서 **인프라 관리 및 유지보수를 담당하여 사용자는 데이터 분석에 집중**할 수 있음(운영 오버헤드 감소).

* **확장성**

    자동 스케일링을 통해 수요에 맞게 리소스를 조정할 수 있음.

* **보안**

    VPC 지원, IAM 정책, TLS 암호화 등을 통해 데이터 보안을 강화함.

* **통합성**

    **다양한 AWS 서비스와 쉽게 통합**할 수 있어 데이터 수집 및 분석이 용이함.

## 단점

* **비용**

    대규모 데이터 처리 시 비용이 증가할 수 있음.

* **복잡성**

    고급 기능을 활용하려면 OpenSearch 및 Kibana에 대한 깊은 이해가 필요함.

* **제한된 제어**

    완전한 제어권이 필요한 사용자에게는 제한적일 수 있음.

## Use case

* **로그 분석**

    서버 로그, 애플리케이션 로그, 보안 로그 등의 실시간 분석.

* **데이터 검색**

    전자상거래 사이트의 제품 검색, 문서 검색, 메타데이터 검색 등.

* **보안 모니터링**

    보안 이벤트 및 지표 모니터링, 침입 탐지 시스템.

* **운영 모니터링**

    시스템 성능 모니터링, 애플리케이션 성능 분석, 실시간 대시보드 생성.


## Summary

Amazon OpenSearch는 **실시간 로그 분석, 검색, 데이터 시각화** 등을 위한 강력한 관리형 서비스임.

높은 **확장성과 다양한 보안 옵션**을 제공하며, **AWS 서비스와의 원활한 통합**을 통해 데이터 수집 및 분석을 용이하게 함. 

OpenSearch의 **분산 아키텍처와 Kibana 혹은 OpenSearch 대시보드같은 시각화 도구**를 통해 다양한 사용 사례에 적용 가능함.