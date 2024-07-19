# Design High-Performing Architectures

## Lambda

* 서버리스 아키텍처로 마이그레이션 하는데  AWS Lambda를 아키텍처의 백본으로 사용 할 때 고려해야할 사항.  
    > * AWS Lambda는 기본적으로 AWS-owned VPC에서 작동. 따라서 public internet이나 public AWS API에 접근 가능.  
    > * Lambda가 VPC-enabled가 되면 NAT Gateway를 통해 public subnet으로 route 되어야 함.
    > * 여러 Lambda function에서 code를 재사용하기 위해서는 AWS Lambda Layer를 고려할 필요가 있음.

* 피크시간 동안 밀리초 지연 시간으로 시간당 수백만 개의 요청을 처리하기 위해 최소한의 운영 오버헤드로 충족할 수 있는 방법.
    > * S3 버킷을 사용하여 웹 사이트의 정적 콘첸츠를 호스팅, CloudFront 배포를 실행, 백엔드 API에 Amazon API Gateway 및 **AWS Lambda 함수**를 사용, Amazon DynamoDB에 데이터를 저장.
    > * CloudFront를 사용하여 빠르고 확장 가능한 콘텐츠 배포 가능. 캐시를 사용하여 밀리초 대기 시간 보장.
    > * Amazon DynamoDB는 고성능의 NoSQL 데이터베이스로서, 초당 수백만 요청을 처리할 수 있으며, 지연 시간이 매우 낮음.
    > * **서버리스**: AWS Lambda와 API Gateway를 사용하면 서버를 직접 관리할 필요가 없으므로 운영 오버헤드가 크게 줄음. 또한, Lambda는 수요에 따라 자동으로 확장됨.

## AWS Global Accelerator

