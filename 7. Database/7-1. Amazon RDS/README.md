# [AWS RDS](https://aws.amazon.com/ko/rds/?gclid=Cj0KCQjw0ruyBhDuARIsANSZ3wpsWljDcC1kapJJvUSyCfYIwguY_n_KyJxm2EbmsAdK9la7dkt_-YQaAsdhEALw_wcB&trk=fa578b5f-d60e-499f-a297-d9fdfdced64e&sc_channel=ps&ef_id=Cj0KCQjw0ruyBhDuARIsANSZ3wpsWljDcC1kapJJvUSyCfYIwguY_n_KyJxm2EbmsAdK9la7dkt_-YQaAsdhEALw_wcB:G:s&s_kwcid=AL!4422!3!548652089646!p!!g!!aws%20rds!11550597574!121019969748)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/eb86c7cf-8b3f-40b3-b8e1-6c9687cf16bd" width = "25" height = "25"> AWS RDS(Relational Database Service)

### 설명

* AWS에서 제공하는 **완전 관리형 관계형 데이터베이스 서비스**.  
* 데이터베이스 관리의 복잡성을 줄이고, 사용자가 데이터베이스 관리 작업 대신 애플리케이션 개발에 집중할 수 있도록 도움.  
* Amazon RDS는 다양한 데이터베이스 엔진을 지원하며, 고가용성과 확장성을 갖춘 서비스임.

### 특징

1. **지원하는 데이터베이스 엔진**

    * **Amazon Aurora**  
    MySQL 및 PostgreSQL 호환 고성능 데이터베이스
    * **MySQL**  
    오픈 소스 관계형 데이터베이스
    * **MariaDB**  
    MySQL의 포크(Fork)로서의 오픈 소스 데이터베이스
    * **PostgreSQL**  
    고급 기능을 가진 오픈 소스 데이터베이스
    * **Oracle**  
    상용 관계형 데이터베이스
    * **Microsoft SQL Server**  
    상용 관계형 데이터베이스
    * **IBM DB2**

2. **자동화된 관리**

    * **프로비저닝**(Automated Provisioning)  
    데이터베이스 인스턴스를 쉽게 생성 및 설정
    * **패치 관리**(OS Patching)  
    데이터베이스 소프트웨어의 자동 업데이트 및 패치
    * **백업 및 복구**  
    자동 백업 설정 및 특정 시점 복구(Point-in-time Recovery) 지원
    * **모니터링 및 메트릭**  
    Amazon CloudWatch를 통해 성능 메트릭 모니터링

3. **고가용성 및 내구성**

    * **Multi-AZ 배포**  
    여러 가용 영역에 데이터베이스 복제본을 생성하여 장애 발생 시 자동 Failover

    * **자동 백업**  
    자동화된 백업과 스냅샷 기능을 제공하여 데이터 보호

    * **스토리지 옵션**  
    [General Purpose SSD](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-1.%20EBS/6-1-1.%20General%20Purpose%20SSD), [Provisioned IOPS SSD](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-1.%20EBS/6-1-2.%20Provisioned%20IOPS%20SSD), [Hard Disk Drives](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-1.%20EBS/6-1-3.%20Hard%20Disk%20Drives) 지원

4. **확장성**

    * **읽기 복제본(Read Replicas)**  
    읽기 작업의 부하를 분산시키기 위해 읽기 복제본 생성 가능

    * **성능 조정**  
    필요에 따라 쉽게 스토리지 및 컴퓨팅 리소스 확장 가능(Scaling capability, Vertical & horizontal)

5. **보안**

    * **VPC 통합**  
    Amazon VPC와 통합하여 네트워크 접근 제어

    * **IAM 연동**  
    AWS IAM을 통해 세밀한 권한 관리

    * **데이터 암호화**  
    데이터 저장 및 전송 시 암호화 지원

    **위와 같은 장점 덕분에 EC2 인스턴스에서 실행하는 DataBase보다 효율적임**

    하지만, SSH 사용 불가능.

### Use Case

* **전자상거래 애플리케이션**  
주문, 고객 정보, 제품 정보 등을 관계형 데이터베이스에 저장하고 처리
* **SaaS 애플리케이션**  
사용자 데이터, 인증 정보 등을 저장하여 여러 고객이 동일한 데이터베이스 인프라를 공유
* **모바일 애플리케이션**  
사용자 프로필, 활동 로그, 애플리케이션 상태 데이터를 저장 및 관리

## RDS Simple Architecture

![RDS architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/80114e7f-a88c-48c3-a68a-ff3b2f14be9a)

## Summary

* PostSQL, MySQL, Oracle, SQL Server, DB2, MariaDB, Custom

* 프로비저닝 된 RDS 인스턴스 크기 & EBS Volume Type & Size

* 스토리지 Auto Scaling 가능.

* Multi AZ, Read Replicas 지원됨.

* IAM, Security Groups, KMS, SSL in transit으로 보안.

* 자동 백업. Point in time 복원(~35일)

* Long-term recovery를 위한 Manual DB Snapshot 가능.

* IAM Authentication, Secret Manager와 통합 가능.