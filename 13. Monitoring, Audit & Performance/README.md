# Monitoring, Audit & Performance

Monitoring, Audit & Performance와 관련된 요소 설명.

## CloudWatch vs. CloudTrail vs. Config

|특징|CloudWatch|CloudTrail|AWS Config|
|:---|:---|:---|:---|
|주요기능|모니터링 및 로깅, 경고, 메트릭 수집|API 호출 및 사용자 활동 로깅|리소스 구성 및 변경 추적, 규정 준수 관리|
|데이터 유형|시스템 메트릭(CPU, Network 등), 로그, 이벤트|API 호출 이벤트 로그|리소스 구성 상태, 구성 변경 내역|
|주요 사용 사례|애플리케이션 성능 모니터링, 시스템 상태 체크|보안 및 규정 준수 감사, API 호출 추적|리소스 상태 모니터링, 규정 준수 확인, 변경 추적|
|대상 리소스|EC2, RDS, Lambda 등 다양한 AWS 리소스|모든 AWS 서비스의 API 호출|모든 AWS 리소스|
|경고 및 알림|알람 설정 및 경고|API 이벤트 발생 시 알림|규정 위반 시 알림(Deny 불가능)|
|대시보드|메트릭과 로그를 시각화할 수 있는 대시보드|X|X|
|규정 준수 도구|X|보안 및 규정 준수 이벤트 로깅|리소스 구성 상태와 규정 준수 모니터링|
|자동화 기능|경고에 대한 자동화된 대응(Lambda 트리거 등)|X|규정 위반에 대한 자동화된 수정(Remediation)|
|통합 서비스|AWS Lambda, SNS, SQS 등 다양한 서비스와 통합|S3, CloudWatch Logs, SNS와 통합|Lambda, SNS, Systems Manager Automation(SSM Automation)등과 통합|
|로그 보존|사용자 정의 가능(S3에 저장)|기본적으로 90일 보존, 이후 S3로 전송 가능|변경 내역은 영구 보존(기본적으로 7년 이상 저장)|
|설정 방법|메트릭 및 로그 설정, 경고 설정|이벤트 로그를 S3로 전송, SNS 알림 설정|규칙 설정 및 리소스 트래킹 설정|

## Architecture Example

### EventBridge + Cloud Trail

![EventBridge, CloudTrail Architecture](https://github.com/user-attachments/assets/cc2edd1c-138a-4d60-a196-323fb48da8c4)


### EventBridge's Interception of API Calls

![Intercept API Calls Architecture](https://github.com/user-attachments/assets/307359fd-c06c-4aff-bc50-d8be354073a2)

### Use Event Bridge to trigger notifications

![EventBridge architecture](https://github.com/user-attachments/assets/cc8cc208-5dd3-4109-a798-81327a23daef)

### Send configuration change & compliance state notifications to SNS

![SNS architecture](https://github.com/user-attachments/assets/c76c6ae4-8839-4f0e-9895-f5118a6364f7)

## With Elastic Load Balancer

![with Elastic Load Balancer](https://github.com/user-attachments/assets/49974475-2ac5-4639-91bc-ae7c834c5060)

### AWS CloudTrail

* API Call로 Load Balancer에 누가 변화를 줬는지 확인.

### Amazon CloudWatch

* ELB의 Security Group으로 들어오는 Connection과 관련된 Metric을 Monitoring.

* Load Balancer의 Performance와 연관된 Metric을 Dashboard로 표현.

* Error Codes를 시간별로 **퍼센티지**로 표현.

### AWS Config

* Load Balancer의 보안 그룹의 **규칙**을 확인.

* Load Balancer의 **구성 변화**를 확인.

* Load Balancer로 SSL Certificate가 항상 할당되는지 확인(규정 준수, Compliance).