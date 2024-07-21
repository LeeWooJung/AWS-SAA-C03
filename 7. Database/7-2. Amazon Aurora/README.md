# [Amazon Aurora](https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)

## Amazon Aurora

### 설명
* **Amazon Aurora**는 Amazon Web Services(AWS)에서 제공하는 **관계형 데이터베이스** 서비스로, MySQL 및 PostgreSQL과 호환되는 고성능, 고가용성 데이터베이스를 제공함(Not open source).  
* Amazon Aurora는 AWS의 완전 관리형 데이터베이스 서비스인 **[Amazon RDS](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-1.%20Amazon%20RDS)** 에서 운영됨.

### 특징

1. **고성능 및 확장성**  
    * **높은 성능**  
    Amazon Aurora는 일반 MySQL 데이터베이스보다 최대 5배, PostgreSQL 데이터베이스보다 최대 3배 빠른 성능을 제공.
    * **자동 확장**  
    **스토리지는 10GB에서 최대 128TB까지 자동으로 확장**됨.  
    사용자가 스토리지 용량을 미리 계획할 필요가 없음.

2. **고가용성 및 내구성**

    * **다중 AZ 배포**  
    기본적으로 다중 가용 영역(AZ)에 걸쳐 데이터를 복제하여 장애 발생 시에도 자동으로 장애 조치(failover)를 수행(High Availability Native).
    * **자동 백업 및 스냅샷**  
    데이터베이스를 자동으로 백업하고 사용자가 원할 때 언제든지 복구할 수 있음.
    * **데이터 무결성**  
    Aurora는 데이터를 6개 복제본(across 3 AZ)으로 유지하며, 손실된 데이터 블록을 자동으로 복구.
    * **Cross Region Replication 가능**

3. **호환성**

    * **MySQL 및 PostgreSQL 호환**  
    MySQL 및 PostgreSQL과 호환되므로 기존의 애플리케이션을 거의 수정하지 않고도 Amazon Aurora로 마이그레이션할 수 있음.

4. **보안**

    * **암호화**  
    데이터는 전송 중 및 저장 중에 자동으로 암호화됨.
    * **네트워크 격리**  
    VPC(Virtual Private Cloud)를 사용하여 네트워크를 격리할 수 있음.
    * **IAM 통합**  
    AWS Identity and Access Management(IAM)과 통합되어 세분화된 액세스 제어를 제공함.

5. **무중단 패치**

    * **자동 패치**    
    Amazon Aurora는 데이터베이스 인스턴스를 최신 상태로 유지하기 위해 자동으로 패치를 적용.  
    관리자는 패치 적용을 위한 유지 보수 창을 설정할 수 있으며, Aurora는 설정된 창 내에서 패치를 수행함.

    * **관리 편의성**  
    패치가 자동으로 적용되므로 관리자는 수동으로 패치를 관리할 필요가 없음.  
    이는 특히 대규모 데이터베이스 환경에서 유용.

    * **무중단 업그레이드**  
    Amazon Aurora는 대부분의 패치를 무중단으로 적용할 수 있음.  
    이는 Aurora의 아키텍처 덕분에 가능한데, **Aurora는 스토리지와 컴퓨팅 리소스를 분리**하여 업데이트를 적용할 수 있기 때문.

    * **연속적인 가용성**  
    데이터베이스가 계속 작동하면서 백그라운드에서 패치가 적용됨.  
    따라서 애플리케이션의 가용성이 유지되고, 사용자는 서비스 중단을 경험하지 않음.

### 아키텍처

Amazon Aurora의 아키텍처는 성능과 내구성을 극대화하기 위해 설계됨.

1. **스토리지 계층**

    * **분산형 스토리지**  
    Aurora 스토리지는 다중 AZ에 걸쳐 분산되어 있으며, 각 AZ에 2개의 복제본을 저장.
    * **일관성 있는 성능**  
    Aurora는 쓰기 작업을 병렬로 수행하여 성능을 향상시키고, 자동으로 데이터 복구 및 복제본 관리를 수행.

