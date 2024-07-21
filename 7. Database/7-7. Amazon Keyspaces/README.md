# [Amazon Keyspaces](https://docs.aws.amazon.com/keyspaces/latest/devguide/what-is-keyspaces.html)

## <img src = "https://github.com/user-attachments/assets/7030295e-9e91-4af4-b583-181bb7762ade" width = "25" height = "25"> Amazon Keyspaces

Amazon Keyspaces는 **Apache Cassandra와 호환되는 완전 관리형 서버리스 데이터베이스 서비스**임.  

cf. Apache Cassandra: Open-Source NoSQL Distributed database

이를 통해 사용자는 대규모의 애플리케이션을 **쉽게 확장**할 수 있으며, 복잡한 클러스터 관리 작업 없이도 **높은 가용성과 성능을 제공**받을 수 있음.

## 특징

### Apache Cassandra 호환성

Amazon Keyspaces는 **Apache Cassandra의 오픈 소스 쿼리 언어인 CQL** (Cassandra Query Language)과 **완벽하게 호환**됨.  

이를 통해 **기존의 Cassandra 애플리케이션을 쉽게 마이그레이션**할 수 있으며, 추가적인 코드 변경 없이도 사용할 수 있음.

### 완전 관리형 서비스

Keyspaces는 클러스터 관리, 패치, 백업, 복구 등 **데이터베이스 관리 작업을 자동**으로 처리함.  

이는 사용자가 **인프라 관리에 신경 쓰지 않고 애플리케이션 개발에 집중**할 수 있게 함(관리 오버헤드 감소).

### 서버리스 아키텍처  

Keyspaces는 **서버리스 아키텍처로 설계**되어 있어, 사용자가 인프라를 프로비저닝하거나 관리할 필요가 없음.  

대신, **서비스는 자동으로 확장되어 애플리케이션의 요구 사항을 충족**함. 

사용자는 **사용한 만큼만 비용을 지불**하게 됨.

### 높은 가용성과 내구성

Keyspaces는 **여러 AWS 가용 영역에 데이터를 복제하여 높은 가용성과 내구성을 보장**함(테이블을 여러 가용영역에 세번 복제).  

이는 장애 발생 시에도 데이터 접근이 가능하도록 함.

### 확장성

Keyspaces는 **대규모의 데이터와 트래픽을 처리할 수 있도록 설계**됨. 

데이터베이스는 애플리케이션의 트래픽에 따라 자동으로 확장(tables up/down)되어 **수천 TPS (초당 트랜잭션)를 처리**할 수 있음.

### 보안

Keyspaces는 **Amazon VPC**를 통한 네트워크 격리, **AWS Identity and Access Management** (IAM)를 통한 접근 제어, **AWS Key Management Service** (KMS)를 통한 데이터 암호화 등을 통해 데이터 보안을 보장함. 

**데이터 전송 시 TLS**를 사용하여 보안을 강화함.

### 자동 백업 및 복구  

Keyspaces는 **지속적인 백업 기능을 제공**하며, **특정 시점으로의 복구**(Point-in-Time Recovery, ~35일)를 지원함.  

이는 데이터 손실을 최소화하고 데이터베이스를 원하는 시점으로 복원할 수 있게 함.

### Capacity Mode

On-demand mode, Provisioned Mode with Auto-Scaling이 있음.

## Use case

* **IoT 데이터 스토리지**

    수십억 개의 **IoT 장치에서 발생하는 데이터를 실시간으로 수집하고 저장**하는 데 적합함.  

    Keyspaces는 **높은 쓰기 처리량과 확장성을 제공**하여 이러한 데이터를 효율적으로 관리할 수 있음.

* **추천 시스템**

    사용자 행동 데이터를 저장하고, 이를 분석하여 **개인화된 추천을 제공**하는 데 사용될 수 있음.  
    
    Keyspaces의 높은 읽기 및 쓰기 성능은 **실시간 추천 알고리즘**에 적합함.

* **온라인 거래 시스템**  

    **대규모의 트랜잭션 데이터를 빠르게 처리하고 저장하는 데 적합**함. 
    
    Keyspaces는 데이터의 무결성과 일관성을 보장하며, 높은 가용성을 제공함.

* **메시지 서비스**

    대규모의 메시지 데이터를 효율적으로 저장하고 검색하는 데 사용될 수 있음. 
    
    Keyspaces는 메시지의 빠른 삽입과 조회를 지원함.

## Summary

* Amazon Keyspaces는 높은 확장성, 가용성 및 성능을 제공하는 **완전 관리형 서버리스 데이터베이스 서비스**로서, Apache Cassandra와 호환됨.  

* 이를 통해 **대규모의 애플리케이션을 쉽게 확장**할 수 있으며, 복잡한 클러스터 관리 작업 없이도 높은 가용성과 성능을 제공받을 수 있음. 

* Keyspaces는 다양한 사용 사례에 적합하며, 특히 **실시간 데이터 처리가 중요한 애플리케이션에 유리**함.