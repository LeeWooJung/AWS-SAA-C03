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

## AWS Configuration

* EC2 인스턴스에 애플리케이션 배포 후, ACM이 만료되기 전에 보안 팀에게 알리는 솔루션을 구축하기 위한 방법.
    > * [AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/how-does-config-work.html)를 사용하여 SSL/TLS certificates가 만료되기 30일 이내인지 확인.
    > * 그 후, SNS notification을 통해 알림.