2. **데이터베이스 계층**

    * **읽기 전용 복제본**  
    여러 읽기 전용 복제본을 추가하여 읽기 성능을 확장할 수 있음.  
    읽기 전용 복제본은 읽기 성능을 확장하고, 읽기 요청을 분산함.
    * **자동 장애 조치**  
    기본 인스턴스에 장애가 발생하면 자동으로 읽기 전용 복제본 중 하나를 기본 인스턴스로 승격하여 중단 시간을 최소화.

### Use Case

* **웹 및 모바일 애플리케이션**  
고성능과 확장성이 요구되는 웹 및 모바일 애플리케이션에 적합.  
예를 들어, 전자 상거래 사이트, 게임 애플리케이션 등이 있음.
* **엔터프라이즈 애플리케이션**  
ERP, CRM, 금융 시스템 등 트랜잭션이 많은 엔터프라이즈 애플리케이션에 적합.
* **분석 및 보고**  
실시간 분석 및 보고 기능이 필요할 때, Amazon Aurora의 빠른 읽기 성능을 활용할 수 있음.
* **백엔드 데이터베이스**  
마이크로서비스 아키텍처에서 각 서비스가 독립적인 데이터베이스를 필요로 할 때, Aurora의 자동 확장성과 관리형 서비스를 활용할 수 있음.

### 관리 및 운영

* **자동화된 관리**  
AWS Management Console, AWS CLI, RDS API를 통해 Amazon Aurora를 쉽게 관리할 수 있음.
* **모니터링 및 로깅**  
Amazon CloudWatch를 사용하여 성능 메트릭과 로그를 모니터링할 수 있음.  
AWS CloudTrail을 통해 API 호출을 로깅할 수 있음.
* **자동 패치 및 업데이트**  
Amazon Aurora는 자동으로 데이터베이스 소프트웨어를 최신 버전으로 업데이트함.

### 장점 및 단점

1. **장점**

    * 높은 성능과 확장성
    * 자동화된 관리 및 운영
    * 고가용성과 내구성
    * MySQL 및 PostgreSQL과의 호환성
    * 강력한 보안 기능

2. **단점**

    * **사용 비용**  
    다른 데이터베이스 솔루션에 비해 비용이 높을 수 있음
    * **벤더 종속성**  
    AWS 환경에 종속적이므로 다른 클라우드로의 이동이 어려울 수 있음

### Summary

* Amazon Aurora는 **고성능, 고가용성, 확장성이 필요한 관계형 데이터베이스 워크로드에 매우 적합한 솔루션**.  
* 특히, MySQL 및 PostgreSQL과의 호환성을 제공하므로 기존 애플리케이션을 쉽게 마이그레이션할 수 있으며, **자동화된 관리 기능**을 통해 데이터베이스 운영을 단순화할 수 있음.  
* Amazon Aurora를 사용함으로써 데이터베이스 성능을 극대화하고, 관리 부담을 줄이며, 비즈니스 로직에 집중할 수 있는 환경을 제공받을 수 있음.

* PosgreSQL, MySQL 과 호환 가능. 스토리지와 Compute 분리 가능.

* **Storage**: 6개의 replicas가 3개의 AZ에 걸쳐 데이터를 저장. Highly Available, Self-Healing, Auto-Scaling

* **Compute**: Multiple AZ에 걸친 Cluster DB Instance, Read Replicas의 Auto Scaling.

* **Cluster**: Writer, Reader DB Instance를 위한 Custom Endpoints.

* RDS와 같은 Security, Monitoring, Maintenance 특징.

* **Serverless**: unpredictable, intermittent 워크로드 혹은 capacity planning이 없는 것에 적합.

* **Aurora Global**: 각 Region에 최대 16개의 DB Read Instances 가능, 1초 이내에 replication 가능.

* **Aurora Machine Learning**: **SageMaker**, **Comprehend on Aurora**를 사용하여 Machine Learning 가능.

* **Aurora Database Cloning**: Snapshot 복원보다 빠름. 존재하는 Cluster로부터 새로운 Cluster 복제.