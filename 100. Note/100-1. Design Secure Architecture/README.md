# Design Secure Architecture

## IAM

* Amazon DynamoDB에서 Production 환경에서 몇 개의 테이블을 실수로 지웠을 때 해결하는 방법.  
    > [IAM Permission Boundary](https://aws.amazon.com/ko/blogs/security/delegate-permission-management-to-developers-using-iam-permissions-boundaries/) 설정.

* 다른 계정의 Amazon S3에 액세스 하는 Lambda 함수를 구현하는 방법.
    > * IAM 역할을 생성하여 Lambda 함수에 Amazon S3 버킷에 대한 액세스 권한을 부여.
    > * Amazon S3 버킷 또한, Lambda 함수의 액세스를 허용하는지 확인해야 함.

* AWS 계정에서 관리되는 production 환경의 일부 리소스에 액세스할 수 있도록 개발 환경의 사용자 집합에게 액세스 권한을 위임하는 방법.
    > * 새로운 [IAM 역할](https://aws.amazon.com/ko/iam/features/manage-roles/)을 생성하여 production 환경의 리소스에 액세스할 수 있는 권한 부여.
    > * IAM 역할을 사용하면 일반적으로 조직의 AWS 리소스에 액세스 할 수 없는 사용자 또는 서비스에 액세스 권한을 위임할 수 있음.

## VPC

* 온프레미스 데이터를 AWS 클라우드로 이동시킬 때 Amazon IPSec VPN Connection을 설정하기 위해 올바른 방법.  
    > * AWS Side: Virtual Private Gateway(VGW)
    > * On-premise Side: Customer Gateway
  
* 여러 VPC간의 연결을 위해 리소스 효율적이고, 확장 가능한 솔루션.
    > * [AWS transit gateway](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html): VPC와 on-premise network를 연결해주는 hub역할.

* Public Subnet을 통해 Amazon SQS에 액세스 하도록 VPC 바인딩을 구성하는 방법.
    > * VPC endpoint를 사용하여 Amazon SQS에 접근할 수 있음.
    > * [Amazon SQS용 VPC endpoint](https://aws.amazon.com/ko/about-aws/whats-new/2018/12/amazon-sqs-vpc-endpoints-aws-privatelink/)를 사용하면 AWS 서비스에 비공개로 연결 할 수 있고, 이는 가용성과 확장성이 뛰어난 [AWS PrivateLink](https://aws.amazon.com/ko/privatelink/)를 기반으로 함.

* AWS Direct Connect 연결을 사용하는 곳과 AWS Site-to-Site VPN이 여러 개 있는 곳 간의 보안 통신을 제공할 수 있는 방법.
    > * [AWS VPN CloudHub](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPN_CloudHub.html) 는 VPC 유무에 관계 없이 사용할 수 있는 간단한 hub-and-spoke model에서 작동.
    > * Multiple branch 오피스와 원격 사무실간의 연결을 위한 저렴한 옵션을 구현함.

* 공유 및 중앙 관리형 VPC를 AWS Organization에 제공하기 위한 방법.
    > * VPC Sharing을 사용하여 AWS Organization의 동일한 상위 조직에 속한 다른 AWS 계정과 하나 이상의 서브넷을 공유.
    > * VPC Sharing(Resource Access Manager의 일부): Amazon EC2 인스턴스, Amazon RDS 데이터베이스, Amazon Redshift 클러스터, AWS Lambda 함수와 같은 리소스를 여러 AWS 계정에서 공유되고 중앙에서 관리되는 VPC로 생성할 수 있음.
    > * AWS Organization과 동일한 조직에 속한 다른 계정과 하나 이상의 서브넷을 공유해야 함.

## AWS Configuration

* EC2 인스턴스에 애플리케이션 배포 후, ACM이 만료되기 전에 보안 팀에게 알리는 솔루션을 구축하기 위한 방법.
    > * [AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/how-does-config-work.html)를 사용하여 SSL/TLS certificates가 만료되기 30일 이내인지 확인.
    > * 그 후, SNS notification을 통해 알림.

## AWS S3

* Amazon S3에 교차 계정 액세스 요청이 증가할 때, Amazon S3 버킷에 저장된 데이터에 대해 사용자 수준 및 계정 수준 액세스 권한을 제공하는 방법.
    > * Amazon S3 Bucket Policies를 사용하여 단일 버킷 내의 객체 중 일부 또는 전체에 대한 권한을 추가하거나 거부할 수 있음.
    > * 해당 정책을 사용자, 그룹 또는 Amazon S3 버킷에 연결하여 권한을 중앙 집중식으로 관리할 수 있음.