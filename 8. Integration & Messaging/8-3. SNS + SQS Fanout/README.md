# [SNS + SQS Fanout](https://docs.aws.amazon.com/ko_kr/sns/latest/dg/sns-sqs-as-subscriber.html)

## 과정

* **SNS 주제 생성**  
Amazon SNS에서 주제를 생성함.
* **SQS 큐 생성**  
메시지를 수신할 SQS 큐를 생성함.
* **SNS 주제와 SQS 큐 연결**  
SQS 큐를 SNS 주제에 구독자로 추가함.
* **메시지 게시**  
애플리케이션이 SNS 주제에 메시지를 게시함.
* **메시지 전달**  
SNS가 메시지를 SQS 큐에 전달함.
* **메시지 처리**  
SQS 큐에 메시지가 도착하면 이를 소비하는 애플리케이션이 메시지를 처리함.

## 장점

* **확장성**  
하나의 SNS 주제로 다수의 SQS 큐에 메시지를 전달할 수 있어 확장성이 높음. SQS를 구독자로 점진적으로 추가할 수 있음.
* **비동기 처리**  
SQS를 사용해 메시지를 비동기적으로 처리할 수 있어 시스템의 부하를 줄일 수 있음.
* **내결함성**  
SQS의 내결함성 기능으로 메시지 손실을 방지할 수 있음.

## 단점

* **복잡성**  
SNS와 SQS를 결합해 사용하는 설정이 다소 복잡할 수 있음.
* **지연 시간**  
메시지 전달과 처리에 지연 시간이 발생할 수 있음.

## 특징

* **SQS access policy**를 이용하여 SNS가 SQS에 Topic을 write할 수 있도록 허락하여야 함.
* **Cross-Region Delivery**; 다른 Region에 존재하는 SQS Queue와 연결될 수 있음.
* Fully decoupled, and no data loss

## Architecture Example

![architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/594d0901-006f-4aa1-af18-e6578a2f8d81)

## Summary

* SNS와 SQS를 활용한 Fan Out은 **SNS 주제로 메시지를 게시하고, 이를 여러 SQS 큐로 전달해 비동기적으로 처리하는 방식**임.  
* 이를 통해 확장성과 내결함성을 높일 수 있지만, 설정이 복잡하고 지연 시간이 발생할 수 있음.  
* Access Policy를 통해 SNS에서 SQS로 메시지를 게시할 수 있는 권한을 설정하며, Cross-Region Delivery를 통해 지리적으로 분산된 시스템 간 메시지 전달이 가능함.