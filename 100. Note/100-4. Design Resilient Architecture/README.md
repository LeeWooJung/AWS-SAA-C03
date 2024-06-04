# Design Resilient Architectures

## S3

* Amazon S3에 저장된 객체가 실수로 삭제 되는 것을 방지하는 방법.  
    > * Amazon S3 Bucket에 [Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)을 활성화 하기.
    > * Amazon S3 Bucket 객체 삭제 시, [MFA를 확인](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMFADelete.html)하도록 설정하기.

* Amazon S3에 기록되는 로그 파일을 읽을 때, 기존 로그 파일을 덮어 씌우고 읽을 경우 생기는 데이터 불일치의 해결 방법.
    > * Amazon S3는 [쓰기 후 읽기 일관성을 자동으로 제공](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#ConsistencyModel).
    > * 기존 개체를 덮어 쓴 후 바로 읽기가 가능.

* Amazon S3 버킷에 존재하는 대용량 데이터를 딱 한 번 복사하여 [다른 지역의 Amazon S3로 이동](https://repost.aws/ko/knowledge-center/move-objects-s3-bucket)시키려 할 때 사용할 수 있는 방법(Snowball은 사용하지 않음).
    > * AWS S3 Sync를 사용하여 원본 버킷에서 대상 버킷으로 데이터를 복사.
    > * Amazon S3 batch [replication](https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html)을 설정하여 데이터를 복사하여 이동시킨 다음, replication 삭제. 이를 이용하면 객체를 비동기식으로 자동으로 복사할 수 있음. 

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

## AWS Aurora

* AWS Aurora를 사용하는 애플리케이션에 요청 비율이 주기적으로 급증할 때를 대비해 애플리케이션의 탄력성을 높이기 위한 방법.
    > * AWS Aurora Replica를 생성하여 데이터 읽기를 분산시킬 수 있음.
    > * AWS Aurora Replica는 가용성을 높일 수 있음. Primary Instance(Write 전용)이 문제가 생겼을 때, Replica가 Prmiary Instance를 대체하여 문제를 해결할 수 있음.
    > * 추가적으로, Amazon CloudFront를 사용하여 오리진 장애 조치 기능을 제공할 수 있음.

* [Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.html)를 사용하는데, 데이터베이스 읽기로 인해 높은 입출력이 발생하여 데이터베이스에 대한 쓰기 요청에 대한 대기 시간이 늘어날 때 해결할 수 있는 방법.
    > * Read Replica를 생성하여 애플리케이션의 endpoint를 수정.

## AWS DynamoDB

* 여러 도시의 주요 지표 데이터를 키-값 쌍 형식으로 AWS 클라우드로 보낼 때, 고가용성있고 안정적으로 저장하기 위한 서비스.
    > * Amazon DynamoDB는 키-값 및 문서 데이터베이스로 밀리초의 성능을 제공함.
    > * 보안, 백업 및 복원, 인메모리 캐싱을 갖춘 완전관리형, 다중 지역, 다중 마스터, 내구성이 뛰어난 데이터베이스.
    > * Amazon DynamoDB를 AWS Lambda와 결합하여 지표 데이터를 키-값 데이터로 처리할 수 있음.

## Amazon Kinesis

* 수집된 데이터를 실시간 분석하는 스트리밍 시스템을 만들고, 데이터를 분석 후 모바일 애플리케이션에 알림을 보내는 방법.
    > * [Amazon Kinesis](https://aws.amazon.com/ko/kinesis/)를 사용하면 스트리밍 데이터를 쉽게 수집, 처리 및 분석할 수 있음.
    > * Amazon Kinesis를 사용하면 기계 학습, 분석 및 기타 애플리케이션을 위한 비디오, 오디오, 로그, 웹사이트 클릭 스트림 및 IoT 원격 측정 데이터와 같은 실시간 데이터를 수집할 수 있음.
    > * [Amazon SNS](https://aws.amazon.com/ko/sns/)는 알림을 보낼 수 있음.

* 회사의 특수한 요구사항에 맞게 스트리밍 데이터를 처리하고 분석하는 사용자 지정 애플리케이션을 구축하기 위해 필요한 AWS 서비스.
    > * [Amazon Kinesis Data Streams](https://aws.amazon.com/ko/kinesis/data-streams/)를 사용하여 데이터 스트림을 처리하고, 실시간 데이터 프로세서에 대한 생산자와 소비자를 분리.

## Amazon CloudWatch

* 애플리케이션의 CPU가 특정 임계값을 위반할 때마다 이메일로 알림받기 위해 사용할 수 있는 AWS 서비스.
    > * [Amazon CloudWatch](https://aws.amazon.com/ko/cloudwatch/faqs/)는 애플리케이션을 모니터링하고, 시스템 전반의 성능 변화에 대응, 리소스 활용도를 최적화하고, 운영 상태에 대한 통합 보기를 얻을 수 있음.
    > * Amazon SNS는 높은 처리량, 푸시 기반, 다대다 메시징을 기반으로 알림을 보냄.

## Amazon SQS

* [Amazon SQS](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html) 표준 대기열에서 FIFO 대기열로 마이그레이션 하기 위해 확인해야할 것.
    > * FIFO Queue의 throughput이 초당 3,000 개의 메세지가 넘지 않도록 해야 함.
    > * FIFO Queue의 이름이 .fifo 로 끝나도록 해야 함.
    > * 표준 Queue를 삭제하고 FIFO Queue를 새로 생성해야 함.
    > * Amazon SQS는 메시지 지향 미들웨어 관리 및 운영과 관련된 복잡성과 오버헤드를 제거하고 개발자가 작업에 집중할 수 있도록 지원함.

## Amazon RDS

* 온프레미스에서 Oracle 데이터베이스와 호스트 운영체제(OS)를 사용하는 애플리케이션을 실행하는데, Oracle 데이터베이스 계층의 가용성을 향상시키기 위해 사용할 수 있는 AWS 서비스.
    > * [Amazon RDS Custom for Oracle](https://aws.amazon.com/ko/blogs/aws/amazon-rds-custom-for-oracle-new-control-capabilities-in-database-environment/)을 사용.
    > * 데이터베이스 서버 호스트 및 운영 체제에 액세스하고 사용자 정의할 수 있음.
    > * 고가용성을 위해 다중 AZ 구성을 사용할 수 있음.
    > * Amazon RDS는 클라우드에서 관계형 데이터베이스를 쉽게 설정, 운영 및 확장할 수 있는 관리형 서비스이지만 데이터베이스의 호스트 OS에 대한 액세스는 허용하지 않음. 따라서 RDS Custom for Oracle을 사용해야 함.