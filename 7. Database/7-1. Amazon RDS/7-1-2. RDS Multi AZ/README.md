# [AWS RDS Multi AZ](https://aws.amazon.com/ko/rds/features/multi-az/)

## AWS RDS Multi AZ

### 설명

Amazon RDS(**Multi-AZ**)는 RDS(Relational Database Service)의 고가용성 옵션 중 하나로, 주 데이터베이스 인스턴스의 복제본을 다른 가용 영역에 자동으로 생성하여 가용성을 향상시킴.

### 특징

1. **자동 복제**  
주 데이터베이스 인스턴스의 모든 데이터는 다른 가용 영역에 있는 **복제본으로 자동 복제**됨.

2. **자동 장애 조치**  
주 데이터베이스 인스턴스에 장애가 발생하면 Amazon RDS는 **자동으로 읽기 및 쓰기 작업을 복제본으로 전환**하여 서비스 중단 시간을 최소화함.

3. **데이터 싱크 유지**  
데이터베이스의 복제본은 주 데이터베이스 인스턴스와 동기적(**SYNC**)으로 유지되므로 **데이터의 일관성이 유지**됨.

4. **고가용성 보장**  
Multi-AZ 구성은 가용 영역의 장애로부터 데이터베이스를 보호하여 시스템의 가용성을 향상시킴.

5. **Scaling에 사용되지 않음**

### 작동 방식

1. **주 데이터베이스 인스턴스**  
애플리케이션의 주 데이터베이스 인스턴스는 **읽기 및 쓰기 작업**을 처리함.

2. **다중 가용 영역 복제본**  
Multi-AZ 구성에서는 주 데이터베이스 인스턴스의 복제본이 **다른 가용 영역에 자동으로 생성**됨.  
이 복제본은 주 데이터베이스와 동기적(**SYNC**)으로 유지되며, 필요 시 주 데이터베이스 인스턴스의 역할을 대신 수행함.

3. **장애 조치**(Failover)  
주 데이터베이스 인스턴스에 장애가 발생하면 Amazon RDS는 자동으로 복제본으로 전환하여 서비스를 계속 제공함.  
이 과정에서 애플리케이션은 새로운 주 데이터베이스 인스턴스로 자동으로 연결됨. **이 때, 애플리케이션이 서버에 접속하려 하는 DNS 이름은 바뀌지 않음**.

### Use Case

1. **고가용성 요구 사항**  
서비스의 가용성을 높이고 장애 시간을 최소화해야 하는 경우 Multi-AZ 구성을 사용해야 함.

2. **지역적 재해 복구**  
서로 다른 가용 영역에 데이터베이스의 복제본을 유지함으로써 지역적 재해 발생 시 데이터의 안전성을 보장할 수 있음.

3. **비즈니스 연속성**  
데이터베이스의 장애에 대비하여 응용 프로그램의 연속성을 보장하는 데 사용됨.

## From Single AZ to Multi AZ

### 설명

* Amazon RDS를 Single-AZ에서 Multi-AZ로 변환하면 고가용성 및 내구성을 높일 수 있음.  
* Multi-AZ 배포에서는 기본 데이터베이스 인스턴스와 동기화된 **스탠바이 복제본**이 다른 가용 영역에 유지됨.  
* 장애 발생 시 스탠바이 인스턴스로 자동으로 전환되므로 데이터베이스의 가용성이 보장됨.

### 장점

* **고가용성**  
데이터베이스 인스턴스가 장애가 발생하면 스탠바이 인스턴스로 자동 전환하여 서비스 중단을 최소화함.
* **데이터 내구성**  
동기화된 스탠바이 인스턴스를 유지하여 데이터 손실을 방지함.
* **자동 백업**  
스탠바이 인스턴스를 사용하여 백업을 수행하므로, 백업 중에 성능에 미치는 영향을 최소화 함.
* **간편한 유지보수**  
유지보수 작업 중에도 스탠바이 인스턴스를 사용하여 가용성을 유지할 수 있음.

### 변환 방법

1. **AWS Management Console**  
    
    AWS Management Console에 로그인.  
    &rarr; RDS 서비스로 이동.  
    &rarr; 변경하려는 데이터베이스 인스턴스를 선택.  
    &rarr; 인스턴스의 "Instance Actions" 메뉴에서 "**Modify**"를 선택.  
    &rarr; "Availability & durability" 섹션에서 "**Multi-AZ deployment**"를 "Yes"로 변경.  
    &rarr; "Continue"를 클릭하고 설정을 검토한 후 "Apply immediately" 또는 "Apply during the next maintenance window"를 선택.  
    &rarr; "Modify DB Instance"를 클릭하여 변경 사항을 저장.

2. **AWS CLI**  

    ```bash
    aws rds modify-db-instance \
    --db-instance-identifier your-db-instance-identifier \
    --multi-az \
    --apply-immediately
    ```

3. **CloudFormation**  
CloudFormation 템플릿에서 'MultiAZ' 속성을 'true'로 설정하고 스택을 업데이트.

    ```yaml
    Resources:
        MyDBInstance:
            Type: AWS::RDS::DBInstance
            Properties:
                DBInstanceClass: db.m5.large
                Engine: mysql
                MultiAZ: true
                # Other properties...
    ```

### Use Snapshot

#### 설명
Amazon RDS 스냅샷은 특정 시점에서 데이터베이스의 상태를 캡처하여 백업하는 기능.  
Multi-AZ 배포를 사용할 때, 스냅샷의 생성 및 복구에도 차이가 발생.

#### 장점
* **향상된 데이터 보호**  
Multi-AZ 배포에서는 기본 인스턴스와 스탠바이 인스턴스 **모두 동기화**되므로 스냅샷을 생성할 때 데이터 손실 위험이 줄어듦.
* **백업 성능 향상**  
스탠바이 인스턴스를 사용하여 스냅샷을 생성하므로, 기본 인스턴스의 성능에 미치는 영향을 최소화함.
* **복구 시간 단축**  
Multi-AZ 배포에서 스냅샷을 복구할 때 스탠바이 인스턴스도 자동으로 생성되므로, 고가용성 환경을 신속하게 복구할 수 있음.

#### 변환 방법

* 스냅샷이 생성되면, AWS Management Console에서 "Snapshots" 섹션으로 이동.
* 생성된 스냅샷을 선택하고 "Actions"에서 "Restore snapshot"을 선택.
* 복구 설정에서 "Multi-AZ deployment"를 "Yes"로 선택.
* 나머지 설정을 완료하고 "Restore DB Instance"를 클릭.

## RDS Multi AZ Architecture

![RDS Multi AZ architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/8673fe89-e05b-490c-9571-15755b54c17f)

## From Single AZ to Multi AZ using Snapshot

![Single AZ to Multi AZ architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/7a5fdee7-cf99-4f47-bb51-a374cb510bea)