* UDP 프로토콜을 사용하여 지연시간이 짧은 라이브 스포츠 결과를 배포하기 위한 방법.
    > * 전 세계 사용자에게 high-performance, availability를 유지하는 애플리케이션을 배포할 수 있는 방법으로 [AWS Global Accelerator](https://aws.amazon.com/ko/global-accelerator/)가 있음.

## Amazon CloudFront

* ALB 뒤의 Amazon EC2 인스턴스에서 웹 애플리케이션을 호스팅 중. 또한, Amazon Route53에 등록된 자체 도메인 이름을 사용 중. 이 때, 정적 데이터와 동적 데이터가 존재하고, 정적 데이터는 Amazon S3에 저장. 정적 데이터 및 동적 데이터의 성능을 개선하고 대기시간을 줄이기 위한 방법.
    > * Route 53 -> Amazon CloudFront -> [Amazon S3(정적 데이터), ALB(동적 데이터)]
    > * CloudFront는 전 세계의 엣지 로케이션을 사용하여 콘텐츠를 캐시하므로, 사용자에게 더 가까운 서버에서 콘텐츠를 제공하여 지연 시간을 줄이고 성능을 향상.
    > * Route 53을 사용하여 트래픽을 CloudFront로 라우팅하면, 사용자 도메인 이름을 그대로 사용하면서 CloudFront의 성능 향상 기능을 활용할 수 있음.

* Amazon S3에서 정적 웹사이트를 호스팅하고 DNS에 Amazon Route 53을 사용하고 있을 때, 웹사이트에 액세스하는 사용자의 대기시간을 줄이기 위해 가장 비용 효율적인 방법.
    > * Amazon CloudFront 배포를 추가하고, Route 53 항목을 CloudFront 배포로 변경하면 됨.
    > * CloudFront를 S3 버킷 앞에 두면 웹사이트 콘텐츠를 전 세계 사용자에게 가까운 곳에서 캐시하여 전체적인 대역폭 사용량을 줄이고, 사용자가 웹사이트에 접근할 때의 대기 시간을 현저히 줄일 수 있음.
    > * CloudFront는 콘텐츠를 엣지 위치에 캐시하여 원본(S3)에 직접적으로 요청하는 횟수를 줄이고, S3에서의 데이터 전송 등 추가 비용을 최소화함.
    
## Amazon RedShift

* Amazon Redshift를 사용하여 데이터 웨어하우징 솔루션을 구축하고, 1년 이후의 데이터를 Amazon S3로 옮기더라도 해당 데이터와 일일 데이터를 비교할 수 있는 기능을 유지하는 방법.
    > * [Amazon Redshift](https://aws.amazon.com/ko/blogs/big-data/amazon-redshift-spectrum-extends-data-warehousing-out-to-exabytes-no-loading-required/)는 대규모 데이터 세트 저장 및 분석을 위해 설계된 완전 관리형 페타바이트 규모의 클라우드 기반 데이터 웨어하우스 제품.
    > * Amazon Redshift Spectrum에서 Amazon Redshift Cluster 테이블을 이용하여 S3의 historical data를 pointing하여 query를 쉽게 할 수 있음.

## Network Load Balancer

* 퍼블릭 서브넷에 여러 인스턴스를 프로비저닝하고 이러한 인스턴스 ID를 [NLB](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html) 대상으로 지정하여 올바르게 라우팅하는 방법.
    > * 인스턴스 ID를 사용하여 대상을 지정하는 경우 트래픽은 인스턴스의 기본 네트워크 인터페이스에 지정된 Primary Private IP 주소를 사용하여 인스턴스로 라우팅 됨.

## EC2

* EC2 User Data의 특징.
    > * User data는 EC2 인스턴스를 처음 실행했을 때만 실행 됨.
    > * User data는 root user 권한으로만 실행됨.

* 애플리케이션 간의 네트워크 성능이 높을 때 가장 잘 수행되는 분산 데이터 처리 프레임워크를 AWS에 배포할 때 해당 성능을 최대화 하기 위한 방법.
    > * [Placement Group](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/placement-groups.html)의 차이점을 알아야 함.
    > * **Cluster Placement Group 사용**.
    > * 단일 가용 영역 내 인스턴스의 논리적인 그룹으로, 동일한 클러스터에 배치된 인스턴스는 네트워크 대기 시간이 짧고 네트워크 처리량이 높음. 대부분의 네트워크 트래픽이 그룹 내 인스턴스 간에 발생하는 경우에 권장 됨.
    > * Partition: 다른 파티션에 있는 인스턴스 그룹과 기본 하드웨어를 공유하지 않도록 논리적으로 분산.
    > * Spread: 연관된 오류를 줄이기 위해 서로 다른 기본 하드웨어에 소규모 인스턴스 그룹을 엄격하게 배치.

* 일주일 동안 예정된 이벤트를 위해 특정 AWS 리전의 3개의 특정 가용 영역에서 보장된 Amazon EC2 용량이 필요한데, 이를 확보하기 위한 방법.
    > * [온디맨드 용량](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-1.%20EC2#ec2-cost-optimization) 예약을 필요한 지역과 3개의 가용영역을 지정하여 생성.
    > * 특정 리전 내에서 사용할 EC2 인스턴스 용량을 예약함으로써, 요청한 가용 영역에 필요한 EC2 인스턴스를 보장.
    > * 예상치 못한 인스턴스 부족을 방지할 수 있음.
    > * **주의**: 예약 인스턴스는 1~3년 정도의 장기용이므로 사용하면 안 됨.


## AWS DataSync

* 애프리케이션 마이그레이션을 위해 AWS Direct Connect 연결을 만들고, 기존 애플리케이션은 매일 비디오파일을 NFS 파일 시스템에 write 함. 마이그레이션 후에는 Amazon EFS 파일시스템이 탑재된 Amazon EC2 인스턴스에서 애플리케이션을 호스팅할 예정. 마이그레이션 중단 전에 온프레미스에서 생성된 비디오파일을 EFS 파일 시스템에 복제하는 방법
    > * 온프레미스 서버에 [AWS DataSync](https://aws.amazon.com/ko/datasync/)를 구성.
    > * Private VIF를 사용하여 AWS Direct Connect 연결을 통해 AWS EFS용 Private Link 인터페이스 VPC endpoint로 데이터를 전송.
    > * 24시간마다 비디오 파일을 Amazon EFS 파일 시스템으로 보내도록 AWS DataSync 예약 작업 설정.

## AWS FSx for Lustre

* 병렬 및 분산 방식으로 빠르게 처리되고 저장되어야 하는 '핫 데이터', 저렴한 비용으로 읽기 및 업데이트를 위한 빠른 액세스를 통해 참조용으로 보관되어야 하는 '콜드 데이터'와 같은 데이터 들을 빠르게 처리할 수 있는 서비스.
    > * [AWS FSx for Lustre](https://aws.amazon.com/ko/fsx/lustre/)는 '핫 데이터'를 병렬 및 분산 방식으로 처리 함.
    > * 또한, Amazon S3에 '콜드 데이터'를 쉽게 저장할 수 있는 기능을 제공.
    > * AWS FSx for Lustre(고성능 파일 시스템): 기계학습, 고성능 컴퓨팅, 비디오 처리, 재무 모델리와 같은 워크로드에 사용.
    > * 스토리지가 컴퓨팅 속도를 따라가기 원하는 빠른 스토리지가 필요한 애플리케이션을 위해 설계됨.

## AWS Kinesis

* IoT 데이터를 Amazon Kinesis Data Stream(KDS)로 처리 중인데, 생산 되는 데이터와 이를 처리하는 애플리케이션 사이의 데이터 전달 속도에 지연이 발생할 때 해결 방법.
    > * Amazon Kinesis Data Stream의 [Enhanced Fanout](https://aws.amazon.com/ko/blogs/aws/kds-enhanced-fanout/) 기능 사용.
    > * Enhanced Fanout을 통해 여러 샤드를 생성할 수 있고, 샤드의 수가 늘어남에 따라 애플리케이션이 받아 처리할 수 있는 데이터의 양도 증가 함.

* 수백만 건의 정보를 다른 여러 내부 애플리케이션과 공유할 수 있는 확장 가능한 실시간 솔루션이 필요함. 또한, 민감한 데이터를 제거하기 위해 트랜잭션을 처리 후 데이터베이스에 저장하기 위한 방법.
    > * 트랜잭션 데이터를 [Amazon Kinesis Data Streams](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-4.%20AWS%20Kinesis/8-4-1.%20Kinesis%20Data%20Streams)로 스트리밍. AWS Lambda 통합을 사용하여 모든 트랜잭션에서 민감한 데이터를 제거한 다음, Amazon DynamoDB에 트랜잭션 데이터를 저장. 다른 애플리케이션은 Kinesis Data Streams의 트랜잭션 데이터를 사용 가능.
    > * Amazon Kinesis Data Streams를 사용하여 대규모 데이터를 실시간으로 처리하고, 여러 내부 애플리케이션에 제공 가능. 또한, 수평적으로 확장 가능.
    > * AWS Lambda를 사용하여 각 거래에서 민감한데이터를 제거하고 DynamoDB에 저장 가능. 이를 통해, 데이터를 실시간으로 처리하고 저장할 수 있음.

## Amazon Neptune

* 복잡한 쿼리를 처리하려고 할 때 가장 적합한 AWS 데이터베이스 서비스.
    > * [Amazon Neptune](https://aws.amazon.com/ko/neptune/)은 빠르고 안정적이며 완벽하게 관리되는 그래프 데이터베이스 서비스.
    > * 수 많은 관계를 저장하고, 밀리초의 지연시간으로 그래프를 쿼리하는 데 최적화된 특수 목적의 고성능 그래프 데이터베이스 엔진.
    > * 읽기 전용 복제본, 특정 시점으로 복구, Amazon S3에 대한 지속적인 백업, 가용 영역 간 복제 기능을 갖춘 고가용성을 제공.
    > * 처리량이 높은 대화형 그래프 쿼리를 지원하여 소셜 네트워킹 애플리케이션을 구축할 수 있음.

## Amazon Aurora

* Amazon RDS for MySQL을 사용하고, 읽기 복제본을 생성 했는데도 성능에 문제가 발생. 전 세계에서 글로벌 규모로 작동하게끔 하기 위한 비용 효율적인 솔루션.
    > * [Amazon Aurora 글로벌 데이터베이스](https://aws.amazon.com/ko/rds/aurora/global-database/)를 사용하여 각 지역에서 짧은 지연 시간으로 빠른 로컬 읽기를 지원.

## Amazon EBS

* Amazon EC2 인스턴스를 종료하면 연결된 Amazon EBS 볼륨도 손실되는 것에 대한 설명.
    > * Amazon EBS 볼륨은 Amazon EC2 인스턴스의 [루트 볼륨](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/RootDeviceStorage.html)으로 구성 됨.
    > * 인스턴스 종료 시 연결된 루트 볼륨도 종료하는 것이 기본. 하지만 종료되지 않고 유지되도록 변경할 수 있음.

## Amazon EFS

* 웹 사이트에서 항목 카탈로그에 Amazon EC2 인스턴스 스토어를 사용. 해당 카탈로그가 가용성이 높고 내구성이 있는 위치에 저장되길 원할 때의 방법.
    > * 카탈로그를 [Amazon EFS](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-2.%20EFS) 로 이동.
    > * Amazon EC2 인스턴스 스토어는 EC2 인스턴스에 로컬로 연결된 일시적인 스토리지를 제공.
    > * 이는 인스턴스가 중단되거나 종료될 때, 데이터가 영구적으로 보존되지 않음.
    > * Amazon EFS는 여러 가용 영역에 걸쳐 자동으로 데이터를 복제하고, 고가용성과 내구성(지정된 연도 동안 11 9s - 99.999999999%)을 제공하는 완전 관리형 파일 시스템. 

## Amazon Database Migration Service(DMS)

* Amazon S3 버킷에 존재하는 데이터와 로그 파일을 Amazon Kinesis Data Streams로, 새로 S3에 저장되는 데이터를 지속적으로 업데이트 스트리밍 할 때, 가장 빠른 방법.

    > * AWS DMS를 Amazon S3와 Amazon Kinesis Data Streams 간의 브릿지로 활용.
    > * AWS DMS를 사용하면 데이터를 관계형 데이터 베이스, 데이터 웨어하우스, 스트리밍 플랫폼 및 AWS 클라우드의 기타 데이터 스토어로 원활하게 마이그레이션 할 수 있음.
    > * [AWS DMS를 사용하면 새로 코드를 작성하지 않고도 실시간 분석을 위해 Amazon S3에서 Amazon Kinesis Data Streams로 데이터를 스트리밍하도록 기존 애플리케이션을 확장할 수 있음](https://aws.amazon.com/ko/blogs/big-data/streaming-data-from-amazon-s3-to-amazon-kinesis-data-streams-using-aws-dms/).

## NAT(Network Address Translation)

* VPC내의 Private Subnet에 존재하는 인스턴스가 NAT 인스턴스 또는 NAT 게이트웨이를 사용하여 인터넷으로의 outbound IPv4 트래픽을 시작하도록 하는데 옳은 것을 고르기.

    > * [NAT 인스턴스](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html) 또는 [NAT 게이트웨이](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html)는 VPC의 Public Subnet에서 사용하면 Private Subnet의 인스턴스가 인터넷으로의 아웃바운드 IPv4 트래픽을 시작할 수 있음.
    > * NAT 인스턴스는 bastion server로 사용될 수 있음.
    > * NAT 인스턴스는 port forwarding을 지원함.
    > * 보안 그룹은 NAT 인스턴스와 연결될 수 있음.
    > * [NAT Gateway vs NAT Instances](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html)

## AWS Snowball

* NFS를 사용하여 온프레미스 네트워크 연결 스토리지에 비디오 파일을 저장하는데, 총 스토리지는 70TB이고 이를 Amazon S3로 마이그레이션하기 위해 최소한의 네트워크 대역폭을 사용하며 가능한 빨리 전송하는 방법.

    > * [AWS Snowball](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-4.%20Snow%20Family) Edge Job
    > * Snowball Edge 장치를 사용하면 대규모 데이터를 물리적으로 전송할 수 있어, 네트워크 대역폭에 대한 의존성을 줄이고 전송 속도를 크게 높일 수 있음.
    > * Snowball Edge는 데이터를 암호화하여 안전하게 AWS로 전송 가능.
    > * Snowball Edge Storage Optimized 디바이스를 사용하여 약 80TB까지 전송할 수 있으며, 더 큰 용량은 병렬 또는 순차적으로 전송 가능.

## Amazon SQS

* 애플리케이션은 AWS Lambda 함수를 사용하여  Amazon API Gateway를 통해 정보를 수신하고 데이터베이스에 정보를 저장함. 대용량 데이터를 처리하기 위해 Lambda 할당량을 크게 늘려야 할 때, 확장성을 개선하고 구성 노력을 최소화하기 위한 방법.
    > * 두 개의 Lambda 함수를 설정하고, 하나는 정보를 수신할 기능, 하나는 데이터베이스에 로드하는 기능을 구현.
    > * Amazon SQS를 사용하여 Lambda 함수 통합.
    > * [Amazon SQS](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-1.%20Amazon%20SQS)
    > * 자동으로 메시지를 대기열에 저장하고 여러 소비자에게 분산할 수 있어 확장성이 뛰어남.
    > * Lambda 함수와 SQS 모두 AWS 관리형 서비스로, 별도의 서버 관리가 필요 없으며 자동으로 확장됨.
    > * SQS를 사용하면 데이터 수신과 데이터베이스 로드를 분리하여 각 작업의 부하를 분산할 수 있음.
    > * 메시지 대기열을 통해 비동기 처리가 가능해져, 데이터베이스 로드 작업이 지연되더라도 데이터 수신 작업에 영향을 주지 않음.

## Amazon AppFlow

* 애플리케이션은 데이터 수집을 위해 여러 SaaS 소스와 통합됨. Amazon EC2 인스턴스를 실행하여 데이터를 수신하고 분석을 위해 데이터를 Amazon S3 버킷에 업로드하는데, 업로드가 완료되면 사용자에게 알림을 보냄. 이 때, 성능 개선을 위해 최소한의 운영 오버헤드를 실현하는 방법.
    > * Amazon AppFlow 흐름을 생성하여 각 SaaS 소스와 S3 버킷 간의 데이터를 전송. S3 버킷에 전송이 완료되면 [Amazon SNS](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-2.%20Amazon%20SNS) 주제에 이벤트를 보내도록 설정.
    > * Amazon AppFlow는 관리형 서비스로, SaaS 소스에서 직접 데이터를 추출하고 Amazon S3, Amazon RedShift로 전송하여 데이터 수집 및 업로드 과정을 최적화함.
    > * 추가적인 인프라나 서버 관리 없이도 손쉽게 SaaS 소스와의 데이터 통합 구현 가능.
    > * AppFlow를 사용하면 엔터프라이즈급 규모에 원하는 빈도로 비즈니스 이벤트에 대한 응답 또는 온디맨드 데이터 플로우를 실행 가능.
    > * 필터링 및 검증과 같은 데이터 변환 기능을 구성하여 추가 단계 없이 플로우 자체의 일부로 바로 사용 가능한 풍부한 데이터 생성 가능.

## Amazon API Gateway

* 데이터가 스트리밍될 때 데이터를 변환하는 프로세스 API와 데이터를 위한 스토리지 솔루션이 필요할 때, 최소한의 운영 오버헤드로 해결하는 방법.
    > * **Amazon Kinesis Data Stream**으로 데이터를 보내도록 **Amazon API Gateway API**를 구성.
    > * Kinesis 데이터 스트림을 데이터 원본으로 사용하는 **Amazon Kinesis Data Firehose** 전송 스트림 생성.
    > * AWS Lambda 함수를 사용하여 데이터를 변환.
    > * Kinesis Data Firehose 전송 스트림을 사용하여 Amazon S3로 데이터를 보냄.
    > * **Amazon API Gateway**
    > * 어떤 규모에서든 개발자가 API를 손쉽게 게시, 유지 관리, 모니터링 및 보호할 수 있도록 지원하는 **완전관리형 서비스**.
    > * 트래픽 관리, 권한 부여 및 액세스 제어, 모니터링, API 버전 관리를 비롯해 최대 수십만 건의 동시 API 호출을 수락 및 처리하는 데 관련된 모든 작업을 처리함. 
    > * API를 호스팅하기 위해 **EC2 인스턴스**를 사용하면 인스턴스 서버 관리, 패치, 유지보수 등의 작업이 필요하여 운영 오버헤드를 증가시킴.
    > * **AWS Glue**는 ETL 작업을 위해 설계된 서비스로, 데이터 변환에 적합하지만 데이터 스트리밍 처리에는 적합하지 않음. 또한 **Amazon S3**를 소스로 함.
    > * **AWS Glue**
    > * 분석, 기계 학습 및 애플리케이션 개발을 위해 데이터를 쉽게 탐색, 준비, 그리고 조합할 수 있도록 지원하는 서버리스 데이터 통합 서비스.
    > * 데이터 카탈로그를 사용하여 데이터를 쉽게 찾고 액세스할 수 있음.