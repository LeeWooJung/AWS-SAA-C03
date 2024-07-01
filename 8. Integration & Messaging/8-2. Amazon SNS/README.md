# [SNS](https://aws.amazon.com/ko/sns/)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/2aa50df2-4f78-4596-a969-7bdf1a22b5e7" width = "30" height = "30"> AWS SNS

* Amazon Simple Notification Service (SNS)는 고도로 **확장 가능하고, 비용 효율적이며, 유연한 메시징 서비스로, 마이크로서비스, 분산 시스템, 서버리스 애플리케이션의 통신을 쉽게 해줌**.  
* SNS를 통해 애플리케이션 간의 메시지를 신속하게 전달하고, 알림을 전송하며, 데이터 처리를 트리거할 수 있음.
* 많은 AWS Services가 알람을 위해 SNS로 직접적으로 메시지를 전송할 수 있음.

## 정의 및 개념

### 정의  
* Amazon SNS는 **주제 기반의 메시징 서비스로**, **발행-구독**(publish-subscribe) 모델을 사용하여 메시지를 여러 구독자에게 전달함.

### 개념  
* SNS는 주제(Topic)와 구독(Subscription)을 사용함.  
* **주제는 메시지를 보유하고, 구독자는 주제에서 메시지를 받음**.  
* 주제에 메시지를 게시하면 모든 구독자가 해당 메시지를 수신함.

## 주요 기능

* **주제**(Topic)  
    * 메시지를 게시할 수 있는 엔드포인트.  
    * 각 주제는 고유의 **ARN**(Amazon Resource Name)을 가짐.

* **구독**(Subscription)  
    * 주제에 대한 메시지를 수신하는 엔드포인트.  
    * **이메일, SMS, HTTP/HTTPS, AWS Lambda 함수, Amazon SQS 큐 등을 포함**할 수 있음.

* **메시지 게시**(Publishing Messages)  
    * 발행자가 주제에 메시지를 게시하면, 해당 메시지가 모든 구독자에게 전달됨.

* **메시지 필터링**(Message Filtering)  
    * 특정 조건에 따라 **구독자가 메시지를 필터링하여 필요한 메시지만 수신**할 수 있음.
    * 만약 Filtering policy가 없다면 Subscriber는 모든 메시지를 받게 됨.

* **FIFO 주제**  
    * **순서 보장과 중복 제거**가 필요한 경우, FIFO 주제를 사용할 수 있음.
    * Message Group ID 별로 Ordering 할 수 있음.
    * Deduplication ID를 사용하여 중복을 제거할 수 있음.
    * SQS FIFO Queue를 Subscriber로 사용할 수 있음.
    * SQS FIFO와 같은 제한된 Throughput을 가짐.

## Architecture
Amazon SNS는 **발행-구독 모델**을 기반으로 동작하며, 다음과 같은 아키텍처 요소를 포함.

* **주제**(Topic)  
**메시지를 게시할 수 있는 기본 엔드포인트**로, 다양한 유형의 구독자를 연결할 수 있음. 최대 100,000개의 Topic 생성 가능.

* **구독**(Subscription)  
**주제에 연결된 엔드포인트**로, 주제에 게시된 메시지를 수신함. 하나의 Topic에 최대 12,500,000개의 구독 가능.

* **발행자**(Publisher)  
주제에 메시지를 게시하는 역할을 하며, **애플리케이션, 서버리스 함수, 사용자 인터페이스 등 다양한 소스에서 메시지를 게시**할 수 있음.

* **구독자**(Subscriber)  
주제의 메시지를 수신하는 역할을 하며, **이메일, SMS, HTTP/HTTPS 엔드포인트, AWS Lambda 함수, Amazon SQS 큐 등 다양한 형식으로 구독**할 수 있음.

## How to publish

### Topic Publish

Topic Publish는 **주제를 통해 다수의 구독자에게 메시지를 전송하는 방법**임.  
이 방법을 사용하면 한 번의 게시로 여러 엔드포인트에 메시지를 전달할 수 있음.

* **과정**
    * 주제를 생성함.
    * 구독자를 주제에 추가함. 구독자는 이메일, SMS, HTTP/HTTPS 엔드포인트, SQS 큐, Lambda 함수 등이 될 수 있음.
    * 메시지를 주제에 게시함. 이 메시지는 주제에 구독된 모든 엔드포인트로 전송됨.

* **장점**
    * **확장성**  
    한 번의 게시로 다수의 구독자에게 메시지를 전송할 수 있음.
    * **관리 편의성**  
    주제를 중심으로 구독자를 관리할 수 있음.
    * **다양한 프로토콜 지원**  
    다양한 종류의 엔드포인트를 구독자로 추가할 수 있음.

* **단점**
    * **지연 시간**  
    구독자 수가 많을수록 메시지 전송에 시간이 걸릴 수 있음.

* **아키텍처 예시**  
애플리케이션이 주제에 메시지를 게시하면, 주제에 구독된 여러 엔드포인트(예: 이메일, SQS, Lambda)가 메시지를 수신함.

### Direct Publish

Direct Publish는 **특정 엔드포인트로 직접 메시지를 전송하는 방법**임.  
주로 **모바일 푸시 알림**에 사용됨.  
이 방법을 통해 특정 디바이스나 애플리케이션 엔드포인트로 직접 메시지를 보낼 수 있음.

