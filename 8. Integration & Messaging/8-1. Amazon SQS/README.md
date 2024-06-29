# [SQS](https://docs.aws.amazon.com/ko_kr/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/0e9af410-4b41-4f3b-aa03-bc13f268c260" width = "30" height = "30"> AWS SQS

* Amazon SQS는 AWS에서 제공하는 **메시지 큐 서비스**로, **애플리케이션 구성 요소 간의 메시지 전송을 쉽게 할 수 있도록 설계**되었음.  
* 이는 분산 애플리케이션의 구성 요소 간의 통신을 **비동기적으로 처리**할 수 있게 해주며, **메시지의 유실을 방지하고, 시스템을 더욱 탄력적**으로 만들 수 있음.

## 주요 개념

### 메시지 가시성 시간 초과 (Message Visibility Timeout)

* 메시지를 **소비자가 처리하는 동안 다른 소비자들이 해당 메시지를 보지 못하게 하는 시간**.  
* 기본값은 30초이며, 최대 12시간까지 설정 가능함. 
* 이는 메시지를 처리하는 시간이 주어진다는 의미임. 
* 주어진 시간이 끝나면, 메시지는 다시 보임. 
* 만약 주어진 시간 동안 메시지를 처리하지 못하면, 해당 메시지는 두 번 처리될 수 있음. 
* **ChangeMessageVisibility** API를 호출하여 메시지 처리 시간을 조금 더 달라고 요청할 수 있음.

### 롱 폴링 (Long Polling)

* 큐에 메시지가 없을 때도 **연결을 유지하여, 메시지가 도착할 때까지 기다리는 방식**.
* 불필요한 요청을 줄이고 비용을 절감할 수 있음. 
* Wait time은 1s ~ 20s까지 정해질 수 있으나, 20s가 권장됨. 
* Queue Level에서 활성화 되거나, **WaitTimeSeconds** API Level에서 활성화 가능.