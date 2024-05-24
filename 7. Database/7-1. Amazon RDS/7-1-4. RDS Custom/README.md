# [AWS RDS Custom](https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/UserGuide/rds-custom.html)

## AWS RDS Custom

### 설명

* 표준 Amazon RDS와 달리 사용자에게 운영 체제 수준에서의 제어를 제공함.  
* 특정 데이터베이스 엔진 버전이나 고유한 데이터베이스 설정이 필요한 환경에 적합.

### 사용 이유

* RDS Custom은 특정 요구 사항을 충족하기 위해 **Amazon RDS의 관리 기능**과 **EC2의 유연성을 결합**함.  
* 이를 통해 운영 체제 및 데이터베이스 설정을 세부적으로 제어할 수 있음.  
* 일반적으로 SAP, Oracle E-Business Suite 같은 엔터프라이즈 애플리케이션을 호스팅할 때 유용함.

### RDS Custom 시작

1. **VPC 및 서브넷 설정**  
    * RDS Custom 인스턴스를 배포할 VPC 및 서브넷 그룹을 설정함.  
    * VPC는 RDS Custom 인스턴스가 네트워크에 안전하게 연결될 수 있도록 함.

    ```json
    {
    "VpcId": "vpc-0abcd1234efgh5678",
    "DBSubnetGroupName": "my-subnet-group"
    }
    ```

2. **RDS Custom DB 인스턴스 생성**
    * AWS Management Console, AWS CLI, 또는 AWS SDK를 사용하여 RDS Custom DB 인스턴스를 생성.
    * Oracle Database 예시
    ```bash
    aws rds create-db-instance --db-instance-identifier my-custom-db \
    --db-instance-class db.m5.large \
    --engine custom-oracle-ee \
    --allocated-storage 20 \
    --db-subnet-group my-subnet-group \
    --master-username admin \
    --master-user-password mypassword
    ```

3. **IAM 역할 설정**
    * RDS Custom 인스턴스에 연결할 때 사용할 IAM 역할을 설정함.  
    * 이 역할은 RDS Custom 인스턴스가 Amazon S3와 같은 다른 AWS 서비스에 접근할 수 있도록 함.
    ```json
    {
        "RoleName": "RDSCustomRole",
        "AssumeRolePolicyDocument": {
        "Version": "2012-10-17",
        "Statement": [
                {
                    "Effect": "Allow",
                    "Principal": {
                        "Service": "rds.amazonaws.com"
                    },
                    "Action": "sts:AssumeRole"
                }
            ]
        }
    }
    ```

4. **운영 체제 접근 및 사용자 정의 설정**
    * RDS Custom 인스턴스는 EC2 **인스턴스처럼 운영 체제에 접근할 수 있음**.  
    * SSM(Session Manager)을 사용하여 인스턴스에 접근하고 운영 체제 수준에서 사용자 정의 설정을 적용할 수 있음.

### RDS Custom 관리
1. **패치 관리**  
    * RDS Custom 인스턴스에 대한 패치 관리도 필요함.  
    * 사용자 정의 환경에서는 운영 체제 및 데이터베이스 엔진에 대해 패치를 직접 관리해야 함.

2. **백업 및 복구**
    * RDS Custom 인스턴스는 자동 및 수동 백업을 지원함.  
    * AWS Management Console, CLI, 또는 SDK를 통해 스냅샷을 생성하고 복구할 수 있음.

3. **모니터링 및 로깅**
    * CloudWatch를 사용하여 RDS Custom 인스턴스의 성능을 모니터링할 수 있음.  
    * 로그는 CloudWatch Logs에 저장될 수 있으며, 이를 통해 인스턴스의 상태를 확인할 수 있음.

### RDS Custom 장점

* **제어성**  
운영 체제 및 데이터베이스 엔진 설정에 대한 높은 수준의 제어를 제공.
* **유연성**  
특정 애플리케이션 요구 사항에 맞게 환경을 조정할 수 있음.
* **관리 용이성**  
RDS의 자동화된 관리 기능과 EC2의 유연성을 결합하여 관리 부담을 줄임.

### RDS Custom 지원 데이터베이스 엔진

1. **Oracle Database**  
    * **Amazon RDS Custom for Oracle**은 Oracle Database 엔진을 지원.  
    * 사용자는 운영 체제에 대한 액세스 및 관리 권한을 가지면서도 RDS의 관리 기능을 활용할 수 있음.  
    * 지원되는 버전: Oracle Database 12.1, 12.2, 18c, 19c

2. **Microsoft SQL Server**  
    * **Amazon RDS Custom for SQL Server**는 Microsoft SQL Server 엔진을 지원.  
    * SQL Server 환경에서 고유한 커스터마이징 요구 사항을 충족하기 위한 것.
    * 지원되는 버전: SQL Server 2016, 2017, 2019

### RDS Custom을 사용하기 위한 EC2 접근 방법

1. **AWS Systems Manager(SSM) Session Manager**

* AWS Systems Manager Session Manager는 EC2 인스턴스에 안전하고 관리하기 쉬운 방식으로 접근할 수 있도록 해줌.  
* Session Manager를 사용하면 SSH 키를 관리할 필요 없이 브라우저나 AWS CLI를 통해 세션을 시작할 수 있음.

2. **SSH(Secure Shell)** 접근

* 일부 사용자는 SSH를 통해 직접 EC2 인스턴스에 접근할 수도 있음.  
* 하지만, RDS Custom 인스턴스의 경우, AWS에서는 SSM을 사용하는 것을 권장하고 있음

Amazon RDS Custom 인스턴스에 접근하기 위해 **AWS Systems Manager Session Manager**를 사용하는 것이 권장됨.  
이는 SSH 키 관리의 부담을 덜고, 더욱 안전하고 관리하기 쉬운 방식으로 접근할 수 있게 해줌.  
필요 시, SSH를 사용할 수도 있지만, SSM을 통한 접근이 더 효율적이고 보안적인 방법임.

### Deactivate Automation Mode

#### 설명

* RDS Custom을 적용하기 위해서 반드시 Automation Mode를 비활성화(Deactivate)할 필요는 없음.  
* 그러나 RDS Custom 인스턴스를 사용하면서 **특정 사용자 정의 작업을 수행하거나 인스턴스에 대한 직접적인 제어가 필요할 경우**, Automation Mode를 비활성화하는 것이 필요할 수 있음.

#### Automation Mode 비활성화가 필요한 경우

* 사용자가 직접적인 인스턴스 접근 및 사용자 정의 작업을 수행하려면, 일시적으로 Automation Mode를 비활성화해야 할 수 있음.  
* 예를 들어, 커스텀 패키지를 설치하거나 특정 설정을 변경하는 등의 작업을 수행할 때 이 모드를 비활성화해야 함.

#### RDS Custom 인스턴스 작업 흐름

1. **Automation Mode 비활성화**

    * **사용자 정의 작업을 수행하기 전**에 Automation Mode를 비활성화.

2. **사용자 정의 작업 수행**

    * 필요한 변경 작업이나 설치 작업을 수행.

3. **Automation Mode 재활성화**

    * 작업이 완료되면 Automation Mode를 다시 활성화하여 관리 작업이 자동으로 수행되도록 설정함.

RDS Custom 인스턴스에서 **특정 작업을 수행하려면 Automation Mode를 비활성화**해야 할 수 있지만, 이는 특정 작업을 위한 것이지 항상 비활성화할 필요는 없음.  
일반적으로, Automation Mode를 활성화 상태로 유지하는 것이 관리와 유지보수 측면에서 더 유리함.