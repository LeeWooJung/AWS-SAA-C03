# Design Resilient Architectures

## S3

* Amazon S3에 저장된 객체가 실수로 삭제 되는 것을 방지하는 방법.  
    > * Amazon S3 Bucket에 [Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html)을 활성화 하기.
    > * Amazon S3 Bucket 객체 삭제 시, [MFA를 확인](https://docs.aws.amazon.com/AmazonS3/latest/userguide/UsingMFADelete.html)하도록 설정하기.
    > * [S3 MFA Delete 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3/6-3-12.%20S3%20MFA%20Delete)

* Amazon S3에 기록되는 로그 파일을 읽을 때, 기존 로그 파일을 덮어 씌우고 읽을 경우 생기는 데이터 불일치의 해결 방법.
    > * Amazon S3는 [쓰기 후 읽기 일관성을 자동으로 제공](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html#ConsistencyModel).
    > * 기존 개체를 덮어 쓴 후 바로 읽기가 가능.

* Amazon S3 버킷에 존재하는 대용량 데이터를 딱 한 번 복사하여 [다른 지역의 Amazon S3로 이동](https://repost.aws/ko/knowledge-center/move-objects-s3-bucket)시키려 할 때 사용할 수 있는 방법(Snowball은 사용하지 않음).
    > * AWS S3 Sync를 사용하여 원본 버킷에서 대상 버킷으로 데이터를 복사.
    > * Amazon S3 batch [replication](https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html)을 설정하여 데이터를 복사하여 이동시킨 다음, replication 삭제. 이를 이용하면 객체를 비동기식으로 자동으로 복사할 수 있음.
    > * [S3 Batch Operations 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3/6-3-8.%20Batch%20Operations)

## Amazon API Gateway

* 갑작스러운 트래픽 변화를 처리하기 위해 throttling 하는 방법.
    > * Amazon API Gateway, Amazon SQS, Amazon Kinesis
    > * [Amazon API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-request-throttling.html): [토큰 버킷 알고리즘을 사용하여 API에 대한 요청을 조절](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-7.%20AWS%20API%20Gateway#%ED%8A%B8%EB%9E%98%ED%94%BD-%EA%B4%80%EB%A6%AC).
    > * [Amazon SQS](https://aws.amazon.com/ko/sqs/features/): 메시지 손실이나 지연 시간 증가 없이 일시적인 볼륨 급증을 완화하는 버퍼 기능을 제공.
    > * Amazon Kinesis: 스트리밍 데이터를 실시간으로 수집, 버퍼링 및 처리할 수 있는 확장 가능한 완전 관리형 서비스.

## AWS CloudTrail

* Amazon S3 버킷 설정의 변경을 사용자의 권리를 제한하지 않고 확인하는 방법.
    > * [AWS CloudTrail](https://aws.amazon.com/ko/cloudtrail/)은 AWS 계정의 거버넌스, 규정 준수, 운영 감사 및 위험 감사를 지원하는 서비스.
    > * AWS 계정 내에서 이루어진 API 호출을 분석하는 데 사용.
    > * [AWS CloudTrail 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/13.%20Monitoring%2C%20Audit%20%26%20Performance/13-3.%20AWS%20CloudTrail)

## AWS Aurora

* AWS Aurora를 사용하는 애플리케이션에 요청 비율이 주기적으로 급증할 때를 대비해 애플리케이션의 탄력성을 높이기 위한 방법.
    > * AWS Aurora Replica를 생성하여 데이터 읽기를 분산시킬 수 있음.
    > * AWS Aurora Replica는 가용성을 높일 수 있음. Primary Instance(Write 전용)이 문제가 생겼을 때, Replica가 Prmiary Instance를 대체하여 문제를 해결할 수 있음.
    > * 추가적으로, Amazon CloudFront를 사용하여 오리진 장애 조치 기능을 제공할 수 있음.
    > * [Aurora Replica Auto Scaling 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-2.%20Amazon%20Aurora/7-2-3.%20Replica%20Auto%20Scaling)

* [Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/Aurora.Overview.html)를 사용하는데, 데이터베이스 읽기로 인해 높은 입출력이 발생하여 데이터베이스에 대한 쓰기 요청에 대한 대기 시간이 늘어날 때 해결할 수 있는 방법.
    > * Read Replica를 생성하여 애플리케이션의 endpoint를 수정.

## AWS DynamoDB

* 여러 도시의 주요 지표 데이터를 키-값 쌍 형식으로 AWS 클라우드로 보낼 때, 고가용성있고 안정적으로 저장하기 위한 서비스.
    > * [Amazon DynamoDB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-4.%20Amazon%20DynamoDB)는 키-값 및 문서 데이터베이스로 밀리초의 성능을 제공함.
    > * 보안, 백업 및 복원, 인메모리 캐싱을 갖춘 완전관리형, 다중 지역, 다중 마스터, 내구성이 뛰어난 데이터베이스.
    > * Amazon DynamoDB를 AWS Lambda와 결합하여 지표 데이터를 키-값 데이터로 처리할 수 있음.

## Amazon Kinesis

* 수집된 데이터를 실시간 분석하는 스트리밍 시스템을 만들고, 데이터를 분석 후 모바일 애플리케이션에 알림을 보내는 방법.
    > * [Amazon Kinesis](https://aws.amazon.com/ko/kinesis/)를 사용하면 스트리밍 데이터를 쉽게 수집, 처리 및 분석할 수 있음.
    > * Amazon Kinesis를 사용하면 기계 학습, 분석 및 기타 애플리케이션을 위한 비디오, 오디오, 로그, 웹사이트 클릭 스트림 및 IoT 원격 측정 데이터와 같은 실시간 데이터를 수집할 수 있음.
    > * [Amazon SNS](https://aws.amazon.com/ko/sns/)는 알림을 보낼 수 있음.
    > * [Amazon SNS 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-2.%20Amazon%20SNS)

* 회사의 특수한 요구사항에 맞게 스트리밍 데이터를 처리하고 분석하는 사용자 지정 애플리케이션을 구축하기 위해 필요한 AWS 서비스.
    > * [Amazon Kinesis Data Streams](https://aws.amazon.com/ko/kinesis/data-streams/)를 사용하여 데이터 스트림을 처리하고, 실시간 데이터 프로세서에 대한 생산자와 소비자를 분리.
    > * [Kinesis Data Streams 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-4.%20AWS%20Kinesis/8-4-1.%20Kinesis%20Data%20Streams)

## Amazon CloudWatch

* 애플리케이션의 CPU가 특정 임계값을 위반할 때마다 이메일로 알림받기 위해 사용할 수 있는 AWS 서비스.
    > * [Amazon CloudWatch](https://aws.amazon.com/ko/cloudwatch/faqs/)는 애플리케이션을 모니터링하고, 시스템 전반의 성능 변화에 대응, 리소스 활용도를 최적화하고, 운영 상태에 대한 통합 보기를 얻을 수 있음.
    > * Amazon SNS는 높은 처리량, 푸시 기반, 다대다 메시징을 기반으로 알림을 보냄.

* AWS에서 실행되는 애플리케이션에서 인프라 메트릭 경보를 구현해야 함. CPU 사용률이 단기간에 50%이상으로 증가하는 경우에는 **회사는 조치를 취할 필요가 없**지만, CPU 사용률이 50% 이상으로 증가하고 디스크의 읽기 IOPS가 동시에 높다면, 회사에서 최대한 빨리 조치를 취해야 함. 또한 **오경보를 줄여야 함**. 이 때 방법.
    > * 가능한 경우 **Amazon CloudWatch 복합 경보 생성**(composite alarm).
    > * **CloudWatch Composite Alarm**
    > * **다중 조건 설정**: [CloudWatch Composite Alarm](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/13.%20Monitoring%2C%20Audit%20%26%20Performance/13-1.%20Amazon%20CloudWatch/13-1-5.%20CloudWatch%20Alarms#composite-alarms)을 사용하면 여러 개의 단일 경보를 조합하여 특정 조건이 충족될 때만 경보가 발생하도록 설정할 수 있음. 
    > * **거짓 경보 감소**: 두 개 이상의 단일 지표가 특정 조건을 충족할 때만 경보를 발생시키므로, 단일 지표의 일시적인 스파이크로 인한 거짓 경보를 줄일 수 있음.
    > * 복합 경보의 모든 기본 경보는 복합 경보와 **동일한 AWS 계정 및 리전**에 있어야 함.
    > * CF. **Amazon CloudWatch Synthesis**
    > * 애플리케이션의 end-to-end 사용자 경험을 모니터링하기 위해 사용됨.
    > * 전체 트랜잭션에서 끊어진 링크나 작동하지 않는 링크, 단계별 작업 완료, 페이지 로드 오류, UI 자산의 로드 지연 시간, 복잡한 마법사 흐름 또는 체크아웃 흐름을 모니터링. 

## Amazon SQS

* [Amazon SQS](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html) 표준 대기열에서 FIFO 대기열로 마이그레이션 하기 위해 확인해야할 것.
    > * FIFO Queue의 throughput이 초당 3,000 개의 메세지가 넘지 않도록 해야 함.
    > * FIFO Queue의 이름이 .fifo 로 끝나도록 해야 함.
    > * 표준 Queue를 삭제하고 FIFO Queue를 새로 생성해야 함.
    > * Amazon SQS는 메시지 지향 미들웨어 관리 및 운영과 관련된 복잡성과 오버헤드를 제거하고 개발자가 작업에 집중할 수 있도록 지원함.
    > * [Amazon SQS Queue 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-1.%20Amazon%20SQS/8-1-1.%20Queue)

* 새 데이터 전송에 대한 알림을 수신하는 **Amazon SNS**, 주제 데이터를 처리하고 저장하는 **AWS Lambda**를 사용하는 워크플로우가 있는데, 네트워크 연결 문제로 인해 때때로 수집 워크플로가 실패함. 장애가 발생하면 수동으로 작업을 재실행하지 않는 이상, 데이터를 수집하지 않음. 모든 데이터를 최종적으로 처리되도록 하는 방법.
    > * **Amazon Simple Queue Service**(SQS) 대기열을 장애 발생 대상으로 구성함. 대기열의 메시지를 처리하도록 Lambda 함수를 수정.
    > * **메시지 저장 및 재시도**: Amazon SQS는 메시지를 안전하게 저장하고, 네트워크 장애나 처리 실패가 발생했을 때 메시지를 손실 없이 보존함. Lambda 함수가 데이터를 처리하는 도중에 네트워크 장애가 발생하면, SQS는 메시지를 큐에 저장하고, 문제가 해결 된 후 Lambda 함수가 다시 메시지를 처리하도록 함.
    > * **내결함성**: SQS는 내결함성을 제공하여, 메시지를 여러 가용 영역에 중복 저장함으로써 데이터 손실을 방지함. 이 덕에 네트워크 장애나 다른 문제로 인해 메시지가 손실되지 않도록 보장함.
    > * **자동 재시도**: Lambda 함수가 SQS로부터 메시지를 가져와 처리할 때 오류가 발생하면, SQS는 자동으로 재시도를 함.
    > * [Amazon SQS Consuming Msg 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-1.%20Amazon%20SQS/8-1-3.%20Cosuming%20Message)

## Amazon RDS

* 온프레미스에서 Oracle 데이터베이스와 호스트 운영체제(OS)를 사용하는 애플리케이션을 실행하는데, Oracle 데이터베이스 계층의 가용성을 향상시키기 위해 사용할 수 있는 AWS 서비스.
    > * [Amazon RDS Custom for Oracle](https://aws.amazon.com/ko/blogs/aws/amazon-rds-custom-for-oracle-new-control-capabilities-in-database-environment/)을 사용.
    > * 데이터베이스 서버 호스트 및 운영 체제에 액세스하고 사용자 정의할 수 있음.
    > * 고가용성을 위해 다중 AZ 구성을 사용할 수 있음.
    > * Amazon RDS는 클라우드에서 관계형 데이터베이스를 쉽게 설정, 운영 및 확장할 수 있는 관리형 서비스이지만 데이터베이스의 호스트 OS에 대한 액세스는 허용하지 않음. 따라서 RDS Custom for Oracle을 사용해야 함.
    > * [RDS Custom 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-1.%20Amazon%20RDS/7-1-4.%20RDS%20Custom)

## EC2

* Amazon [Elastic Beanstalk](https://aws.amazon.com/ko/elasticbeanstalk/) 배포에서 새 인스턴스를 생성하는데 걸리는 시간을 2분 미만으로 만들 수 있는 방법.
    > * Amazon EC2 User Data를 사용하여 Dynamic installation 이 부팅시 작용하도록 지정.
    > * Standard AMI에 포함되지 않은 소프트웨어를 설치해야 하는 경우 사용자 지정 AMI가 프로비저닝 시간을 향상 시킬 수 있음.
    > * [Golden AMI](https://aws.amazon.com/ko/blogs/awsmarketplace/announcing-the-golden-ami-pipeline/)를 사용하여 정적인 설치 구성 요소를 설치하도록 설정.
    > * [Elastic Beanstalk 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-3.%20Elastic%20Beanstalk)
    > * [AMI 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-1.%20EC2/3-1-3.%20AMI)

* Auto Scaling 그룹에서 선택된 [launch configuration](https://docs.aws.amazon.com/autoscaling/ec2/userguide/launch-configurations.html)이 애플리케이션 워크 플로우를 처리하는 데 최적화 되지 않은 잘못된 인스턴스 유형을 사용할 때 해결 방법.
    > * 새로운 시작 구성(Launch Configuration)을 생성하고 Auto Scaling 그룹에서 해당 구성을 사용하도록 수정.
    > * 이전 시작 구성은 삭제.
    > * 시작 구성이 생성되면 더 이상 수정할 수 없음. 따라서 기존 구성을 삭제하고 새로운 구성을 생성해야 함.

* single Spread [placement group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html)(단일)을 사용하여 애플리케이션을 실행중인데 최적의 성능을 발휘하기 위해 15개의 EC2 인스턴스가 필요. 15개의 인스턴스를 배포하는데 필요한 가용 영역(AZ)의 개수.
    > * **3개**
    > * [Spread placement group](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-1.%20EC2/3-1-1.%20Placement%20Groups#spread)은 각각 별도의 랙에 배치된 인스턴스 그룹으로, 각 랙에는 자체 네트워크와 전원이 있음.
    > * 별도로 유지해야 하는 중요한 인스턴스의 수가 적은 애플리케이션에는 분산 배치 그룹을 사용하는 것이 좋음.
    > * Spread placement group은 동일한 지역의 여러 가용 영역에 걸쳐있을 수 있는데, 그룹별 가용 영역당 **최대 7개**의 인스턴스를 실행할 수 있음.

## AWS Global Accelerator

* 48시간 내에 블루-그린 배포를 테스트하려고 하는데 사용자는 DNS 캐싱이 발생하기 쉬운 휴대폰을 사용함. 이 때, 많은 사용자를 대상으로 배포 테스트를 하기 위해 사용할 수 있는 옵션.
    > * [AWS Global Accelerator](https://aws.amazon.com/ko/blogs/networking-and-content-delivery/using-aws-global-accelerator-to-achieve-blue-green-deployments/)를 사용하여 트래픽의 일부를 특정 배포에 분산 시킬 수 있음.
    > * AWS Global Accelerator는 엔드포인트 가중치를 사용하여 엔드포인트 그룹의 엔드포인트로 전달되는 트래픽의 비율을 결정.
    > * AWS Global Accelerator를 사용하면 클라이언트 장치 등의 DNS 캐싱에 영향을 받지 않고 블루 환경과 그린 환경 사이에서 트래픽을 점진적으로 또는 한꺼번에 이동할 수 있음.
    > * [AWS Global Accelerator 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main?tab=readme-ov-file)

## AWS DMS(Database Migration Service)

* 사용중이거나 추가 될 데이터를 지속적으로 복제하고 데이터를 Amazon RedShift로 스트리밍하고자 할 때, 기본 인프라를 관리할 필요 없이 개발 시간이 가장 적게 필요하고, 리소스 효율성이 가장 높은 솔루션.
    > * [AWS DataMigration Service](https://aws.amazon.com/ko/dms/)(DMS)를 사용하여 데이터베이스의 데이터를 Amazon Redshift로 복제.
    > * **AWS DMS**  
    > * 데이터베이스를 AWS로 빠르고 안전하게 마이그레이션하는데 도움이 됨.  
    > * 소스 데이터베이스는 마이그레이션 중에도 완벽하게 작동하므로 데이터베이스에 의존하는 애플리케이션의 가동 중지 시간이 최소화 됨.
    > * Amazon RedShift, Amazon S3로 스트리밍하여 고가용성으로 데이터를 지속적으로 복제할 수 있음.
    > * [AWS Database Migration Service 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/16.%20Disaster%20Recovery%20%26%20Migrations/16-1.%20Database%20Migration%20Service)

## AWS DataSync

* 온프레미스 데이터 센터를 AWS로 마이그레이션 함. 데이터 센터는 **NFS**기반 파일 시스템에 데이터를 저장하는 **SFTP** 서버를 호스팅 함. 서버는 Amazon EFS를 사용하는 Amazon EC2 인스턴스에서 호스팅 되어야 함. 해당 작업을 자동화 하기 위한 방법.
    > * 온프레미스 데이터 센터에 **AWS DataSync** 에이전트를 설치.
    > * [AWS DataSync](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main?tab=readme-ov-file)를 사용하여 온프레미스 SFTP 서버에 적합한 **위치 구성**을 생성.
    > * AWS DataSync는 온프레미스 데이터를 AWS로 안전하고 신속하게 전송하기 위해 설계된 서비스. 온프레미스에 설치되어 데이터를 자동으로 전송 가능.
    > * DataSync는 소스와 대상 위치를 지정하여 데이터를 전송할 수 있도록 구성함.
    > * 온프레미스 SFTP 서버를 소스로, AWS EFS 파일 시스템을 대상으로 구성하면 됨.
    > * DataSync를 사용하여 전송 작업을 스케줄링하거나 자동화 할 수 있어 전송 과정이 간편해짐.

## AWS Direct Connect

* 회사의 온프레미스 인프라를 AWS로 확장하는 하이브리드 아키텍처를 설계 중. AWS 리전에 대해 일관된 짧은 지연 시간 및 고가용성 연결이 필요. 비용을 최소화 하는 대신, 기본 연결이 실패할 경우 더 느린 트래픽을 기꺼이 수용할 때 사용할 수 있는 방법.
    > * 리전에 대해 **AWS Direct Connect** 연결을 프로비저닝.
    > * Direct Connect 연결이 실패할 경우, 백업으로 **VPN 연결**을 프로비저닝.
    > * **AWS Direct Connect**는 전용 네트워크 연결을 통해 AWS와 온프레미스 인프라 간의 고성능, 저지연 연결을 제공.
    > * Direct Connect 연결 장에 발생에 대한 대첵으로 [VPN 연결을 백업](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/15.%20VPC/15-13.%20Direct%20Connect(DX)#with-site-to-site-vpn-backup)으로 설정할 수 있음.

## Application Load Balancer(ALB)

* HTTP 애플리케이션은 NLB(Network Load Balancer) 뒤에 있고, 해당 애플리케이션을 실행하는 EC2 인스턴스는 Auto Scaling Group에 속함. NLB는 HTTP 오류를 감지하지 못함. 사용자 정의 스크립트나 코드를 작성하지 않고, 애플리케이션의 가용성을 개선하는 방법.
    > * [NLB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-3.%20Network%20Load%20Balancer)를 [ALB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-2.%20Application%20Load%20Balancer)로 교체함.
    > * 애플리케이션의 URL을 제공하여 HTTP 상태를 확인하고, 비정상적인 인스턴스가 교체되도록 Auto Scaling 작업을 구성함.
    > * **ALB**: HTTP 및 HTTPS 트래픽 처리에 적합한 로드 밸런스. OSI 7계층에서 동작.
    > * **NLB**: TCP, UDP 및 TLS 트래픽 처리에 적합한 로드 밸런서. OSI 4계층인 전송계층에서 동작함.