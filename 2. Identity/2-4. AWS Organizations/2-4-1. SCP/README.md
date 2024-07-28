# [SCP](https://docs.aws.amazon.com/ko_kr/organizations/latest/userguide/orgs_manage_policies_scps.html)

## SCP(Service Control Policies)

Users와 Roles를 제약하기 위해 OU혹은 계정에 적용되는 **IAM Policies**

SCP는 **Management Account**에 적용되지 않음

IAM과 마찬가지로 기본적으로 **어떤 접근도 허용하지 않음**. 따라서 **Explicit Allow**정책이 필요함.

## Hierarchy Example

![scp hierarchy](https://github.com/user-attachments/assets/b26aece8-156b-441d-a2fb-9e448cb624db)

### Management Account

SCP를 적용하더라도, 관리 계정이므로 **SCP가 적용되지 않음**.

따라서 모든 작업을 수행할 수 있음.

### Account A

RedShift에 접근하는 것 이외에 모든 작업 수행 가능.

Account A에 **AuthorizedRedshift**가 적용 되었지만, Account A가 속한 OU(**Prod OU**)에 **DenyRedshift**가 적용되었기 때문에 Redshift에 접근할 수 없음.

### Account B

Redshift와 Lambda에 접근하는 것 이외에 모든 작업 수행 가능.

**Prod OU**에 **DenyReshift**가 적용되었고, Account B가 속한 **HR OU**에 **DenyAWSLambda**가 적용되었기 때문.

### Account C

Redshift에 접근하는 것 이외에 모든 작업 수행 가능.

**Prod OU**에 **DenyRedshift**가 적용되었기 떄문.

## BlockList & AllowList Example

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowsAllActions",
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        },
        {
            "Sid": "DenyDynamoDB",
            "Effect": "Deny",
            "Action": "dynamodb:*",
            "Resource": "*"
        }
    ]
}
```

* **Version**

    정책 언어의 특정 버전을 가리킴.

* **Statements**

    정책 문서에는 두 개의 주요 정책 문이 포함되어 있음.

    * **Sid:"AllowAllActions"**

        * **Sid**(Statement ID): 정책 문을 식별하는 고유 ID, 여기서는 "AllowsAllActions"
        * **Effect**: "Allow"는 이 정책문을 허용하는 효과를 가짐.
        * **Action**: "*"는 모든 AWS 서비스와 작업을 의미.
        * **Resource**: "*"는 모든 리소스를 의미.

        위 정책 문은 모든 AWS 서비스와 작업에 대한 모든 리소스에 대한 접근을 허용함.

    * **Sid:"DenyDynamoDB"**

        * **Sid**(Statement ID): 정책 문을 식별하는 고유 ID, 여기서는 "DenyDynamoDB"
        * **Effect**: "Deny"는 거부 효과를 가짐.
        * **Action**: "dynamodb:*"는 DynamoDB의 모든 작업을 의미.
        * **Resource**: "*"는 모든 리소스를 의미.

        위 정책 문은 DynamoDB 서비스의 모든 작업에 대한 모든 리소스에 대한 접근을 거부함.

결국, 조직 내의 계정은 DynamoDB를 제외한 모든 AWS 서비스와 작업을 사용할 수 있지만, DynamoDB에 대해서는 어떤 작업도 수행할 수 없음.

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:*",
                "cloudwatch:*"
            ],
            "Resource": "*"
        }
    ]
}
```

* **Version**

    정책 언어의 특정 버전을 가리킴.

* **Statements**

    정책 문서에는 하나의 주요 정책 문이 포함되어 있음.

    * **Sid:"AllowAllActions"**

        * **Effect**: "Allow"는 이 정책문을 허용하는 효과를 가짐.
        * **Action**
            * **"ec2:*"**: EC2 서비스의 모든 작업을 의미.
            * **"cloudwatch:*"**: CloudWatch 서비스의 모든 작업을 의미.
        * **Resource**: "*"는 모든 리소스를 의미.

결국, 위 정책 문은 다음과 같은 접근 제어를 정의함.

EC2 서비스의 모든 작업에 대한 모든 리소스에 접근을 허용.

CloudWatch 서비스의 모든 작업에 대한 모든 리소스에 접근을 허용.