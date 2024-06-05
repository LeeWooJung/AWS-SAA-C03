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

* Amazon EC2 인스턴스가 Amazon S3, Amazon DynamoDB에 액세스해야 할 때 가장 안전한 옵션인 솔루션
    > * [적절한 IAM 역할을 연결](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html).
    > * IAM 역할을 사용하여 Amazon EC2 인스턴스에서 실행되는 애플리케이션에 대한 임시 자격 증명을 관리.

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

## AWS ElastiCache

* SQL 쿼리 결과에 대해 캐싱을 지원하는 고가용성 **HIPAA** 규격 인메모리 데이터 베이스에서 참조 데이터를 처리할 때 사용할 수 있는 것.
    > * **Redis**는 밀리초 미만의 지연 시간을 제공하는 매우 빠른 인 메모리 데이터 스토어.
    > * **Redis**는 캐싱, 채팅/메시지, 게임 순위표, 지리 공간, 기계학습, 미디어 스트리밍, 대기열, 실시간 분석, 세션 스토어 등 실시간 트랜잭션 및 분석 처리 사용 사례에 탁월한 선택.
    > * **Redis**는 즉시 복제, 고가용성 및 클러스터 샤딩을 지원.

    > * **Memcached**는 캐시 또는 데이터 저장소로 사용할 수 있는 Memcached 호환 인 메모리 키-값 저장소 서비스.
    > **Memcached**는 액세스 지연 시간을 줄이고, 처리량을 늘리며, 관계형 또는 NoSQL 데이터베이스의 로드를 완화하기 위해 인 메모리 캐시를 구현하는데 탁월.

## Amazon GuardDuty

* [Amazon GuardDuty](https://aws.amazon.com/ko/guardduty/)에서 지원하는 데이터 소스로 식별할 수 있는 것.
    > * Amazon GuardDuty: AWS 계정, 워크로드, Amazon S3에 저장된 데이터를 보호하는 위협 탐지 서비스.
    > * 지속적인 위협 탐지를 위한 지능적이고 비용 효율적인 옵션을 제공.
    > AWS CloudTrail 이벤트, Amazon VPC 흐름 로그, DNS 로그와 같은 여러 AWS 데이터 소스에서 이벤트를 분석.

## Elastic Load Balancer

* Elastic Load Balancer가 target group의 Amazon EC2 인스턴스를 비정상적으로 표시했는데, 해당 인스턴스에 정상 접속 가능할 때 추측할 수 있는 이유.
    > * [Security Group이 Load Balancer에서 오는 트래픽을 허용](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-update-security-groups.html)하지 않는 경우.
    > * [Health Check 경로](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/target-group-health-checks.html)가 잘못 구성된 경우.

## Amazon Cognito

* Amazon API Gateway 내에서 API 호출을 승인하기 위해 인증/권한 메커니즘을 사용하기에 적합한 솔루션.
    > * Amazon Cognito User Pool: Amazon Cognito의 사용자 디렉터리.
    > * 사용자 관리 기능이 있으며 외부 자격 증명 공급자와 통합 가능.
    > * 제공 서비스: 가입 및 로그인, 사용자 로그인을 위한 내장형 맞춤형 웹 UI, 외부 자격증명 공급자와의 통합, 사용자 디렉터리 관리 및 사용자 프로필, MFA 등.