# IAM Roles vs. Resource-based Policies

## IAM Role

IAM Role은 **특정 AWS 리소스에 접근할 수 있는 권한을 제공하는 엔터티**임. 

사용자, 애플리케이션, 서비스 등 다른 엔터티가 역할을 **가정**하여 권한을 획득할 수 있음.

### 특징

* **정책 첨부**

    역할에 IAM 정책을 첨부하여 역할이 수행할 수 있는 작업을 정의함.

* **역할 가정**(Assume Role)

    사용자는 역할을 가정하여 권한을 **임시로 얻을 수 있음**. 
    
    이는 사용자나 서비스가 자신의 기본 권한 외에 **추가 권한이 필요할 때 유용**함.

* **STS 토큰**

    역할을 가정할 때 **AWS Security Token Service**(STS) 토큰을 발급받아 **일시적으로 사용**할 수 있음.

### Use case

* 애플리케이션이 다른 AWS 서비스에 액세스해야 할 때.

* 다른 AWS 계정 간에 권한을 부여할 때.

* 특정 작업을 수행하는 임시 권한이 필요할 때.

### Example

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::example-bucket"
        }
    ]
}
```

## Resource-based Policies

리소스 기반 정책은 **특정 AWS 리소스에 대해 허용 또는 거부되는 작업을 정의**함. 

**정책이 리소스에 직접 첨부**됨.

### 특징

* **정책 첨부**

    정책이 리소스에 직접 첨부됨.

* **외부 계정 액세스**

    리소스 기반 정책을 사용하여 **다른 AWS 계정의 사용자나 역할이 리소스에 접근할 수 있도록 설정**할 수 있음.

* **리소스 범위**

    특정 리소스에 대해서만 적용됨.

### Use case

* S3 버킷에 대한 접근 제어.
* SQS 큐에 대한 접근 제어.
* SNS 주제에 대한 접근 제어.

### Example

``` json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::123456789012:user/ExampleUser"
            },
            "Action": "s3:ListBucket",
            "Resource": "arn:aws:s3:::example-bucket"
        }
    ]
}
```

## 차이점 요약

|구분|IAM Role|Resource-based Policies|
|:---|:---|:---|
|정책 첨부 위치|역할에 첨부|리소스에 직접 첨부|
|권한 부여 대상|사용자, 애플리케이션, 서비스 등|특정 리소스에 대한 접근 제어|
|외부 계정 액세스|역할 신뢰 정책을 통해 외부 계정이 역할을 가정할 수 있음|외부 계정의 사용자나 역할에 대해 리소스 접근 권한 부여|
|사용 사례|AWS 서비스 간 액세스, 임시 권한 부여|S3 버킷, SQS, SNS, CloudWatch Logs, Lambda, API Gateway 등의 리소스 접근 제어|

IAM Role을 이용하여 역할을 가정할 경우, **기존 Permission을 포기하고 Role에 적용된 Permission을 획득해야 함**.

**Resource-based policy**를 사용할 경우 Principal은 자신에게 적용된 Permission을 포기할 필요가 없음.