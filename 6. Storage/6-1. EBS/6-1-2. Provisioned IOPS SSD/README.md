# [Provisioned IOPS SSD](https://docs.aws.amazon.com/ebs/latest/userguide/provisioned-iops.html)

## Provisioned IOPS SSD

### 설명

Provisioned IOPS SSD 볼륨은 Amazon EBS의 가장 높은 성능을 자랑하는 스토리지 볼륨으로, **낮은 지연 시간이 필요한 중요하고 IOPS 집약적이며 처리량 집약적인 워크로드를 위해 설계**되었음.  
이 볼륨은 Amazon EBS io2 Block Express 볼륨으로, 2021년부터 사용 가능해졌으며, 볼륨 당 최대 256,000 IOPS와 4,000 MB/s의 처리량을 제공함으로써, 일반 목적 볼륨보다 4배 더 많은 IOPS를 제공함.

Provisioned IOPS SSD 볼륨은 99.999%의 높은 내구성과 0.001% 이하의 연간 장애율을 가지며, 이는 **1년 동안 실행되는 볼륨 10만 개당 1건의 볼륨 장애가 발생함을 의미**함.  

이러한 특성으로 인해, Provisioned IOPS SSD 볼륨은 **SAP HANA, Oracle, Microsoft SQL Server, IBM DB2**와 같은 성능 집약적이고 비즈니스에 중요한 애플리케이션에 이상적임.  
또한, 이 볼륨은 I/O 펜싱을 지원하는 **Multi-Attach** 기능을 통해, 하나의 io2 Block Express 볼륨을 동일한 가용성 영역 내의 최대 16개의 Nitro 기반 EC2 인스턴스에 연결할 수 있음.

성능이나 내구성 요구 사항이 덜 엄격한 애플리케이션의 경우, General Purpose SSD를 사용하는 것이 좋음.

### 특성

* **사용 사례**  
Provisioned IOPS SSD 볼륨은 지연 시간에 민감한 트랜잭션 워크로드에 이상적임.  
일반적으로 I/O 집약적인 NoSQL 및 관계형 데이터베이스에 사용됨.
* **볼륨 크기**  
4 GB에서 16 TB까지.
* **내구성**  
99.8% - 99.9%의 내구성을 제공함(연간 실패율 0.1% - 0.2%).

### io1 vs. io2

* **io1**  
io1 볼륨은 기존의 Provisioned IOPS SSD 볼륨으로, 높은 IOPS를 제공하지만, io2 볼륨에 비해 IOPS 대비 저장소 비율이 낮음.  
io1 볼륨은 GB당 최대 50 IOPS를 제공할 수 있음.

* **io2**  
io2 Block Express 볼륨은 다음 세대의 Amazon EBS 스토리지 서버 아키텍처에 기반을 두고 있으며, **Nitro System** 기반 인스턴스에서 실행되는 가장 요구 사항이 까다로운 I/O 집약적 애플리케이션의 성능 요구 사항을 충족시키기 위해 구축되었음.  
이 볼륨은 99.999%의 내구성과 연간 장애율이 0.001% 이하임을 보장하며, 이는 1년 동안 운영되는 볼륨 10만 개당 단 1건의 볼륨 장애가 발생함을 의미.

* **정리**  
따라서, io2 볼륨은 io1 볼륨에 비해 더 높은 성능과 내구성을 제공하며, 특히 io2 Block Express는 더 높은 IOPS와 처리량, 그리고 더 큰 저장 용량을 지원함으로써, 더욱 요구 사항이 까다로운 애플리케이션에 적합.
