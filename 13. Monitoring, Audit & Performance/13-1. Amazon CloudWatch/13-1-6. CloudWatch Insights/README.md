# [CloudWatch Insights](https://docs.aws.amazon.com/ko_kr/AmazonCloudWatch/latest/logs/AnalyzingLogData.html)

Amazon CloudWatch Insights는 AWS에서 제공하는 **로그 데이터 분석 서비스**임. 

이는 대규모 **로그 데이터를 실시간으로 분석하고 쿼리할 수 있게 해주는 서비스**로, 운영 문제를 빠르게 해결하고 애플리케이션 성능을 모니터링하며 보안 문제를 탐지하는 데 도움을 줌.

이를 통해 특정 이벤트를 찾거나, 패턴을 분석하거나, 로그 데이터를 시각화할 수 있음.

## 특징

### 강력한 쿼리 언어

로그 데이터를 **필터링, 집계, 정렬, 변환할 수 있는 강력한 쿼리 언어를 제공**함.

### 실시간 분석

로그 데이터를 실시간으로 분석하여 문제를 빠르게 식별하고 해결할 수 있음.

### 시각화

**쿼리 결과를 차트로 시각화**하여 로그 데이터를 직관적으로 이해할 수 있음.

### 저비용

**필요한 로그 데이터를 쿼리한 양에 따라 비용이 청구되므로 비용 효율적**임.

### 통합

CloudWatch 대시보드 및 경고와 통합하여 로그 기반 모니터링 및 경고를 설정할 수 있음.

## 구성요소

* **로그 그룹**(Log Group)

    관련된 로그 스트림의 모음으로, 애플리케이션이나 시스템의 로그 데이터를 논리적으로 그룹화함.

* **로그 스트림**(Log Stream)

    특정 소스에서 생성된 로그 이벤트의 순차적 모음임.

* **쿼리**(Query)

    로그 데이터를 검색하고 분석하기 위해 작성된 명령어 집합임.

* **시각화 차트**

    쿼리 결과를 그래프로 시각화하여 로그 데이터를 분석하고 모니터링할 수 있음.

## 아키텍처

### 로그 수집

애플리케이션 및 인프라에서 생성된 로그 데이터는 CloudWatch 로그 그룹으로 수집됨.

### 로그 저장

로그 데이터는 로그 스트림으로 저장되어 필요할 때 쿼리할 수 있음.

### 쿼리 실행

**사용자는 CloudWatch Insights 콘솔에서 쿼리를 작성하고 실행**함.

### 결과 분석

쿼리 결과는 텍스트 형식으로 표시되거나 시각화 차트로 변환됨.

### 인사이트 도출

**분석된 로그 데이터를 통해 애플리케이션 및 시스템의 성능, 보안, 운영 문제를 파악**함.

## Containers Insights

Containers로 부터 생성된 Metrics, Logs를 수집, 통합, 요약함.

### 가능한 Containers

* **Amazon Elastic Container Service**(Amazon ECS)

* **Amazon Elastic Kubernetes Services**(Amazon EKS)

* **Kubernetes platforms on EC2**

* **Fargate**(ECS, EKS)

* 등등

Amazon EKS, Kubernetes에서 CloudWatch Insights는 Container를 찾기 위해 CloudWatch Agent의 **Containerized Version**을 사용함.

## Lambda Insights

AWS Lambda에서 실행되는 **서버리스** 애플리케이션의 모니터링, 트러블슛팅.

CPU time, Memory, Disk, Network를 포함한 시스템 메트릭을 요약, 수집, 통합함.

Cold Start, Lambda Worker Shutdown과 같은 진단 정보를 수집, 통합, 요약함.

이런 **Lambda Insight**는 Lambda Layer에 제공됨.

## Contributor Insights

Contributor 데이터를 찾기 위해 로그 데이터를 분석하고 **타임시리즈**를 만듦.

이를 통해 **Top-N** Contributors Metrics를 찾을 수 있고, 시스템 성능에 어떤 것이 영향을 미치고 있는지 확인할 수 있음.

모든 **AWS-generated Logs**(VPC, DNS 등)에서 작동함.

초기에 사용자 정의 규칙을 생성하거나 AWS에서 제공하는 규칙을 적용할 수 있음.

### 아키텍처 예시

VPC Flow Logs를 CloudWatch Logs로 전송함.

이를 CloudWatch Contributor Insights에서 쿼리하여 분석함.

이를 통해 Heaviest Network User 등을 확인할 수 있음.

## Application Insights

애플리케이션을 모니터링하여 잠재적 문제를  보여주는 자동화된 **대시보드**를 생성할 수 있음.

**SageMaker**에 의해 작동함.

애플리케이션에서의 문제점을 대시보드로 시각화하여 문제 해결 시간을 극단적으로 줄여줄 수 있음.

문제 요소 혹은 그에 대한 알람은 **Amazon EventBridge**와 **SSM OpsCenter**로 전송될 수 있음.


## 장점

* **실시간 로그 분석**

    로그 데이터를 실시간으로 분석하여 신속하게 문제를 파악하고 해결할 수 있음.

* **비용 효율성**

    필요한 로그 데이터만 쿼리하므로 비용을 절감할 수 있음.

* **강력한 쿼리 기능**

    복잡한 쿼리를 작성하여 로그 데이터를 세밀하게 분석할 수 있음.

* **AWS 서비스 통합**

    CloudWatch 대시보드, 경고, Lambda 함수 등과 통합하여 강력한 모니터링 및 자동화 기능을 제공함.

* **시각화 도구**

    쿼리 결과를 시각적으로 표현하여 로그 데이터를 쉽게 이해할 수 있음.

## 단점

* **쿼리 비용**

    대규모 로그 데이터를 쿼리할 때 비용이 증가할 수 있음.

* **제한된 로그 보관 기간**

    로그 데이터를 장기 보관하려면 별도의 설정이 필요할 수 있음.

## Use case

* **애플리케이션 디버깅**

    애플리케이션에서 발생한 오류를 신속하게 찾아 디버깅할 수 있음.

* **운영 모니터링**

    시스템 성능을 모니터링하고 운영 문제를 실시간으로 탐지할 수 있음.

* **보안 분석**

    로그 데이터를 분석하여 보안 이벤트를 탐지하고 대응할 수 있음.

* **비용 최적화**

    리소스 사용량 및 성능 데이터를 분석하여 비용을 최적화할 수 있음.

## Summary

Amazon CloudWatch Insights는 AWS에서 제공하는 강력한 로그 데이터 분석 서비스임. 

로그 데이터를 **실시간으로 쿼리하고 분석할 수 있으며, 이를 통해 애플리케이션 및 인프라의 문제를 빠르게 해결하고 성능을 모니터링**할 수 있음. 

강력한 쿼리 언어와 시각화 도구를 제공하여 로그 데이터를 효과적으로 분석할 수 있으며, AWS 서비스와 통합되어 강력한 모니터링 및 자동화 기능을 제공함.