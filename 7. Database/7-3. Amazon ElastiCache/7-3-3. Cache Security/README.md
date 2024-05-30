# Cache Security

## Cache Security

* **Amazon ElastiCache**는 클라우드 기반의 관리형 메모리 캐시 서비스로, Redis와 Memcached 엔진을 지원.  
* ElastiCache는 보안 관점에서 다양한 기능을 제공하여 데이터를 안전하게 보호함.

### 네트워크 보안

* **Virtual Private Cloud (VPC)**  
    * ElastiCache 클러스터는 Amazon Virtual Private Cloud (VPC) 내에서 생성할 수 있음.  
    * 이를 통해 클러스터를 격리된 네트워크 내에 배치하고, 서브넷과 라우팅 테이블, 네트워크 게이트웨이 등을 설정하여 접근을 제어할 수 있음.
* **보안 그룹**  
    * VPC 보안 그룹을 사용하여 클러스터에 대한 인바운드 및 아웃바운드 트래픽을 제어.  
    * 특정 IP 주소 범위나 VPC 내의 다른 인스턴스에서의 접근을 허용할 수 있음.

### 접근 제어

* **AWS Identity and Access Management** (IAM)  
    * **IAM 역할**  
    ElastiCache 클러스터에 연결된 애플리케이션이 특정 IAM 역할을 통해서만 클러스터에 접근할 수 있도록 제한할 수 있음.
    * **정책**  
    IAM 정책을 사용하여 ElastiCache 자원에 대한 접근 권한을 세밀하게 제어할 수 있음. 예를 들어, 특정 사용자가 클러스터를 생성하거나 삭제할 수 있는 권한을 제한할 수 있음(AWS API-level Security).

### 데이터 암호화

* **전송 중 암호화** (Encryption in Transit)  
    * **TLS**  
    ElastiCache for **Redis**는 클라이언트와 클러스터 간의 트래픽을 TLS(Transport Layer Security) 프로토콜을 사용하여 암호화함.  
    이를 통해 전송 중에 데이터가 도청되거나 조작되는 것을 방지.
* **저장 시 암호화** (Encryption at Rest)  
    * **KMS**  
    ElastiCache for **Redis**는 AWS Key Management Service (KMS)를 사용하여 저장된 데이터를 암호화할 수 있음.  
    이를 통해 디스크에 저장된 데이터가 보호됨.

### 모니터링 및 감사

* **Amazon CloudWatch**
    * **모니터링**  
    CloudWatch를 통해 ElastiCache 클러스터의 성능 및 운영 상태를 모니터링할 수 있음.  
    주요 메트릭에는 **CPU 사용률, 메모리 사용량, 네트워크 트래픽 등**이 포함됨.
    * **경고 설정**  
    특정 조건을 기준으로 경고를 설정하여 성능 문제나 보안 위협에 대해 신속하게 대응할 수 있음.

* **AWS CloudTrail**
    * **로그 감사**  
    CloudTrail을 통해 ElastiCache와 관련된 모든 API 호출을 로깅할 수 있음.  
    이를 통해 누가 언제 어떤 작업을 수행했는지에 대한 감사 로그를 확인할 수 있음.
    * **변경 기록**  
    CloudTrail 로그는 구성 변경, 보안 설정 변경 등 중요한 변경 사항을 추적하는 데 유용함.

## Summary

**Amazon ElastiCache**는 **VPC 및 보안 그룹을 통한 네트워크 보안, IAM을 통한 접근 제어, TLS 및 KMS를 통한 데이터 암호화, CloudWatch 및 CloudTrail을 통한 모니터링 및 감사 등 다양한 보안 기능**을 제공.  
이를 통해 ElastiCache 클러스터와 데이터를 안전하게 보호할 수 있음.

이와 같은 보안 기능들은 ElastiCache를 사용하여 민감한 데이터를 캐싱하거나 성능을 최적화하는 애플리케이션에서 중요한 역할을 함.