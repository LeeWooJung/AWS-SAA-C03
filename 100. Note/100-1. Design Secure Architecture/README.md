# Design Secure Architecture

## IAM

* Amazon DynamoDB에서 Production 환경에서 몇 개의 테이블을 실수로 지웠을 때 해결하는 방법.  
    > [IAM Permission Boundary](https://aws.amazon.com/ko/blogs/security/delegate-permission-management-to-developers-using-iam-permissions-boundaries/) 설정.

## VPC

* 온프레미스 데이터를 AWS 클라우드로 이동시킬 때 Amazon IPSec VPN Connection을 설정하기 위해 올바른 방법.  
    > * AWS Side: Virtual Private Gateway(VGW)
    > * On-premise Side: Customer Gateway
  
* 여러 VPC간의 연결을 위해 리소스 효율적이고, 확장 가능한 솔루션.
    > * [AWS transit gateway](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html): VPC와 on-premise network를 연결해주는 hub역할.

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