* **과정**
    * 엔드포인트(예: 모바일 디바이스)를 SNS에 등록함.
    * **등록된 엔드포인트의 ARN을 사용하여 메시지를 직접 게시**함.

* **장점**
    * **타겟팅**  
    특정 엔드포인트로 직접 메시지를 보낼 수 있어 타겟팅이 용이함.
    * **효율성**  
    다수의 구독자를 관리할 필요 없이 필요한 엔드포인트로 바로 메시지를 전송할 수 있음.

* **단점**  
    * **유연성 부족**  
    다수의 엔드포인트로 메시지를 전송하려면 각각의 엔드포인트에 대해 별도로 메시지를 게시해야 함.
    * **복잡성**  
    다수의 엔드포인트를 직접 관리해야 함.

* **아키텍처 예시**  
특정 모바일 디바이스에 대한 푸시 알림을 전송할 때, 해당 **디바이스의 ARN을 사용하여 메시지를 직접 게시**함.

## Security

### IAM 정책

* AWS IAM(Identity and Access Management)을 사용하여 SNS 주제와 관련된 **액세스 권한을 제어**(Access Control)할 수 있음.

    ``` json
    {
    "Version": "2012-10-17",
    "Statement": [
        {
        "Effect": "Allow",
        "Action": "sns:Publish",
        "Resource": "arn:aws:sns:region:account-id:topic-name",
        "Condition": {
            "ArnEquals": {
            "aws:SourceArn": "arn:aws:iam::account-id:role/role-name"
            }
        }
        }
    ]
    }
    ```
    SNS Topic 게시 권한을 부여하는 정책.

### 주제 정책

* **주제 자체에 정책을 설정**(SNS Access Policies, S3 bucket policies와 비슷함)하여 특정 IAM 사용자 또는 역할에게만 게시할 수 있도록 제한할 수 있음.
* Cross-account access에 유용함.
* 다른 AWS Service가 SNS Topic 을 작성하도록 하기에 유용함.
    ``` json
    {
        "Version": "2012-10-17",
        "Id": "__default_policy_ID",
        "Statement": [
            {
                "Effect": "Allow",
                "Principal": {
                    "AWS": "arn:aws:iam::account-id:role/role-name"
                },
                "Action": "SNS:Publish",
                "Resource": "arn:aws:sns:region:account-id:topic-name"
            }
        ]
    }
    ```

### SSL/TLS

* HTTPS 프로토콜을 사용하여 **전송 중 데이터를 암호화**함.
* AWS 콘솔이나 SDK, CLI에서 HTTPS 엔드포인트를 사용하도록 설정할 수 있음.

### 서버 측 암호화(Server-Side Encryption, SSE)

* SNS 주제에 대해 **서버 측 암호화**를 활성화하여 메시지를 안전하게 저장할 수 있음.
* **AWS KMS**(Key Management Service)와 통합하여 데이터 암호화 키를 관리함.

### VPC 엔드포인트

* VPC 내에서 **프라이빗하게 SNS에 액세스할 수 있도록 VPC 엔드포인트를 설정**할 수 있음.
* 이를 통해 인터넷을 거치지 않고 안전하게 SNS와 통신할 수 있음.

### Client side encyption

* Client 측에서 Encryption/Decryption을 진행할 수 있음.

## 장점

* **확장성**  
수백만 명의 구독자와 수십만 개의 주제를 처리할 수 있음. 

* **유연성**  
다양한 유형의 구독자를 지원하며, 메시지 필터링을 통해 원하는 메시지만 수신할 수 있음.

* **비용 효율성**  
사용한 만큼만 지불하며, **초기 비용 없이 시작**할 수 있음.

* **고가용성**  
여러 가용 영역에 걸쳐 메시지를 복제하여 높은 가용성을 보장함.

## 단점

* **복잡성**  
대규모 시스템에서 많은 주제와 구독을 관리하는 것이 복잡할 수 있음.

* **메시지 전송 지연**  
HTTP/HTTPS 엔드포인트를 사용할 때 네트워크 지연이 발생할 수 있음.

* **제한된 메시지 크기**  
메시지 크기가 **256KB로 제한**되어 있어, 큰 데이터는 다른 서비스를 사용해야 함.

## Use Case

* **알림 시스템**  
사용자에게 이메일, SMS, 푸시 알림 등을 전송하는 시스템.

* **마이크로서비스 통신**  
분산 시스템에서 **마이크로서비스 간의 메시징을 처리**함.

* **서버리스 애플리케이션**  
**AWS Lambda 함수를 트리거하여 데이터 처리나 워크플로우를 실행**함.

## 비교

* **Amazon SQS**  
메시지 대기열 서비스로, 주로 **비동기 작업 처리와 워크로드 분산**에 사용됨.

* **Amazon SNS**  
**발행-구독 모델**로, 여러 구독자에게 메시지를 동시에 전송함.

## Summary

Amazon SNS는 **주제 기반의 발행-구독 모델**을 통해 메시지를 여러 구독자에게 효율적으로 전달하는 고도로 확장 가능하고 유연한 메시징 서비스임. 주로 알림 시스템, 마이크로서비스 간의 통신, 서버리스 애플리케이션에서 사용됨.  
다양한 구독 타입을 지원하며, **메시지 필터링을 통해 필요한 메시지만 수신**할 수 있음.