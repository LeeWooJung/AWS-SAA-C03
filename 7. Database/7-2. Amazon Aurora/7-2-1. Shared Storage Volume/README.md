# [Shared Storage Volume](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.StorageReliability.html)

* Amazon Aurora는 높은 성능과 안정성을 제공하기 위해 **공유 스토리지 볼륨**을 활용.  
* **공유 스토리지 볼륨**  
데이터베이스 인스턴스가 데이터를 저장하고 액세스하는 데 사용되는 분산된 스토리지 계층.  
* 이 공유 스토리지 볼륨은 복제, 자가 치유, 자동 확장과 같은 중요한 기능을 지원하며, 이는 고가용성(High Availability)과 읽기 확장성(Read Scaling) 측면에서 매우 유용.

## Shared Storage Volume

1. **Replication** (복제)

    * **6-Way Replication**  
    Aurora는 데이터를 여러 가용 영역(AZ)에 걸쳐 **6개의 복제본으로 저장**.  
    이로 인해 데이터 손실의 위험이 크게 줄어들고 데이터 접근 속도가 향상됨.
    * **Asynchronous and Synchronous Replication**  
    Aurora는 **쓰기 작업을 동기적**으로 복제하여 데이터 일관성을 보장하며, **읽기 복제본으로 비동기적으로 데이터를 복제**하여 높은 읽기 성능을 유지.

2. **Self Healing** (자가 치유)

    * **자동 복구**  
    스토리지 노드에서 오류가 발생하면 Aurora는 자동으로 오류를 감지하고 데이터의 손상된 복제본을 다른 정상 복제본으로 대체.
    * **정기적 검증 및 수리**  
    Aurora는 **데이터 무결성**을 보장하기 위해 주기적으로 데이터를 검증하고 필요한 경우 복구 작업을 수행.

3. **Auto Expanding** (자동 확장)

    * **자동 스토리지 확장**  
    Aurora의 스토리지는 수요에 따라 자동으로 확장.  
    초기 설정 없이 필요할 때마다 스토리지 용량이 증가하므로, 사용자는 용량 문제를 신경 쓸 필요가 없음.
    * **최대 128TB 지원**  
    Aurora의 스토리지는 최대 128TB까지 확장 가능하며, 이는 대규모 데이터베이스 운영에도 충분한 용량을 제공.

Amazon Aurora는 **공유 스토리지 볼륨**을 통해 복제, 자가 치유, 자동 확장을 지원함으로써 고가용성과 읽기 확장성을 제공.  
이를 통해 Aurora는 데이터베이스의 연속적인 가용성과 높은 읽기 성능을 유지하면서도 데이터 무결성을 보장.  
이러한 기능들은 대규모 데이터베이스 운영 및 다양한 비즈니스 요구 사항을 효율적으로 처리할 수 있도록 설계되었음.

## Architecture
![high availability architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/a6702170-6e33-48c0-a04e-bae0b0000d77)