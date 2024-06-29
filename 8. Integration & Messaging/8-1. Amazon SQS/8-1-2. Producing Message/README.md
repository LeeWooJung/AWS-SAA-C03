# Producing Message

* Amazon SQS에서 메시지를 생성하고 큐에 전송하는 과정은 **메시지를 생성하는 애플리케이션** 또는 **서비스가 메시지를 SQS 큐로 보내는 것을 의미**함. 
* 이 과정은 **AWS SDK 또는 API를 사용**하여 이루어지며, 메시지를 큐에 안전하게 저장하고 다른 소비자가 사용할 수 있도록 함.
* SQS에 메시지가 전송되면, **Consumer가 삭제하기 전까지 메시지는 유지** 됨.

## 메시지 생성 프로세스

### AWS SDK 또는 API 사용

* AWS는 다양한 프로그래밍 언어를 위한 SDK를 제공함 (Java, Python, JavaScript, etc.).
* SDK를 사용하면 **메시지를 SQS 큐에 쉽게 전송**할 수 있음.
* 예를 들어, Python의 boto3 라이브러리를 사용하여 메시지를 SQS에 전송할 수 있음.

### 메시지 속성 (Message Attributes)

* 메시지에는 **본문뿐만 아니라 메타데이터를 포함할 수 있는 속성을 추가**할 수 있음.
* 속성은 메시지 라우팅, 필터링 및 추가 정보를 제공하는 데 사용됨.

### 메시지 본문 (Message Body)

* 메시지의 본문은 실제 데이터가 포함된 부분임.
* 본문은 최대 256 KB의 텍스트 또는 바이너리 데이터를 포함할 수 있음.

### 메시지 그룹 ID (Message Group ID)

* **FIFO 큐의 경우 메시지 그룹 ID**를 사용하여 메시지 순서를 유지할 수 있음.
* Standard Queue에서는 이 기능이 필요하지 않음.

## 메시지 생성 예제

``` python
import boto3

# SQS 클라이언트 생성
sqs = boto3.client('sqs')

# 큐 URL
queue_url = 'https://sqs.region.amazonaws.com/account-id/queue-name'

# 메시지 전송
response = sqs.send_message(
    QueueUrl=queue_url,
    MessageBody='Hello, this is a test message!',
    MessageAttributes={
        'Author': {
            'StringValue': 'LEE',
            'DataType': 'String'
        },
        'Priority': {
            'StringValue': 'High',
            'DataType': 'String'
        }
    }
)

print('Message ID:', response['MessageId'])
```

이 예제에서는 boto3 라이브러리를 사용하여 SQS 큐에 메시지를 전송함. 메시지 본문과 함께 Author와 Priority라는 두 가지 속성을 추가함.

## 메시지 속성

메시지 속성은 **메시지 본문 외에 추가로 전송할 수 있는 메타데이터**임.  
속성은 **키-값 쌍으로 구성**되며, 데이터 타입을 명시해야 함.  
메시지 속성의 데이터 타입은 String, Number, Binary 등을 포함함.

``` python
MessageAttributes={
    'AttributeKey': {
        'StringValue': 'AttributeValue',
        'DataType': 'String'
    }
}
```

## 메시지 전송 설정

### DelaySeconds

* 메시지가 큐에 도착한 후 소비자에게 표시되기까지의 **지연 시간을 설정**할 수 있음.
* 최대 15분까지 설정 가능함.

### Message Deduplication ID (FIFO 큐)

* **중복 메시지를 제거하기 위한 고유 식별**자임.
* 동일한 Deduplication ID를 가진 메시지는 큐에 하나만 존재함.

## 메시지 전송 시나리오

* **비동기 작업 요청**

    웹 애플리케이션에서 **사용자 요청을 SQS 큐로 보내고**, 백엔드에서 비동기적으로 처리하는 시나리오임.

* **분산 시스템 간 통신**

    **마이크로서비스 아키텍처에서 서비스 간 메시지를 전송하여 통신을 비동기적**으로 처리함.

* **일괄 처리 작업**

    대량의 데이터를 처리할 때 메시지를 큐에 넣고, 여러 작업자(워커)가 병렬로 작업을 처리함.