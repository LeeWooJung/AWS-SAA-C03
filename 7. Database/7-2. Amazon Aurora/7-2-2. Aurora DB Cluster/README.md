# [Aurora DB Cluster](https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.html)

## Aurora DB Cluster

### 설명
* **Amazon Aurora DB 클러스터**는 고가용성, 확장성, 성능 향상을 위한 고유한 아키텍처를 갖추고 있음.  
* 이 아키텍처는 데이터베이스 클러스터, 데이터베이스 인스턴스, 스토리지 계층으로 구성되며, 클라이언트와의 상호작용을 위한 엔드포인트를 제공함.

### 구성 요소

1. **Aurora DB Cluster**  

    * 하나의 Aurora 클러스터는 여러 데이터베이스 인스턴스로 구성됨.  
    * 클러스터는 **[공유 스토리지 계층](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-2.%20Amazon%20Aurora/7-2-1.%20High%20Availability%20for%20Amazon%20Aurora)**을 사용하여 모든 데이터베이스 인스턴스가 동일한 데이터를 공유.  
    * 클러스터 내의 데이터베이스 인스턴스는 **Primary Instance**(쓰기 및 읽기 인스턴스)와 **최대 15개의 읽기 전용 복제본**(Read Replica)으로 구성.

2. **Cluster Volume**

    * 클러스터 볼륨은 **여러 가용 영역**(AZ)에 걸쳐 분산된 공유 스토리지 계층.
    * 데이터는 **6개의 복제본으로 저장**되며, 이는 높은 내구성과 가용성을 보장합니다.
    * 클러스터 볼륨은 자동으로 확장되며, 최대 128TB의 데이터를 저장할 수 있음.

3. **Replication**

    * 데이터 변경 사항은 **비동기적**으로 클러스터 내 모든 읽기 전용 복제본에 복제됨.  
    * 복제는 고성능과 낮은 지연 시간을 유지하면서 데이터를 여러 AZ에 걸쳐 복제하여 고가용성을 보장함.

### Endpoint

1. **Cluster Endpoint**

    * 클러스터 엔드포인트는 클러스터 전체를 나타내는 엔드포인트.
    * 클러스터의 **Primary Instance에 연결**되며, 주로 읽기 및 쓰기 작업을 처리.
    * 클러스터 엔드포인트는 자동 장애 조치를 지원하여 Primary Instance가 장애를 겪을 경우 자동으로 새로운 Primary Instance로 연결됨.

2. **Writer Endpoint**

    * Writer Endpoint는 클러스터의 Primary Instance에 연결됨.
    * 모든 쓰기 작업과 일부 읽기 작업을 처리.
    * Writer Endpoint는 클러스터 내의 유일한 쓰기 엔드포인트로, 데이터의 일관성을 유지함.

3. **Reader Endpoint**

    * Reader Endpoint는 클러스터 내의 모든 읽기 전용 복제본(Read Replica)에 **로드 밸런싱**하여 연결됨.
    * 대규모 읽기 작업 부하를 분산하고 처리하기 위해 사용됨.
    * Reader Endpoint를 사용하면 애플리케이션이 각 읽기 전용 복제본에 개별적으로 연결할 필요 없이 **하나의 엔드포인트로 모든 읽기 작업을 효율적으로 분산**할 수 있음.

#### Cluster Endpoint vs. Writer Endpoint

* **Cluster Endpoint**  
    * **용도**  
    클러스터 엔드포인트는 클러스터의 기본 연결 지점으로, 클러스터 내의 기본 데이터베이스 인스턴스(Primary Instance)에 연결.
    * **기능**  
    주로 읽기 및 쓰기 작업을 처리하며, 기본 인스턴스의 장애 발생 시 자동으로 다른 인스턴스로의 장애 조치를 지원.  
    이는 클러스터 내의 현재 Primary Instance로의 연결을 유지하기 위한 용도로 사용됨.
    * **장점**  
    클러스터 엔드포인트를 사용하면 애플리케이션이 항상 현재의 Primary Instance에 연결되도록 할 수 있어, 클러스터의 상태 변경에 신경 쓸 필요가 없음.

* **Writer Endpoint**
    * **용도**  
    Writer Endpoint는 클러스터의 Primary Instance에만 연결.
    * **기능**  
    모든 쓰기 작업과 일부 읽기 작업을 처리.  
    Writer Endpoint는 Primary Instance로의 직접 연결을 위해 사용됨.
    * **장점**  
    Writer Endpoint를 사용하면 애플리케이션이 직접 쓰기 작업을 수행할 수 있는 인스턴스에 연결됨.

* **Summary**

    * Cluster Endpoint는 클러스터 전체를 대표하는 엔드포인트로, 항상 현재 Primary Instance에 연결.  
    클러스터 내 Primary Instance가 변경되더라도 이 엔드포인트는 유효.
    * Writer Endpoint는 Primary Instance로 직접 연결되며, 주로 쓰기 작업을 처리함.

## High Availability

* **자동 장애 조치** (Automatic Failover)  
Primary Instance가 장애를 겪을 경우, Aurora는 **자동으로 읽기 전용 복제본 중 하나를 새로운 Primary Instance로 승격**시킴.  
이 과정은 일반적으로 **30초 이내에 완료**.

* **다중 AZ에 걸친 복제**  
데이터는 여러 AZ에 걸쳐 복제되므로, 특정 AZ에서 장애가 발생하더라도 데이터 접근이 가능.

* **Cluster Endpoint**  
클러스터 엔드포인트는 자동으로 장애 조치를 처리하여, 클라이언트 애플리케이션이 중단 없이 데이터베이스에 접근할 수 있도록 함.

## Read Scaling

* **읽기 전용 복제본** (Read Replica)  
**최대 15개의 읽기 전용 복제본**을 추가하여 읽기 작업 부하를 분산할 수 있음.  
읽기 전용 복제본은 Primary Instance에서 데이터를 **비동기적**으로 복제받아 읽기 요청을 처리.

* **Reader Endpoint**  
Reader Endpoint는 클러스터 내의 모든 읽기 전용 복제본에 **로드 밸런싱**하여 연결.  
이를 통해 애플리케이션은 하나의 엔드포인트로 모든 읽기 작업을 효율적으로 분산할 수 있음.

* **빠른 읽기 작업**  
Aurora의 공유 스토리지 계층은 읽기 전용 복제본이 동일한 데이터를 빠르게 접근할 수 있도록 하여, 읽기 작업의 성능을 최적화함.

## Architecture

![dbcluster architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/1ac9635f-86c6-43ef-be2c-99757eb0062a)