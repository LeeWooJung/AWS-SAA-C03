# [Kinesis Data Firehose](https://docs.aws.amazon.com/ko_kr/firehose/latest/dev/what-is-this-service.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/ae1f0512-0b1e-44b4-b696-900770303a0b" width = "30" height = "30"> Kinesis Data Firehose

* Amazon Kinesis Data Firehose는 **실시간 스트리밍 데이터를 Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, Splunk와 같은 데이터 스토어로 로드**하는 **완전 관리형 서비스** 및 Serverless임.  
* 다양한 데이터의 **배치, 압축, 변환 및 암호화 기능을 제공**하여 데이터의 처리 및 저장을 간소화함.
* Near Real Time: 버퍼 interval을 0 ~ 900 초까지 설정 가능하며, 버퍼 사이즈는 최소 1MB임.
* 실패한 데이터 혹은 전체 데이터의 백업을 위해 S3 Bucket으로 전송할 수 있음.

## 기능

### 자동 스케일링  
Firehose는 데이터 **수집 용량을 자동으로 조정**하여 증가하는 데이터 처리량에 대응할 수 있음.

### 데이터 변환  
Lambda 함수를 사용하여 **스트리밍 데이터를 실시간으로 변환 가능**함.

### 배치 데이터  
데이터를 배치로 수집하여 S3와 같은 대상에 저장할 수 있음.

### 데이터 압축 및 암호화  
데이터를 **전송 중에 압축하고 암호화**할 수 있음.

### 모니터링 및 경보  
**Amazon CloudWatch**를 통해 Firehose 스트림의 상태와 성능을 모니터링할 수 있음.

## 아키텍처

### 데이터 생산자  
* Firehose에 데이터를 전송하는 소스임.  
* 예를 들어, 웹 애플리케이션, IoT 디바이스 등이 있음.

### Firehose 전송 스트림  
* 데이터를 받아서 **대상 데이터 스토어로 전송하는 스트림**임.

### 데이터 변환  
* 필요에 따라 **Lambda 함수를 사용하여 데이터를 변환**할 수 있음.

### 데이터 저장  
* 변환된 데이터는 설정된 대상(S3, Redshift, Elasticsearch, Splunk 등)에 저장됨.

### Example

![kinesis data firehose architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/fd9ee22a-6cd7-4e6d-a498-5f4adf1b49d2)


## 구성 요소

### Delivery Stream  
* Firehose 스트림은 데이터를 전송하고 변환하는 파이프라인임.

### Destination  
* 데이터가 전송될 최종 목적지임.  
* S3, Redshift, Elasticsearch Service, Splunk 등이 있음.

### Lambda Function  
* 스트리밍 데이터의 실시간 변환을 위한 Lambda 함수임.

## 장점

### 완전 관리형  
별도의 인프라 관리 없이 실시간 데이터 수집 및 전송 가능함.

### 실시간 데이터 처리  
데이터를 실시간으로 변환 및 전송할 수 있음.

### 확장성  
자동으로 스케일링하여 증가하는 데이터 처리량에 대응 가능함.

### 다양한 대상 지원  
여러 AWS 서비스 및 타사 서비스와 통합 가능함.

### 간편한 설정  
몇 번의 클릭만으로 데이터 파이프라인을 설정할 수 있음.

## 단점

### 비용  
대량의 데이터를 실시간으로 전송하는 경우 **비용이 발생**할 수 있음.

### 제한된 변환 기능  
복잡한 데이터 변환에는 추가적인 작업이 필요할 수 있음.

### 지연 시간  
실시간 처리가 가능하지만, 일부 경우 데이터 전송에 약간의 지연이 발생할 수 있음.

## Use Case

### 로그 및 이벤트 데이터 분석  
애플리케이션 로그와 이벤트 데이터를 실시간으로 수집하여 분석 및 모니터링 가능함.

### IoT 데이터 처리  
IoT 디바이스에서 수집한 데이터를 실시간으로 처리하고 저장할 수 있음.

### 실시간 스트리밍 데이터 분석  
실시간 스트리밍 데이터를 분석 플랫폼으로 전송하여 실시간 분석을 수행할 수 있음.

### 데이터 웨어하우징  
스트리밍 데이터를 데이터 웨어하우스로 전송하여 배치 분석 가능함.

## 요약

* Amazon Kinesis Data Firehose는 실시간 스트리밍 데이터를 다양한 데이터 스토어로 전송하는 완전 관리형 서비스임.  
* 자동 스케일링, 데이터 변환, 배치 데이터 수집, 데이터 압축 및 암호화 기능을 제공함.  
* 주요 사용 사례로는 로그 및 이벤트 데이터 분석, IoT 데이터 처리, 실시간 스트리밍 데이터 분석, 데이터 웨어하우징 등이 있음.  
* 완전 관리형 서비스로 인프라 관리의 부담을 줄여주지만, 비용과 제한된 변환 기능 등 몇 가지 단점이 있음.