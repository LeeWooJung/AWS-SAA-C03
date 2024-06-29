# Consuming Message

* Amazon SQS에서 메시지를 소비하는 것은 **큐에 있는 메시지를 읽고 처리하는 것을 의미**함.  
* 이는 메시지를 처리하는 애플리케이션 또는 서비스가 **큐에서 메시지를 가져와 필요한 작업을 수행하는 과정**임.  
* 메시지 소비는 AWS SDK 또는 API를 사용하여 이루어짐.

## 메시지 소비 프로세스

### 메시지 수신 (Receive/Poll Message)

* ReceiveMessage API를 호출하여 큐에서 메시지를 가져옴.
* 한 번에 **최대 10개**의 메시지를 수신할 수 있음.
* 메시지는 **기본적으로 최대 12시간 동안 큐에 보관**됨.

### 메시지 처리 (Process Message)

* 수신한 메시지를 애플리케이션 로직에 따라 처리함.
* 처리 중 문제가 발생하면 **메시지를 다시 큐로 반환하거나, 오류 로그에 기록**함.

### 메시지 삭제 (Delete Message)

* 메시지 처리가 완료되면 **DeleteMessage API**를 호출하여 큐에서 메시지를 삭제함.
* 메시지를 삭제하지 않으면, 메시지가 다시 처리될 수 있음.

## 메시지 소비 예제

``` python
import boto3

# SQS 클라이언트 생성
sqs = boto3.client('sqs')

# 큐 URL
queue_url = 'https://sqs.region.amazonaws.com/account-id/queue-name'

# 메시지 수신
response = sqs.receive_message(
    QueueUrl=queue_url,
    MaxNumberOfMessages=10,
    WaitTimeSeconds=10,
    MessageAttributeNames=['All']
)

# 메시지 처리
if 'Messages' in response:
    for message in response['Messages']:
        # 메시지 본문 출력
        print('Message Body:', message['Body'])
        
        # 메시지 속성 출력
        print('Message Attributes:', message.get('MessageAttributes'))
        
        # 메시지 삭제
        receipt_handle = message['ReceiptHandle']
        sqs.delete_message(
            QueueUrl=queue_url,
            ReceiptHandle=receipt_handle
        )
        print('Deleted message:', receipt_handle)
else:
    print('No messages available')
```
이 예제에서는 boto3 라이브러리를 사용하여 SQS 큐에서 메시지를 수신하고, 메시지 본문과 속성을 출력한 후 메시지를 삭제함.

## 메시지 가시성 타임아웃 (Message Visibility Timeout)

* 메시지가 **수신되면 다른 소비자가 해당 메시지를 볼 수 없도록 일정 시간 동안 숨겨짐**.

* 기본 가시성 **타임아웃은 30초**이며, **최대 12시간**까지 설정 가능함.

* 메시지를 처리하는 동안 가시성 타임아웃을 늘리거나 줄일 수 있음.

## 장기 폴링 (Long Polling)

* 장기 폴링을 사용하면 **SQS가 큐에 메시지가 있을 때까지 연결을 유지하여 메시지를 수신**함.

* 네트워크 비용을 절감하고 메시지 수신 지연을 줄일 수 있음.

* WaitTimeSeconds 파라미터를 사용하여 설정함.

## 다중 EC2 인스턴스 소비자 (Multiple EC2 Instances Consumers)

* 여러 EC2 인스턴스가 **동시에 큐에서 메시지를 소비**할 수 있음.

* [Auto Scaling Group](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-2.%20Auto%20Scaling%20Group)을 사용하여 인스턴스를 자동으로 확장하거나 축소할 수 있음.

* 이를 통해 높은 가용성과 확장성을 제공함.

## 장단점

### 장점

* **비동기 처리**  
메시지를 비동기적으로 처리하여 시스템의 응답성을 높일 수 있음.
* **확장성**  
다수의 소비자 인스턴스를 추가하여 처리량을 증가시킬 수 있음.
* **유연성**  
메시지 **가시성 타임아웃**과 **장기 폴링**을 통해 유연한 메시지 소비가 가능함.

### 단점

* **복잡성**  
메시지 소비 로직을 구현하는 데 추가적인 복잡성이 필요함.
* **중복 메시지**  
메시지가 여러 번 소비될 가능성이 있음. 이를 방지하기 위해 중복 제거 로직을 구현해야 함.

## 아키텍처 예시

* **비동기 작업 처리**

    * 웹 애플리케이션에서 사용자 요청을 SQS 큐에 넣고, **백엔드에서 비동기적**으로 처리함.
    * 소비자는 메시지를 처리하고, 결과를 데이터베이스에 저장하거나 다른 서비스로 전송함.

* **분산 작업 처리**

    * 마이크로서비스 아키텍처에서 각 서비스가 독립적으로 메시지를 소비하고 처리함.
    * 예를 들어, 주문 처리 시스템에서 주문 메시지를 큐에 넣고, 여러 소비자가 이를 처리하여 재고를 업데이트하고, 배송을 준비함.

## Sumary

* Amazon SQS에서 메시지를 소비하는 과정은 **메시지를 큐에서 수신하고 처리한 후 삭제**하는 단계를 포함함.  
* **가시성 타임아웃**과 **장기 폴링**을 통해 유연하게 메시지를 처리할 수 있으며, 다수의 EC2 인스턴스 소비자와 **자동 확장 그룹**을 통해 **높은 가용성과 확장성**을 제공할 수 있음.  
* 비동기 처리와 유연성은 장점이지만, 중복 메시지 처리와 복잡성은 단점으로 고려해야 함.