# [AWS RDS Read Replicas](https://aws.amazon.com/ko/rds/features/read-replicas/)

## AWS RDS Read Replicas

### 설명

* Amazon RDS의 **Read Replica**는 데이터베이스 성능을 확장하고 읽기 작업을 분산 처리하기 위한 기능.  
* Read Replica를 사용하면 주 데이터베이스 인스턴스에서 데이터 변경 사항을 **비동기적으로 복제**하여 **읽기 전용 복제본을 생성**할 수 있음.  
따라서 주로 읽기 작업이 많은 환경에서 유용하게 사용됨.

### Use Case

* **읽기 확장**  
애플리케이션이 높은 읽기 요청을 처리해야 할 때, Read Replica를 사용하여 읽기 요청을 분산시킬 수 있음.  
이를 통해 주 데이터베이스 인스턴스의 부하를 줄이고 전체 시스템의 성능을 향상시킬 수 있음.

* **데이터 분석**  
실시간으로 운영되는 **주 데이터베이스에 영향을 주지 않으면서** 데이터 분석을 수행할 수 있음.  
분석 작업은 주로 읽기 작업이므로 Read Replica에서 데이터를 읽어 분석을 수행하면 됨.

* **백업 및 복구**  
주 데이터베이스 인스턴스에서 직접 백업을 수행하는 대신, **Read Replica를 사용하여 백업 작업을 수행**함으로써 주 데이터베이스의 성능에 미치는 영향을 최소화할 수 있음.

* **지리적 분산**  
다른 지역에서 읽기 전용 데이터를 제공해야 하는 경우, Read Replica를 **다른 리전**(Region)에 생성하여 지리적으로 분산된 사용자를 지원할 수 있음. 그러나 이 때는 **많은 비용이 듦**.

### 제약 사항

* Read Replica는 비동기적으로 복제되므로, 주 데이터베이스와 약간의 지연이 발생할 수 있음.  
* 읽기 전용이기 때문에 쓰기 작업은 지원되지 않음.  
    - SQL에서 SELECT문만 사용할 수 있다고 생각하면 됨.
* **최대 5개**의 Read Replica를 생성할 수 있음.

### 비용

* 같은 Region, 다른 AZ : Free
* 다른 Region(Cross-Region) : Cost 많이 듦.

## RDS Replica Promotion

### 설명

* Amazon RDS의 Read Replica는 기본적으로 읽기 전용 데이터베이스 인스턴스로, 주로 읽기 작업의 부하를 분산시키고 데이터베이스의 성능을 향상시키기 위해 사용됨.  
* 그러나 특정 상황에서는 Read Replica를 **독립적인 데이터베이스(DB) 인스턴스로 프로모션**(promote)하여, **쓰기 작업도 수행**할 수 있는 새로운 주(primary) 데이터베이스로 만들 수 있음.

### 사용

1. **장애 복구**(Disaster Recovery)

    * 주 데이터베이스 인스턴스에 장애가 발생했을 때, Read Replica를 **프로모션**하여 새로운 주 데이터베이스로 사용할 수 있음.

2. **데이터베이스 마이그레이션**(Database Migration)

    * 기존 데이터베이스에서 새로운 데이터베이스로의 마이그레이션 과정에서 Read Replica를 프로모션하여 **최소 다운타임으로 데이터베이스 전환을 수행**할 수 있음.

3. **데이터베이스 업그레이드**

    * 데이터베이스 엔진의 버전 업그레이드를 위해 Read Replica를 생성하고, 업그레이드 후 프로모션하여 새로운 버전의 주 데이터베이스로 전환할 수 있음.

## Read Replica Use case Architecture
![Read Replica Use Case Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/107fed6d-c754-4c4c-8e4b-06f12ea2a005)

## Read Replica simple Architecture

![Read Replica multi architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/a6f954c5-b597-496d-beb5-48f84cbff17e)
