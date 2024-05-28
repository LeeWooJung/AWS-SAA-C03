# [Aurora Replica Auto Scaling](https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/AuroraUserGuide/Aurora.Integrating.AutoScaling.html)

## Aurora Replica Auto Scaling

### 설명

* **Aurora Replicas**  
Amazon Aurora 클러스터 내에서 읽기 전용 작업을 처리하는 복제본.  
Replicas는 Primary Instance의 데이터를 실시간으로 복제하여 읽기 성능을 향상시키고 고가용성을 제공함.

* **Auto Scaling**  
클러스터의 읽기 요청 부하가 증가하거나 감소할 때 자동으로 Aurora Replicas의 수를 조정하는 기능.  
이를 통해 필요한 시점에 읽기 용량을 자동으로 확장하거나 축소할 수 있음.

* **Reader Endpoint**  
Aurora 클러스터 내의 모든 읽기 전용 인스턴스(Aurora Replicas)를 단일 엔드포인트로 묶어 제공함.  
애플리케이션이 Reader Endpoint에 연결하면, Aurora는 읽기 요청을 가능한 Aurora Replicas로 분산시켜 부하를 관리함.

## Auto Scaling과 Reader Endpoint 확장

### 동작

1. **모니터링**  
    * Aurora는 지속적으로 클러스터의 읽기 요청 부하를 모니터링함.  
    * 사용자가 설정한 조건에 따라 Auto Scaling 정책이 트리거됨.  
    * 예를 들어, CPU 사용률, 네트워크 트래픽, 읽기 IOPS 등의 지표가 설정된 임계값을 초과하면 Auto Scaling이 시작됨.

2. **Replica 추가**  
    * Aurora는 클러스터에 추가적인 Aurora Replicas를 생성.  
    * 새로운 Replicas는 Primary Instance로부터 데이터를 복제하여 읽기 요청을 처리할 준비를 함.

3. **Reader Endpoint 확장**  
    * 새로운 Aurora Replicas가 생성되면, Reader Endpoint가 자동으로 확장됨.  
    * 이는 Reader Endpoint에 연결된 애플리케이션이 추가된 Replicas를 통해 읽기 요청을 처리할 수 있게 함.  
    * Aurora는 이 과정에서 부하를 새로운 Replicas로 자동으로 분산시켜 클러스터의 전체 읽기 성능을 향상시킴.

4. **로드 밸런싱**  
    * Reader Endpoint는 이제 추가된 Replicas를 포함하여 모든 읽기 전용 인스턴스 간에 읽기 요청을 분산시킴.  
    * 이는 클러스터의 모든 Replicas가 고르게 부하를 처리하게 함으로써 응답 시간을 최소화하고 성능을 최적화함.

## Architecture

![Auto Scaling Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/f94f66ca-3112-4a17-90ad-9971f9bfcc00)

