# [Identity and Access Management](https://aws.amazon.com/ko/iam/)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/56f4e197-4513-47f7-90fd-db70b9d46f9f" width = "20" height = "20"> IAM

* **IAM**: AWS IAM은 AWS 서비스 및 리소스에 대한 **액세스**를 관리하고 조정하는 데 사용.  
 이를 통해 민첩성과 혁신을 지원하면서 워크로드와 인력의 액세스를 안전하게 관리 가능.
* **사용자 및 그룹**: IAM을 사용하여 단일 AWS 계정에서 ID를 관리하거나 중앙에서 여러 AWS 계정에 ID를 연결가능.  
속성 기반 액세스 제어를 사용하여 사용자 속성(예: 부서, 직무, 팀 이름)을 기준으로 세분화된 권한을 만듦.
* **IAM 권한**: 권한 관리를 통해 최소 권한 정책을 생성하고, 리소스에 대한 외부 및 미사용 액세스를 확인하며, 지속적인 분석을 통해 적절한 권한을 부여할 수 있음.
* **IAM 정책**: IAM 정책은 JSON 형식으로 작성되며, AWS 리소스에 대한 세분화된 액세스 제어를 가능하게 함.  
정책은 서비스 제어 정책을 사용하여 IAM 사용자 및 역할에 대한 권한 가드레일을 설정하고, AWS Organizations의 계정에 대한 데이터 경계를 구현하는 데 사용.  
IAM 정책은 **최소 권한**만을 부여하여 보안을 강화하는 것이 중요.
* IAM은 Global Service(Not Regional Service)

## IAM 사용자 및 그룹

* **IAM 사용자**: 실제 사람이나 애플리케이션을 의미하며 AWS 서비스에 접근할 수 있는 권한을 가짐.  
각 사용자는 고유한 식별 정보와 자격 증명을 가지고 있으며, 이를 통해 AWS 서비스에 로그인하고 사용할 수 있음.
* **IAM 그룹**: 여러 IAM 사용자를 하나의 그룹으로 묶어서 관리할 수 있음.  
그룹에 정책을 연결함으로써 그룹에 속한 모든 사용자에게 동일한 권한을 부여할 수 있음.  
예를 들어, ‘개발자’ 그룹에는 EC2와 S3에 대한 접근 권한을, ‘DB 관리자’ 그룹에는 RDS에 대한 접근 권한을 줄 수 있음.

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/7a950dc0-0282-4efc-b7d5-b9aa7d08005e" width="30" height="20"> IAM Role

* **IAM Role**: AWS IAM 역할은 권한 세트를 정의하는 기능임.  
역할을 사용하면 신뢰할 수 있는 IAM 사용자나 애플리케이션, 또는 **AWS 서비스가 일시적으로 권한**을 가질 수 있게 됨.  
역할은 **IAM 사용자나 그룹에 연결되지 않고**, 대신 역할을 맡을 수 있는 신뢰할 수 있는 엔티티에게만 권한을 부여함.

* **예시**: IAM 사용자가 S3 버킷에 접근하려면, S3 Read 권한이 연결된 역할을 맡아야 함.  
역할을 맡으면 그 IAM 사용자는 임시 보안 자격 증명을 받아서 S3 버킷에 접근할 수 있게 됨.  
이 과정에서 역할은 권한을 갖고 있지만, 그 권한은 필요한 사용자나 서비스가 역할을 맡을 때만 활성화됨.

* **정책**: 역할을 만들 때는 누가 역할을 맡을 수 있는지 지정하는 신뢰 정책(Trust Policy)을 설정해야 함.  
신뢰 정책에는 역할을 맡을 수 있는 IAM 사용자나 AWS 리소스를 담당자(**Principal**)로 지정함.  
이렇게 역할을 통해 권한을 임시로 부여받는 방식으로 AWS 리소스에 접근하거나 작업을 수행할 수 있게 됨

## IAM 정책 구조

* **Version**: policy language version("2012-10-17"을 항상 포함해야 함)
* **ID**: Identifier of policy (Optional)
* **Statement**: 한 개 이상의 개별 statements (Required)

### Statement 구조

* **Sid**: Identifier of statement (Optional)
* **Effect**: Allow or Deny ; allow or deny access
* **Principal**: IAM 정책이 적용될 account, user, role 등에 대한 정의
* **Action**: IAM Effect가 적용될 Actions
* **Resource**: Action이 적용될 자원
* **Condition** (Optional): conditions for when this policy is in effect

## IAM 정책 예시
* **개발자그룹(Sid: DevGroupPolicy)**  
    * EC2 인스턴스에 대한 조회, 시작 및 중지 권한
    * S3 버킷의 목록 조회 및 객체 가져오기 권한
* **DB관리자그룹(Sid: DBAdminGroupPolicy)**
    * RDS 인스턴스에 대한 조회, 시작 및 중지, 수정 권한
* **리전**: ap-northeast-2

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:Describe*",
                "ec2:StartInstances",
                "ec2:StopInstances",
                "s3:ListBucket",
                "s3:GetObject"
            ],
            "Resource": "*",
            "Condition": {"StringEquals": {"aws:RequestedRegion": "ap-northeast-2"}},
            "Sid": "DevGroupPolicy"
        },
        {
            "Effect": "Allow",
            "Action": [
                "rds:Describe*",
                "rds:StartDBInstance",
                "rds:StopDBInstance",
                "rds:ModifyDBInstance"
            ],
            "Resource": "*",
            "Condition": {"StringEquals": {"aws:RequestedRegion": "ap-northeast-2"}},
            "Sid": "DBAdminGroupPolicy"
        }
    ]
}

```

## IAM 정책 예시2
* **Sid(Statement ID)** : S3AccessPolicy
* **Effect**: 'Allow', 'Deny' 등
* **Principal**: AWS 계정 또는 AWS Service
* **Action**: 허용 또는 거부하려는 작업
* **Resource**: 권한이 적용될 리소스

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "S3AccessPolicy",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::123456789012:root"
            },
            "Action": [
                "s3:GetObject",
                "s3:ListBucket"
            ],
            "Resource": [
                "arn:aws:s3:::example-bucket",
                "arn:aws:s3:::example-bucket/*"
            ]
        }
    ]
}

```

## IAM 정책 예시3

IAM for S3

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "BucketLevelPermissions",
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME"
        },
        {
            "Sid": "ObjectLevelPermissions",
            "Effect": "Allow",
            "Action": [
                "s3:GetObject",
                "s3:PutObject",
                "s3:DeleteObject"
            ],
            "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
        }
    ]
}
```

**BucketLevelPermissions**는 S3 버킷의 목록을 나열하는 작업을 허용함. 이 때, Resource는  
> arn:aws:s3:::YOUR_BUCKET_NAME  

으로 특정 버킷을 대상으로 함.

**ObjectLevelPermissions**는 S3 특정 버킷(YOUR_BUCKET_NAME)의 객체를 대상으로 **GetObject**(읽기), **PutObject**(쓰기), **DeleteObject**(삭제) 작업을 허용함. 이 때, Resource는 **Bucket Level**과 다르게  
> arn:aws:s3:::YOUR_BUCKET_NAME/*  

와 같이 마지막에 "/*"가 붙음

## Diagram

![diagram](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/b508135d-0d54-4ef9-bae8-18211c7517f4)