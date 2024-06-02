# Design Resilient Architectures

## S3

* Amazon S3에 저장된 객체가 실수로 삭제 되는 것을 방지하는 방법.  
    > * Amazon S3 Bucket에 [Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)을 활성화 하기.
    > * Amazon S3 Bucket 객체 삭제 시, [MFA를 확인](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMFADelete.html)하도록 설정하기.

* Amazon S3에 기록되는 로그 파일을 읽을 때, 기존 로그 파일을 덮어 씌우고 읽을 경우 생기는 데이터 불일치의 해결 방법.
    > * Amazon S3는 [쓰기 후 읽기 일관성을 자동으로 제공](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#ConsistencyModel).
    > * 기존 개체를 덮어 쓴 후 바로 읽기가 가능.

## Amazon API Gateway

* 갑작스러운 트래픽 변화를 처리하기 위해 throttling 하는 방법.
    > * Amazon API Gateway, Amazon SQS, Amazon Kinesis
    > * [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html): 토큰 버킷 알고리즘을 사용하여 API에 대한 요청을 조절.
    > * [Amazon SQS](https://aws.amazon.com/ko/sqs/features/): 메시지 손실이나 지연 시간 증가 없이 일시적인 볼륨 급증을 완화하는 버퍼 기능을 제공.
    > * Amazon Kinesis: 스트리밍 데이터를 실시간으로 수집, 버퍼링 및 처리할 수 있는 확장 가능한 완전 관리형 서비스.

## AWS CloudTrail

* Amazon S3 버킷 설정의 변경을 사용자의 권리를 제한하지 않고 확인하는 방법.
    > * [AWS CloudTrail](https://aws.amazon.com/ko/cloudtrail/)은 AWS 계정의 거버넌스, 규정 준수, 운영 감사 및 위험 감사를 지원하는 서비스.
    > * AWS 계정 내에서 이루어진 API 호출을 분석하는 데 사용.