# [Aurora Custom Endpoint](https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.Endpoints.html#Aurora.Endpoints.Custom)

## Aurora Custom Endpoint

### 설명

* Amazon Aurora의 **Custom Endpoint**는 클러스터 내에서 특정 인스턴스 그룹에 대한 연결을 관리하는 데 사용됨.  
* 이를 통해 애플리케이션이 특정 역할을 수행하는 인스턴스에 연결할 수 있도록 세부 조정이 가능함.  
* **Custom Endpoint**는 다양한 사용 사례에 유연성을 제공하여 특정 인스턴스에 대해 읽기 또는 쓰기 작업을 분리하거나, 특정 애플리케이션 요구사항에 맞게 트래픽을 분산할 수 있음.

### 특징

1. **지정된 인스턴스 그룹**  
    * **Custom Endpoint**는 Aurora 클러스터 내의 특정 인스턴스 그룹에 대한 연결을 정의함.
    * 클러스터의 인스턴스 중 일부를 선택하여 Custom Endpoint에 할당할 수 있음.

2. **다양한 사용 사례**  
    * 특정 읽기 또는 쓰기 워크로드를 처리하기 위해 **Custom Endpoint**를 사용할 수 있음.
    * 트래픽 분산, 테스트 환경 분리, 리소스 격리 등의 용도로 활용할 수 있음.

3. **유연한 트래픽 관리**  
    * Custom Endpoint는 트래픽을 특정 인스턴스 그룹으로 라우팅하여 부하를 관리하고 성능을 최적화할 수 있음.
    * 동적 확장 또는 축소와 같은 상황에서도 Custom Endpoint 구성을 통해 트래픽 분산을 효율적으로 조정할 수 있음.

### 생성

1. **Custom Endpoint 생성**  
    * AWS Management Console, AWS CLI, RDS API 등을 통해 Custom Endpoint를 생성할 수 있음.
    * Custom Endpoint를 생성할 때 연결할 **인스턴스 그룹을 지정**해야 함.

2. **인스턴스 그룹 지정**  
    * Aurora 클러스터 내에서 Custom Endpoint에 연결할 인스턴스를 선택함.
    * 예를 들어, 고성능 읽기 작업을 처리하기 위해 높은 스펙의 인스턴스만 선택할 수 있음.

3. **트래픽 라우팅**  
    * Custom Endpoint에 연결된 애플리케이션 트래픽은 지정된 인스턴스 그룹으로 라우팅됨.
    * 이를 통해 읽기 또는 쓰기 작업을 특정 인스턴스에 집중시키거나 분산시킬 수 있음.

### Use Case

1. **고성능 읽기 작업**  
    * 고성능 읽기 작업을 위해 고성능 Aurora Replicas를 Custom Endpoint에 할당.
    * 예를 들어, **분석 쿼리**를 처리하는 인스턴스 그룹을 지정하여 읽기 성능을 최적화할 수 있음.

2. **테스트 및 개발 환경**  
    * Custom Endpoint를 사용하여 테스트 또는 개발 환경을 **분리**할 수 있음.
    * 특정 인스턴스를 테스트 작업에 할당하고 Custom Endpoint를 통해 연결하여 **운영 환경에 영향을 주지 않도록** 할 수 있음.

3. **특정 애플리케이션 요구사항**  
    * 특정 애플리케이션이 요구하는 트래픽 패턴에 맞춰 Custom Endpoint를 구성할 수 있음.
    * 예를 들어, **특정 유형의 쿼리를 처리하는 인스턴스 그룹**을 Custom Endpoint에 할당하여 성능을 최적화할 수 있음.

### 작동 방식

* **Dynamic Membership**  
인스턴스의 추가 또는 제거가 필요할 때 Custom Endpoint의 구성도 동적으로 조정될 수 있음.  
이를 통해 **트래픽을 유연하게 관리**할 수 있음.

* **Health Monitoring**  
Aurora는 Custom Endpoint에 연결된 인스턴스의 상태를 지속적으로 모니터링함.  문제가 발생한 인스턴스는 자동으로 Custom Endpoint에서 제외되어, 트래픽이 안정적으로 분산됨.

* **High Availability**  
Custom Endpoint는 클러스터의 고가용성을 유지하면서 **특정 인스턴스 그룹으로 트래픽을 라우팅하는 기능을 제공**하므로, 고가용성과 성능을 동시에 충족할 수 있음.