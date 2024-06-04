# Design High-Performing Architectures

## Lambda

* 서버리스 아키텍처로 마이그레이션 하는데  AWS Lambda를 아키텍처의 백본으로 사용 할 때 고려해야할 사항.  
    > * AWS Lambda는 기본적으로 AWS-owned VPC에서 작동. 따라서 public internet이나 public AWS API에 접근 가능.  
    > * Lambda가 VPC-enabled가 되면 NAT Gateway를 통해 public subnet으로 route 되어야 함.
    > * 여러 Lambda function에서 code를 재사용하기 위해서는 AWS Lambda Layer를 고려할 필요가 있음.

## AWS Global Accelerator

* UDP 프로토콜을 사용하여 지연시간이 짧은 라이브 스포츠 결과를 배포하기 위한 방법.
    > * 전 세계 사용자에게 high-performance, availability를 유지하는 애플리케이션을 배포할 수 있는 방법으로 [AWS Global Accelerator](https://aws.amazon.com/ko/global-accelerator/)가 있음.
    
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

## Amazon Neptune

* 복잡한 쿼리를 처리하려고 할 때 가장 적합한 AWS 데이터베이스 서비스.
    > * [Amazon Neptune](https://aws.amazon.com/ko/neptune/)은 빠르고 안정적이며 완벽하게 관리되는 그래프 데이터베이스 서비스.
    > * 수 많은 관계를 저장하고, 밀리초의 지연시간으로 그래프를 쿼리하는 데 최적화된 특수 목적의 고성능 그래프 데이터베이스 엔진.
    > * 읽기 전용 복제본, 특정 시점으로 복구, Amazon S3에 대한 지속적인 백업, 가용 영역 간 복제 기능을 갖춘 고가용성을 제공.
    > * 처리량이 높은 대화형 그래프 쿼리를 지원하여 소셜 네트워킹 애플리케이션을 구축할 수 있음.