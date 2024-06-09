# [S3 Event Notifications](https://docs.aws.amazon.com/AmazonS3/latest/userguide/EventNotifications.html)

## S3 Event Notifications

* Amazon S3의 Event Notification은 S3 버킷에서 발생하는 **특정 이벤트**(예: 객체 생성, 객체 삭제 등)에 대해 알림을 보내는 기능.  
* 이를 통해 개발자는 S3 버킷에서 발생하는 이벤트에 대해 실시간으로 대응할 수 있음.
* 대부분 몇 초 이내에 event가 전송되지만, 종종 몇 분 혹은 더 오래 걸릴 때도 있음.

### 주요 개념 및 기능
* **이벤트 유형 (Event Types)**  
    * **s3:ObjectCreated**  
    객체 생성 이벤트 (PUT, POST, COPY, or CompleteMultipartUpload)
    * **s3:ObjectRemoved**  
    객체 삭제 이벤트 (Delete, DeleteMarkerCreated)
    * **s3:ObjectRestore**  
    객체 복원 이벤트 (RestoreInitiated, RestoreCompleted)
    * **s3:Replication**  
    객체 복제 이벤트(OperationFailedReplication, OperationMissedThreshold, OperationReplicatedAfterThreshold)
    * **s3:ReducedRedundancy**  
    Reduced Redundancy Storage (RRS) 객체 손실 이벤트

* **알림 대상** (Notification Destinations)  
    * **Amazon SNS** (Simple Notification Service)  
    주로 알림 메시지를 여러 수신자에게 방송하는 데 사용.
    * **Amazon SQS** (Simple Queue Service)  
    큐에 메시지를 저장하여 나중에 처리할 수 있도록 함.
    * **AWS Lambda**  
    이벤트가 발생할 때 자동으로 지정된 Lambda 함수를 호출하여 코드를 실행.

* **구성 방법**  
    * S3 콘솔, AWS CLI, SDK 또는 API를 사용하여 S3 이벤트 알림을 구성할 수 있음.
    * 이벤트 알림을 설정하려면, 버킷에서 발생하는 특정 이벤트 유형과 알림을 받을 대상(예: SNS 주제, SQS 큐, Lambda 함수)을 지정.

### Use Case

* **실시간 이미지 처리**  
    * 새로운 이미지가 S3 버킷에 업로드될 때 **Lambda 함수를 트리거**하여 이미지 리사이징, 메타데이터 추출, 썸네일 생성 등을 자동으로 처리.

* **데이터 파이프라인 트리거**  
    * S3에 새로운 데이터 파일이 업로드될 때, 이 이벤트를 **SQS 큐에 전달**하여 데이터 파이프라인의 다음 단계(예: 데이터 변환, 로드 등)를 트리거.

* **모니터링 및 알림**  
    * 중요한 객체가 삭제될 때 SNS를 통해 팀에 알림을 보내거나, 객체가 생성될 때 특정 조건에 따라 경고를 생성.

### 장점
* **실시간 대응**  
S3 버킷에서 발생하는 이벤트에 대해 실시간으로 반응할 수 있음.
* **자동화**  
다양한 작업(예: 데이터 처리, 로그 분석 등)을 자동화하여 운영 효율성을 높임.
* **확장성**  
이벤트 알림을 통해 다양한 AWS 서비스와 연동하여 확장 가능한 아키텍처를 구현할 수 있음.

## IAM Permission

AWS S3 이벤트를 Amazon SNS, SQS, 그리고 Lambda로 전달하기 위해서는 해당 서비스에 대한 올바른 권한을 설정하는 **IAM 정책**이 필요함.

### From S3 to SNS Example

```json
    {
    "Version": "2012-10-17",
    "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "sns:Publish"
      ],
      "Resource": "arn:aws:sns:us-east-1:123456789012:YourSNSTopic",
      "Condition": {
        "ArnLike": {
            "aws:SourceArn": "arn:aws:s3:::MyBucket"
        }
      }
    }
  ]
}
```

### From S3 to SQS Example

```json
    {
    "Version": "2012-10-17",
    "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "sqs:SendMessage"
      ],
      "Resource": "arn:aws:sqs:us-east-1:123456789012:YourSQSQueue",
      "Condition": {
        "ArnLike": {
            "aws:SourceArn": "arn:aws:s3:::MyBucket"
        }
      }
    }
  ]
}

```

### From S3 to Lambda Example

```json
    {
    "Version": "2012-10-17",
    "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "lambda:InvokeFunction"
      ],
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:YourLambdaFunction",
      "Condition": {
        "ArnLike": {
            "aws:SourceArn": "arn:aws:s3:::MyBucket"
        }
      }
    }
  ]
}

```

## EventBridge

* Amazon EventBridge를 이용하여 S3 이벤트를 Notification 하는 것은 매우 유연하고 강력한 방법임.  
* EventBridge를 사용하면 **이벤트 기반 아키텍처를 쉽게 구축할 수 있으며, AWS 서비스나 자체 애플리케이션에서 발생하는 이벤트를 다양한 타겟으로 전달할 수 있음**.
* **EventBridge**  
    * EventBridge는 이벤트 소스에서 이벤트를 수신하고 이를 규칙에 따라 다양한 타겟으로 라우팅하는 서비스.  
    * S3에서 발생하는 이벤트(예: 객체 생성, 삭제)를 EventBridge로 전송하고, EventBridge는 이를 지정된 타겟(예: Lambda, SNS, SQS, Step Functions, Kinesis Streams, Kinesis Firehose 등)으로 전달.

### 구성 요소

* **Event Source**  
S3 버킷에서 발생하는 이벤트.
* **EventBridge Rule**  
특정 이벤트 패턴에 일치하는 이벤트를 감지하고 타겟으로 라우팅하는 규칙.
* **Targets**  
이벤트를 처리할 AWS 서비스나 애플리케이션 (예: Lambda 함수, SNS, SQS).

### 장점
* **유연성**  
다양한 타겟으로 이벤트를 라우팅할 수 있어 이벤트 기반 아키텍처를 쉽게 구현할 수 있음.
* **확장성**  
EventBridge는 AWS 서비스와의 통합이 원활하며, 대규모 이벤트 처리에 적합.
* **운영 관리 간소화**  
EventBridge를 사용하면 이벤트 소스와 타겟 간의 직접적인 연동을 관리할 필요 없이 규칙을 통해 간접적으로 관리할 수 있음.