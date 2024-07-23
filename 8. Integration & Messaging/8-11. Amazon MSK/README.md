# [AWS MSK](https://aws.amazon.com/ko/msk/)

## <img src = "https://github.com/user-attachments/assets/307d80d0-4ba0-4fd8-b8d8-824a827b334f" width = "30" height = "30"> AWS Managed Streaming for Apache Kafka

Amazon Managed Streaming for Apache Kafka (MSK)는 **Apache Kafka를 쉽게 실행하고 확장할 수 있도록 완전 관리형으로 제공하는 서버리스 서비스**임. 

* Cluster를 생성, 업데이트, 삭제할 수 있게 해줌.

* MSK는 Kafka broker nodes를 생성 및 관리하고, Zookeeper nodes를 생성 및 관리해줌.

* MSK Cluster를 VPC 내에 **Multi-AZ**에 배포함(가용성을 위해 최대 3개까지 가능)

* Apache Kafka의 failure로부터 자동으로 회복해줌.

* **EBS Volumes**에 데이터를 저장할 수 있음.

[Amazon Kinesis](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-4.%20AWS%20Kinesis)를 대체할 수 있음.

Kafka는 **실시간 데이터 스트리밍을 위한 분산형 메시징 시스템으로 널리 사용**되고 있음.

## 특징

### 완전 관리형

클러스터 프로비저닝, 유지 관리, 자동 패치, 모니터링 등을 자동으로 처리함(운영 오버헤드 감소).

### 확장성 & 서버리스

데이터 스트림의 양에 따라 자동으로 확장 가능함.

### 고가용성

여러 가용 영역에 걸쳐 클러스터를 배포하여 고가용성을 보장함.

### 보안

**VPC 네트워크 통합, AWS IAM을 통한 접근 제어, 데이터 암호화** 등의 보안 기능 제공.

## 구성요소

* **브로커**

    Kafka 클러스터를 구성하는 개별 서버. **데이터 스트림을 처리하고 저장**함.

* **토픽**

    **데이터가 저장되는 카테고리 또는 피드**. 
    
    각 토픽은 여러 파티션으로 나눌 수 있음.

* **파티션**

    토픽 내에서 **데이터를 분산 저장**하는 단위. 
    
    파티션은 **데이터를 분산 처리하여 성능을 향상**시킴.

* **프로듀서**

    데이터를 Kafka 토픽에 게시하는 역할.

* **컨슈머**

    Kafka 토픽에서 데이터를 읽어가는 역할.

* **Zookeeper**

    Kafka **클러스터의 상태를 관리하고, 브로커 간의 메타데이터를 조정**하는 역할.

## 아키텍처

### 데이터 프로듀서

로그, 이벤트, IoT 데이터 등 **다양한 소스에서 데이터를 Kafka 브로커에 전송**함.

### Kafka 브로커

데이터를 **토픽에 저장하고, 필요한 경우 데이터를 파티셔닝**함.

### Zookeeper

클러스터 상태 관리 및 조정.

### 데이터 컨슈머

데이터를 Kafka 브로커에서 읽어가며 실시간 처리 및 분석을 수행함.

## 장점

* **간편성**

    클러스터 관리가 자동화되어 운영 부담이 줄어듦.

* **확장성**

    데이터 양과 처리량에 따라 자동으로 확장 가능.

* **안정성**

    고가용성과 내구성을 제공하여 안정적인 데이터 스트리밍 가능.

* **보안**

    네트워크 통합, 접근 제어, 데이터 암호화 등의 강력한 보안 기능 제공.

## 단점

* **비용**

    관리형 서비스로서 비용이 발생하며, 데이터 양이 많아질수록 비용이 증가할 수 있음.

* **제한된 사용자 설정**

    관리형 서비스 특성상 일부 Kafka 설정에 대한 사용자 제어가 제한적임.

## Use case

* **실시간 로그 분석**

    서버 로그, 애플리케이션 로그를 실시간으로 수집, 처리하여 모니터링 및 분석함.

* **IoT 데이터 처리**

    IoT 장치에서 발생하는 데이터를 실시간으로 수집, 분석하여 상태 모니터링 및 예측 유지보수 수행.

* **이벤트 스트리밍**

    사용자 활동 데이터를 실시간으로 수집, 분석하여 맞춤형 추천 및 마케팅 전략 수립.

## Architecture Example

### MSK general architecture(Apache Kafka)

![msk cluster architecture](https://github.com/user-attachments/assets/6255d731-f728-47b5-ad40-4bd962f809ab)

### MSK Consumers

![msk consumer architecture](https://github.com/user-attachments/assets/a13e710a-b94e-4564-af77-10e4527b6d7f)

## Sumamry

Amazon MSK는 **Apache Kafka를 완전 관리형으로 제공하는 서비스**로, **데이터 스트리밍을 쉽게 실행하고 확장**할 수 있게 함.

주요 특징으로는 **자동 관리, 확장성, 고가용성, 보안** 등이 있으며, 구성 요소로는 브로커, 토픽, 파티션, 프로듀서, 컨슈머, Zookeeper가 있음. 

**간편한 관리와 높은 안정성을 제공하지만, 비용과 일부 설정 제약이 단점**으로 작용할 수 있음.

실시간 로그 분석, IoT 데이터 처리, 이벤트 스트리밍 등 다양한 사용 사례에서 활용 가능함.






