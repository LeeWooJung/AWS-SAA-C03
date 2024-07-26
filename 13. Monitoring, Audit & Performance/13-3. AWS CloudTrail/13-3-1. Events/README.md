# [CloudTrail Events](https://docs.aws.amazon.com/ko_kr/awscloudtrail/latest/userguide/cloudtrail-events.html)

CloudTrail Events는 **AWS 계정 내에서 발생하는 API 호출을 기록한 데이터 항목**임. 

이러한 이벤트는 **누가, 언제, 어떤 액션을 수행했는지에 대한 상세 정보를 제공**함으로써 **보안, 운영, 규정 준수 요구사항을 충족**시키는 데 도움을 줌.

## 이벤트 유형

### Management Events

AWS 계정 내에서 **리소스 생성, 수정, 삭제와 같은 관리 작업을 기록**함. 

기본적으로 **CloudTrail은 Management Events를 기록하도록 구성됨**.

**Read Events**(리소스를 수정하지 못함)와 **Write Events**(리소스를 수정할 수도 있음)로 구분할 수 있음.

예를 들어, EC2 인스턴스를 시작하거나 S3 버킷을 생성하는 작업이 포함됨.

* **Example**

    * Configuring Security(IAM AttachRolePolicy)
    * Configuring rules for routing data(Amazon EC2 CreateSubnet)
    * Setting up logging(AWS CloudTrail CreateTrail)

### Data Events

**S3 객체 수준의 API 활동(GetObject, DeleteObject, PutObject) 및 AWS Lambda 함수 실행(Invoke API)을 기록**함. 

이는 더 세분화된 이벤트를 추적하고 모니터링할 수 있게 함.

기본적으로 **Data Events는 기록되지 않음**(용량을 많이 차지하기 때문)

**Read Events**(리소스를 수정하지 못함)와 **Write Events**(리소스를 수정할 수도 있음)로 구분할 수 있음.

### Insights Events

**비정상적이거나 잠재적으로 위험한 활동을 감지하고 이에 대한 알림을 제공**함. 

Normal management를 분석하여 baseline을 형성함. 그 후, 비정상적인 패턴을 확인하기 위해 **지속적으로 Write Events를 분석함**.

* **아키텍처**

    1) Management Events에서 Event들을 불러옴.
    2) CloudTrail Insight에서 이를 계속적으로 분석함.
    3) 비정상적인 활동이 감지되면 이를 CloudTrail Console, S3 Bucket, EventBridge 등으로 전송함.

다음과 같은 **비정상** 활동이 있음.

* **Example**

    * inaccurate resource provisioning
    * hitting service limits
    * Bursts of AWS IAM actions
    * Gaps in periodic maintenance activity

## 구성요소

* **EventTime**: 이벤트가 발생한 시간임.
* **EventName**: 실행된 API 호출의 이름임.
* **EventSource**: 이벤트가 발생한 AWS 서비스의 이름임.
* **UserIdentity**: 이벤트를 트리거한 사용자의 정보임.
* **EventID**: 각 이벤트를 고유하게 식별하는 ID임.
* **AWSRegion**: 이벤트가 발생한 AWS 리전임.
* **SourceIPAddress**: API 요청이 발생한 IP 주소임.
* **RequestParameters**: API 요청에 사용된 매개변수임.
* **ResponseElements**: API 요청에 대한 응답 내용임.

## Events Retention

Events는 CloudTrail에 **90일 동안 저장**됨.

이보다 더 긴 시간동안 저장하길 원하면, **S3에 저장하여 Athena로 분석해야 함**.

## Summary

CloudTrail Events는 AWS 계정 내에서 발생하는 API 호출을 기록한 데이터 항목으로, 보안, 운영, 규정 준수 요구사항을 충족시키는 데 도움을 줌. 

이벤트는 **Management Events, Data Events, Insights Events**로 구분되며, 각각의 이벤트는 이벤트 시간, API 호출 이름, 발생 소스, 사용자 정보 등 다양한 구성요소를 포함함. 

이를 통해 보안 감사, 운영 문제 해결, 규정 준수를 효과적으로 지원할 수 있음.