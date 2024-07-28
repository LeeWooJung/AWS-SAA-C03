# [AWS Organizations](https://docs.aws.amazon.com/ko_kr/organizations/latest/userguide/orgs_introduction.html)

## <img src = "https://github.com/user-attachments/assets/222ab736-82e3-4ed3-9d8e-74ee49ec516c" width = "20" height = "20"> AWS Organizations

AWS Organizations는 **다중 AWS 계정을 하나의 조직으로 묶어 중앙에서 관리하는 글로벌 서비스**임. 

이 서비스를 사용하면 **계정 생성, 관리, 정책 적용, 청구 관리 등의 작업을 효율적으로 수행**할 수 있어 여러 개의 AWS Accounts를 관리할 수 있음.

Main Account는 **Management Account**임.

다른 Account는 **Member Accounts**임. Member Accounts는 **단 하나**의 Organization에 속함.

## 특징

### 계정 관리

여러 계정을 조직 단위로 그룹화하고 계정 생성을 자동화할 수 있음.

### 정책 적용

**서비스 제어 정책**(SCP)을 사용하여 계정에 대한 접근 및 리소스 사용을 제어할 수 있음.

### 통합 청구

모든 계정의 청구서를 하나로 통합하여 관리할 수 있음.

EC2, S3 등의 할인과 같은 가격 인하를 모든 계정이 통합하여 받을 수 있음.

**Shared reserved Instances**와 **Savings Plan** Discounts도 계정에 걸쳐 받을 수 있음.

### 비용 관리

각 계정의 비용을 추적하고 관리할 수 있음.

### 조직 단위 관리

**조직을 여러 개의 조직 단위**(OU)로 나누어 각 조직 단위별로 정책을 적용할 수 있음.

## 구성 요소

* **루트**

    **조직의 최상위 계층**으로, 모든 계정과 조직 단위를 포함함.

* **계정**

    조직 내의 개별 AWS 계정으로, 사용자는 이 계정들에서 리소스를 생성하고 관리함.

* **조직 단위**(OU)

    **계정을 그룹화하는 단위**로, OU별로 정책을 일괄 적용할 수 있음.

* **서비스 제어 정책**(SCP)

    **조직 내 계정 및 OU에 대해 허용 또는 금지할 수 있는 정책**을 정의함.

## Organizational Units(OU) 

AWS Organizations는 다음과 같은 계층 구조로 나뉨.

* **Root Organizational Unit(OU)**

    * Management Account

        * **OU 1**
            * Member Accounts
        * **OU 2**
            * **OU 2-1**
                * Member Accounts
            * **OU 2-2**
                * Member Accounts
        * **Other OUs**

### Business Unit Example

Business Unit은 다음과 같은 계층적 구조로 나눠질 수 있음.

* **Management Account**

    * **Sales OU**

        * **Sales Account 1**
        * **Sales Account 2**

    * **Retail OU**

        * **Retail Account 1**
        * **Retail Account 2**

    * **Finance OU**

        * **Finance Account 1**
        * **Finance Account 2**

### Environmental Life cycle Example

Environmental Life cycle은 다음과 같은 계층적 구조로 나눠질 수 있음.

* **Management Account**

    * **Prod OU**

        * **Prod Account 1**
        * **Prod Account 2**

    * **Dev OU**

        * **Dev Account 1**
        * **Dev Account 2**

    * **Test OU**

        * **Test Account 1**
        * **Test Account 2**

## 장점

* **중앙 관리**

    여러 계정을 한 곳에서 관리할 수 있어 관리 효율성이 높아짐.

* **정책 일관성**

    서비스 제어 정책(SCP)을 통해 일관된 보안 및 규정 준수를 보장할 수 있음.

* **비용 관리**

    통합 청구를 통해 비용을 효과적으로 추적하고 관리할 수 있음.

* **계정 격리**

    각 계정을 독립적으로 운영하여 보안 및 운영상의 이점을 얻을 수 있음.

* **Log 전송**

    모든 Account에 CloudTrail을 적용할 수 있으며, Logs를 S3 Account로 전송할 수 있음.

    CloudWatch Logs를 중앙 로깅 Account로 전송할 수 있음.

## 단점

* **복잡성 증가**

    많은 계정을 관리하려면 초기 설정과 지속적인 관리가 복잡해질 수 있음.

* **정책 관리**

    SCP를 잘못 설정하면 계정의 서비스 사용을 제한할 수 있어 주의가 필요함.

## Use case

* **대규모 기업**

    여러 부서나 사업부가 각기 다른 AWS 계정을 사용하는 대기업에서 중앙 관리 및 비용 절감을 위해 사용됨.

* **규정 준수**

    금융, 의료 등 규정 준수가 중요한 산업에서 일관된 보안 정책 적용을 위해 사용됨.

* **개발 및 테스트 환경 분리**

    개발, 테스트, 프로덕션 환경을 분리하여 계정 단위로 관리할 때 유용함.

## aws:PrincipalOrgID

aws:PrincipalOrgID는 **AWS 정책 조건 키로, 특정 AWS 조직(AWS Organizations)의 주체(Principal)에게만 액세스를 허용하거나 제한**하는 데 사용됨. 

이 조건 키는 주체가 특정 조직에 속하는 경우에만 정책을 평가하도록 하는 데 유용.

### Example

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:*",
            "Resource": "arn:aws:s3:::example-bucket/*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalOrgID": "o-exampleorgid"
                }
            }
        }
    ]
}
```

위 정책 문은 **모든 S3 작업을 허용**하고, example-bucket내의 **모든 객체**를 대상으로 함.

Conditions에서  
> "aws:PrincipalOrgID": "o-exampleorgid"  

는 주체가 지정된 조직 ID(o-exampleorgid)에 속하는 경우에만 액세스를 허용함.

## Summary

AWS Organizations는 여러 AWS 계정을 중앙에서 관리하고 제어할 수 있는 서비스로, 계정 생성 및 관리, 정책 적용, 통합 청구 등의 기능을 제공함. 

이를 통해 기업은 관리 효율성을 높이고, 일관된 보안 및 규정 준수를 보장할 수 있음.