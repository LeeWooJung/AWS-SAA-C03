# [Hard Disk Drives](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html#vol-type-hdd)

## Hard Disk Drives

### 설명

**Boot Volume으로 사용될 수 없음**.

Amazon EBS의 Hard Disk Drive(HDD) 볼륨 유형에는 **Throughput Optimized HDD (st1)** 과 **Cold HDD (sc1)** 가 있음. 이들은 다음과 같은 특성과 사용 사례를 가지고 있음

* **Throughput Optimized HDD (st1)**  
빈번하게 접근되는 처리량 집약적 워크로드에 적합한 저비용 HDD로 설계되었음.  
빅 데이터, 데이터 웨어하우스, 로그 처리와 같은 대규모 스트리밍 워크로드에 이상적임.
* **Cold HDD (sc1)**  
자주 액세스하지 않는 워크로드에 적합한 가장 저렴한 HDD로, 스토리지 비용을 최대한 낮추어야 하는 시나리오에 최적임.  
이 HDD 볼륨들은 SSD 볼륨에 비해 낮은 비용으로 높은 처리량을 제공하지만, IOPS 성능은 낮음. 순차적인 읽기/쓰기 작업이 많은 워크로드에 적합하며, 랜덤 읽기/쓰기 작업이 많은 워크로드에는 권장되지 않음.