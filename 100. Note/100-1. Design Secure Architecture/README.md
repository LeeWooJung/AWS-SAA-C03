# Design Secure Architecture

## IAM

* Amazon DynamoDB에서 Production 환경에서 몇 개의 테이블을 실수로 지웠을 때 해결하는 방법.  
    > [IAM Permission Boundary](https://aws.amazon.com/ko/blogs/security/delegate-permission-management-to-developers-using-iam-permissions-boundaries/) 설정.  
    > [IAM Permission Boundaries 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/2.%20Identity/2-1.%20Identity%20and%20Access%20Management%20(IAM)/2-1-1.%20IAM%20Permission%20Boundaries)

* 다른 계정의 Amazon S3에 액세스 하는 Lambda 함수를 구현하는 방법.
    > * [IAM 역할](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/2.%20Identity/2-1.%20Identity%20and%20Access%20Management%20(IAM)#-iam-role)을 생성하여 Lambda 함수에 Amazon S3 버킷에 대한 액세스 권한을 부여.
    > * Amazon S3 버킷 또한, Lambda 함수의 액세스를 허용하는지 확인해야 함.

* AWS 계정에서 관리되는 production 환경의 일부 리소스에 액세스할 수 있도록 개발 환경의 사용자 집합에게 액세스 권한을 위임하는 방법.
    > * 새로운 [IAM 역할](https://aws.amazon.com/ko/iam/features/manage-roles/)을 생성하여 production 환경의 리소스에 액세스할 수 있는 권한 부여.
    > * IAM 역할을 사용하면 일반적으로 조직의 AWS 리소스에 액세스 할 수 없는 사용자 또는 서비스에 액세스 권한을 위임할 수 있음.

* Amazon EC2 인스턴스가 Amazon S3, Amazon DynamoDB에 액세스해야 할 때 가장 안전한 옵션인 솔루션
    > * [적절한 IAM 역할을 연결](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html).
    > * IAM 역할을 사용하여 Amazon EC2 인스턴스에서 실행되는 애플리케이션에 대한 임시 자격 증명을 관리.

## Lambda

* **최소 권한 원칙**을 사용하여 AWS Lambda 함수를 실행하는 데 사용할 권한을 구성해야 함. Amazon EventBridge 규칙이 함수를 호출할 때의 방법.
    > * lambda:InvokeFunction을 action으로, Service: events.amazonaws.com을 principal로 사용하여 리소스 기반 정책을 함수에 추가함. [링크](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-use-resource-based.html#eb-lambda-permissions)
    > * 최소 권한 원칙을 따르면, [Lambda](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-4.%20Serverless/3-4-1.%20AWS%20Lambda) 함수는 해당 함수가 수행해야 하는 작업을 실행하는 데 필요한 **최소한의 권한**만을 가져야 함.
    > * 따라서 Event Bridge와의 관계만 추가해주어야 함.
    > * **최소 권한 원칙**
    > * 시스템 보안의 중요한 개념 중 하나로, 사용자, 시스템, 프로세스 또는 애플리케이션에 특정 작업을 수행하기 위해 필요한 최소한의 권한만 부여하는 것을 의미.
    > * 이 원칙은 불필요한 권한 남용을 방지하고 보안을 강화하기 위한 것.


## VPC

* 온프레미스 데이터를 AWS 클라우드로 이동시킬 때 Amazon IPSec VPN Connection을 설정하기 위해 올바른 방법.  
    > * AWS Side: Virtual Private Gateway(VGW)
    > * On-premise Side: Customer Gateway  
    > * [Site-to-Site VPN](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/15.%20VPC/15-11.%20Site-to-Site%20VPN)
  
* 여러 VPC간의 연결을 위해 리소스 효율적이고, 확장 가능한 솔루션.
    > * [AWS transit gateway](https://docs.aws.amazon.com/vpc/latest/tgw/what-is-transit-gateway.html): VPC와 on-premise network를 연결해주는 hub역할.  
    > * [AWS Transit Gateway 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/15.%20VPC/15-12.%20Transit%20Gateway)


* Public Subnet을 통해 Amazon SQS에 액세스 하도록 VPC 바인딩을 구성하는 방법.
    > * [VPC endpoint](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/15.%20VPC/15-8.%20VPC%20Endpoints)를 사용하여 Amazon SQS에 접근할 수 있음.
    > * [Amazon SQS용 VPC endpoint](https://aws.amazon.com/ko/about-aws/whats-new/2018/12/amazon-sqs-vpc-endpoints-aws-privatelink/)를 사용하면 AWS 서비스에 비공개로 연결 할 수 있고, 이는 가용성과 확장성이 뛰어난 [AWS PrivateLink](https://aws.amazon.com/ko/privatelink/)를 기반으로 함.

* AWS Direct Connect 연결을 사용하는 곳과 AWS Site-to-Site VPN이 여러 개 있는 곳 간의 보안 통신을 제공할 수 있는 방법.
    > * [AWS VPN CloudHub](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPN_CloudHub.html) 는 VPC 유무에 관계 없이 사용할 수 있는 간단한 hub-and-spoke model에서 작동.
    > * Multiple branch 오피스와 원격 사무실간의 연결을 위한 저렴한 옵션을 구현함.  
    > [AWS VPN CloudHub 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/15.%20VPC/15-11.%20Site-to-Site%20VPN/15-10-1.%20VPN%20CloudHub)

* 공유 및 중앙 관리형 VPC를 AWS Organization에 제공하기 위한 방법.
    > * VPC Sharing을 사용하여 AWS Organization의 동일한 상위 조직에 속한 다른 AWS 계정과 하나 이상의 서브넷을 공유.
    > * VPC Sharing(Resource Access Manager의 일부): Amazon EC2 인스턴스, Amazon RDS 데이터베이스, Amazon Redshift 클러스터, AWS Lambda 함수와 같은 리소스를 여러 AWS 계정에서 공유되고 중앙에서 관리되는 VPC로 생성할 수 있음.
    > * AWS Organization과 동일한 조직에 속한 다른 계정과 하나 이상의 서브넷을 공유해야 함.

* Amazon EC2 인스턴스를 private subnet에 배포 후, 일부 AWS 서비스에 안전하게 액세스할 수 있도록 VPC 엔드포인트를 사용할 때, **게이트웨이 엔드포인트**를 지원하는 AWS 서비스.
    > * **[Amazon S3, Amazon DynamoDB](https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html)**
    > * (나머지 서비스는 인터페이스 엔드포인트 사용)
    > * [VPC Endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/concepts.html)를 사용하면 인터넷 게이트웨이, NAT 디바이스, VPN 연결 또는 AWS Direct Connect 연결 없이 VPC를 지원하는 AWS 서비스 및 AWS PrivateLink에서 제공하는 VPC 엔드포인트 서비스에 비공개로 연결 가능.
    > * VPC 엔드포인트는 가상장치로, 수평적으로 확장되고 중복되며 가용성이 높은 VPC의 구성 요소.
    > * [VPC 엔드포인트](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/15.%20VPC/15-8.%20VPC%20Endpoints)는 **인터페이스 엔드포인트**, **게이트웨이 엔드포인트** 두 가지 유형으로 구성.

* AWS로 마이그레이션 한 회사에서 VPC로 들어오고 나가는 트래픽을 보호하는 솔루션을 구현하기를 원함. 트래픽 흐름 검사 및 트래픽 필터링과 같은 특정 작업을 수행하기 위한 방법.
    > * [AWS Network Firewall](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/15.%20VPC/15-14.%20AWS%20Network%20Firewall)
    > * VPC를 위한 상태 저장 관리형 네트워크 방화벽 및 침입 탐지 및 방지 서비스.
    > * 네트워크 트래픽을 검사하고 필터링할 수 있는 고급 보안 기능을 제공.
    > * AWS 관리형 서비스로, 사용자 정의 규칙을 쉽게 설정하고 관리할 수 있어 운영 오버헤드를 줄임.
    > * 트래픽 검토 및 필터링에 필요한 다양한 규칙을 설정하여 회사의 보안 요구사항을 충족할 수 있음.
    > 인터넷 게이트웨이, NAT 게이트웨이 또는 VPN 또는 AWS Direct Connect를 통해 들어오고 나가는 트래픽 필터링 포함.

* 퍼블릭 서브넷에서 호스팅되는 EC2 인스턴스의 애플리케이션은 Amazon S3에 저장된 데이터를 처리함. EC2 인스턴스는 인터넷을 통해 Amazon S3에 액세스하지만 다른 네트워크 액세스는 필요하지 않아 인터넷을 통해 전송되지 않고 개인 경로를 사용하는 방법.
    > * EC2 인스턴스를 프라이빗 서브넷으로 이동함.
    > * Amazon S3용 **VPC Endpoint**를 생성하고, 엔드포인트를 프라이빗 서브넷의 라우팅 테이블에 연결.
    > * VPC 엔드포인트는 Amazon S3와 같은 AWS 서비스에 인터넷을 거치지 않고 프라이빗 네트워크를 통해 접근할 수 있게 해줌.
    > * 이를 이용하면 인터넷을 이용하는 것보다 데이터 전송 비용이 절감될 수 있음.

* 외부 공급자의 서비스에 연결해야 하는데, 해당 서비스는 공급자의 VPC에서 호스팅 됨. AWS에서 실행되는 워크로드는 해당 공급자 서비스에 비공개로 연결해야 하며, 해당 서비스로만 연결을 제한하고 회사의 VPC에서만 시작되어야 함. 이 때 이를 해결할 방법.
    > * 공급자에게 대상 서비스에 대한 **VPC 엔드포인트**를 생성하도록 요청하고, AWS **PrivateLink**를 사용하여 대상 서비스에 연결.
    > * **AWS PrivateLink**는 비공개 연결을 제공하여 인터넷을 통하지 않고 안전하게 VPC 간 트래픽을 전달함.
    > * **VPC Endpoint**는 특정 서비스에 대한 접근을 제한할 수 있음.
    > * CF. **Virtual Private Gateway**
    > * 비공개 연결 제공 불가: VGW는 VPC 간의 VPN 연결을 설정하는 데 사용되며, 이는 인터넷을 통하므로 완전히 비공개로 연결을 유지할 수 없음.
    > * 특정 서비스로의 트래픽 제한이 어려움.

## AWS Configuration

* EC2 인스턴스에 애플리케이션 배포 후, ACM이 만료되기 전에 보안 팀에게 알리는 솔루션을 구축하기 위한 방법.
    > * [AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/how-does-config-work.html)를 사용하여 SSL/TLS certificates가 만료되기 30일 이내인지 확인.
    > * 그 후, SNS notification을 통해 알림.  
    > * [AWS Config 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/13.%20Monitoring%2C%20Audit%20%26%20Performance/13-4.%20AWS%20Config)

* AWS 클라우드 배포를 검토하여 Amazon S3 버킷에 무단 **구성 변경**이 없는지 확인하기 위한 방법.
    > * AWS Config
    > * 적절한 규칙으로 AWS Config를 킴.
    > * AWS Config를 키면 먼저 계정에 있는 지원되는 AWS 리소스를 찾고, 각 리소스에 대한 구성 항목을 생성함.
    > * AWS Config는 리소스의 구성이 변경되면 구성 항목을 생성하고, 구성 레코더를 시작할 때부터 리소스의 구성 항목에 대한 기록 내역을 유지.
    > * AWS Config는 S3 버킷의 구성 변경 사항을 지속적으로 모니터링할 수 있음. 특히, 버킷 정책, 액세스 제어 목록(ACL), 암호화 설정 등과 같은 중요한 구성 요소에 대한 변경을 감지할 수 있음.
    > * 자동화된 방식으로 감사 및 준수 체크를 수행하여 운영 오버헤드를 최소화하면서 시스템 보안을 강화할 수 있음.

* AWS ACM으로 가져온 인증서를 사용하도록 Elastic Load Balancer를 구성하고, 각 인증서가 만료되기 30일 전에 회사 보안팀에게 알리기 위한 방법.
    > * **AWS Config**를 사용하여 30일 이내에 만료된 인증서를 확인하도록 규칙을 생성.
    > * AWS Config의 비준수 리소스 보고를 **Amazon SNS**를 통해 사용자 지정 알림을 호출하도록 **Amazon EventBridge**를 구성.
    > * **[ACM](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/14.%20AWS%20Security%20%26%20Encryption/14-4.%20AWS%20Certificate%20Manager)은 가져온 인증서에 대한 관리형 갱신을 제공하지 않음**.
    > * **AWS Config**
    > * AWS 리소스의 구성을 지속적으로 모니터링하고 평가할 수 있는 서비스.
    > * 인증서가 만료되기 30일 전을 체크하는 규칙을 설정하여, 특정 조건을 만족하지 않는 리소스를 자동으로 탐지하고 알림을 보낼 수 있음.
    > * AWS Config는 Amazon EventBridge와 통합되어 규칙 위반 이벤트가 발생했을 때 자동으로 이벤트 생성 가능.

## AWS S3

* Amazon S3에 교차 계정 액세스 요청이 증가할 때, Amazon S3 버킷에 저장된 데이터에 대해 사용자 수준 및 계정 수준 액세스 권한을 제공하는 방법.
    > * [Amazon S3 Bucket Policies](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3/6-3-3.%20Security#%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%95%A1%EC%84%B8%EC%8A%A4-%EC%A0%9C%EC%96%B4)를 사용하여 단일 버킷 내의 객체 중 일부 또는 전체에 대한 권한을 추가하거나 거부할 수 있음.
    > * 해당 정책을 사용자, 그룹 또는 Amazon S3 버킷에 연결하여 권한을 중앙 집중식으로 관리할 수 있음.

* 애플리케이션을 **서버리스 솔루션**으로 이동하려 함. 데이터를 Amazon S3 버킷에 저장하는데, 데이터는 암호화가 필요며 다른 AWS 리전에 복제해야 함. 서버리스 솔루션은 SQL을 사용하여 기존 및 신규 데이터를 분석해야 함. **최소한의 운영 오버헤드**로 해결하는 방법.
    > * 기존 S3 버킷에 데이터를 로드함.
    > * **S3 교차 리전 복제**([CRR](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3/6-3-1.%20Bucket#%EB%B2%84%ED%82%B7%EC%9D%98-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-%EB%B0%8F-%EA%B8%B0%EB%8A%A5))를 사용하여 암호화된 객체를 다른 리전의 S3 버킷에 복제함.
    > * SSE-S3로 서버측 암호화를 사용함.
    > * [Amazon Athena](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-10.%20Amazon%20Athena)를 사용하여 데이터를 쿼리함.
    > * 이미 존재하는 S3 버킷을 사용하는 것은 새로운 버킷을 생성하고 설정(정책, 권한, 복제 설정 등)하는 오버헤드를 감소시킴.
    > * [SS3-S3](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3/6-3-3.%20Security#%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%95%94%ED%98%B8%ED%99%94)는 Amazon S3가 자동으로 관리하는 암호화 키를 사용하여 별도의 키 관리가 필요하지 않아 설정이 간단함.

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

* Amazon S3 버킷에 저장된 민감한 데이터를 식별하고, 악의적인 활동으로부터 Amazon S3에 저장된 모든 데이터를 모니터링하고 보호하는 방법.
    > * [Amazon GuardDuty](https://aws.amazon.com/ko/guardduty/)를 사용하여 S3에 저장된 데이터에 대한 악의적인 활동을 모니터링 할 수 있음.
    > * [Amazon Machie](https://aws.amazon.com/ko/macie/)를 사용하여 Amazon S3에 저장된 민감한 데이터를 식별할 수 있음.
    > * Amazon Machie는 S3에서 중요한 데이터를 검색하고 보호하는 완전 관리형 데이터 보안 및 데이터 개인 정보 보호 서비스.

## Elastic Load Balancer

* Elastic Load Balancer가 target group의 Amazon EC2 인스턴스를 비정상적으로 표시했는데, 해당 인스턴스에 정상 접속 가능할 때 추측할 수 있는 이유.
    > * [Security Group이 Load Balancer에서 오는 트래픽을 허용](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-update-security-groups.html)하지 않는 경우.
    > * [Health Check 경로](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/target-group-health-checks.html)가 잘못 구성된 경우.

* AWS에 배호된 3게층 웹 애플리케이션이 있는데 웹 서버는 VPC의 퍼블릭 서브넷, 애플리케이션 서버/데이터베이스는 VPC의 프라이빗 서브넷에 배포됨. AWS Marketplace의 타사 가상 방화벽 어플라이언스를 검사 VPC에 배포했을 때 트래픽이 웹 서버에 도달하기 전에 애플리케이션에 대한 모든 트래픽을 검사하기 위해 웹 애플리케이션을 어플라이언스와 통합하기 위해 최소한의 운영 오버헤드를 충족하는 방법.
    > * [Gateway Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-4.%20Gateway%20Load%20Balancer)
    > * 검사 VPC에 Gateway Load Balancer를 배포. 게이트웨이 로드 밸런서 엔드포인트를 생성하여 수신 패킷을 수신하고, 패킷을 어플라이언스로 전달.
    > * IP 패킷을 수락: Layer 3을 뜻함.
    > * 트래픽을 가상 방화벽 장치로 쉽게 라우팅할 수 있도록 도와줌. 복잡한 설정 없이도 트래픽 검사가 가능.
    > * Gateway Load Balancer를 사용하면 방화벽, 침입 탐지 및 방지 시스템, 심층 패킷 검사 시스템과 같은 가상 어플라이언스를 배포, 확장 및 관리할 수 있음.
    > * Gateway Load Balancer는 OSI 세 번째 계층인 네트워크 계층에서 작동.

## Amazon Cognito

* Amazon API Gateway 내에서 API 호출을 승인하기 위해 인증/권한 메커니즘을 사용하기에 적합한 솔루션.
    > * Amazon Cognito User Pool: Amazon Cognito의 사용자 디렉터리.
    > * 사용자 관리 기능이 있으며 외부 자격 증명 공급자와 통합 가능.
    > * 제공 서비스: 가입 및 로그인, 사용자 로그인을 위한 내장형 맞춤형 웹 UI, 외부 자격증명 공급자와의 통합, 사용자 디렉터리 관리 및 사용자 프로필, MFA 등.

## Amazon EBS

* [**암호화된** Amazon EBS 볼륨](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-encryption.html)의 올바른 기능.
    > * 볼륨 내부에 저장된 데이터는 암호화 됨.
    > * 볼륨에서 생성된 모든 스냅샷은 암호화 됨. 또한 해당 스냅샷에서 생성된 볼륨이 모두 암호화 됨.
    > * 볼륨과 인스턴스 사이를 이동하는 데이터는 암호화 됨.
    > * 암호화된 볼륨과 스냅샷을 생성할 때 AWS Key Management Service(AWS KMS) 고객 마스터 키(CMK)를 사용.

## Amazon RDS

* Amazon EC2 기반 웹 서버에 애플리케이션을 배포하고, Amazon RDS PostgreSQL 데이터베이스를 저장소로 활용함. 이 때, PostgreSQL DB는 EC2 인스턴스의 인바운드 트래픽을 허용하는 프라이빗 서브넷에 설정되며 데이터 암호화를 위해 AWS KMS를 사용. 이 때, 데이터베이스에 대한 보안 액세스를 촉진하기 위한 방법.
    > * [Amazon RDS에서 전송 중인 데이터에 SSL을 사용하도록 구성](https://aws.amazon.com/ko/rds/features/security/).
    > * SSL/TLS 연결을 사용하여 전송 중인 데이터를 암호화할 수 있음.

* 암호화되지 않은 RDS DB 인스턴스를 사용 중인데, 이제 데이터베이스와 스냅샷이 앞으로 항상 암호화되도록 하는 방법.
    > * 최신 DB **스냅샷 사본을 암호화**.
    > * 암호화된 스냅샷을 복원하여 **기존 DB 인스턴스를 교체**.
    > * 최신 스냅샷을 암호화하면, 가장 최근의 데이터 상태를 반영 및 암호화할 수 있음.
    > * 암호화된 스냅샷을 사용하여 RDS 인스턴스를 생성하면, 해당 RDS는 암호화된 데이터베이스가 됨.
    > * 기존에 암호화 설정이 되지 않은 RDS는 **암호화 되도록 변환할 수 없음**.
    > * **무조건** 새로운 RDS 인스턴스를 생성해야 하며, 기존 인스턴스를 **복원 하더라도 암호화되지 않음**.

## AWS Secret Manager

* Amazon EC2 인스턴스에서 실행되고 있는 Amazon Aurora DB가 있는데, EC2 인스턴스는 파일에 로컬로 저장된 사용자 이름과 암호를 사용하여 DB에 연결함. 이 때 자격 증명 관리의 운영 오버헤드를 최소화 하기 위한 방법.
    > * AWS Secret Manager
    > * 자격 증명을 안전하게 저장하고 관리할 수 있으며, 수동으로 비밀번호를 관리할 필요성을 제거.
    > * 애플리케이션, 서비스 및 IT 리소스에 대한 액세스를 보호하는 데 도움이 되는 보안 정보 관리 서비스. 수명 주기 동안 데이터베이스 자격 증명, API 키 및 기타 보안 정보를 손쉽게 교체, 관리 및 검색 가능.

## Amazon QuickSight

* AWS에서 데이터 레이크를 호스팅하는데, 데이터 시각화를 제공하고 데이터 레이크 내의 모든 데이터 소스를 포함하는 보고 솔루션이 필요. 회사의 관리 팀만 모든 시각화에 대한 전체 액세스 권한을 가져야 하고, 나머지는 제한된 액세스 권한만 가져야할 때 이를 충족하는 방법.
    > * Amazon QuickSight
    > * 다양한 데이터 소스를 연결하여 단일 대시보드에서 시각화할 수 있는 기능을 제공.
    > * 사용자 및 그룹별로 대시보드 접근 권한을 설정할 수 있어 접근 수준을 효과적으로 제어 가능.
    > * **IAM**을 사용하는 것보다 QuickSight의 접근 권한제어 기능을 사용하는 것이 효율적.
    > 세션별 지불 결제 모델을 사용하여 사용량에 대해서만 요금을 지불하면 됨.

## Amazon CloudWatch

* CloudWatch 대시보드에 애플리케이션 지표를 표시하는데, 제품 관리자는 이 대시보드에 주기적으로 액세스하지만, AWS 계정이 없음. **최소 권한 원칙**에 따라 제품 관리자에게 액세스를 제공하기 위한 방법.
    > * CloudWatch 콘솔에서 대시보드를 공유. 제품 관리자의 이메일 주소를 입력하고 공유 링크를 제품 관리자에게 제공.
    > * CloudWatch 콘솔에서 대시보드를 공유할 때, 특장 사용자의 이메일 주소만 입력하면 해당 사용자에게만 접근 권한을 부여할 수 있음(최소한의 권한 원칙을 준수).
    > * IAM 사용자나 그룹을 생성하지 않고도 콘솔에서 간편하게 대시보드를 공유하고 관리할 수 있어 운영 효율이 좋음.

## AWS Single Sign-On(SSO)

* 회사의 모든 게정에 SSO 솔루션이 필요하고, 사내 자체 관리 Microsoft Active Directory에서 사용자 및 그룹을 계속 관리하는데, 애플리케이션을 AWS로 마이그레이션 중일 때 위 조건을 충족시키는 방법.
    > * AWS SSO 콘솔에서 **AWS SSO**를 활성화하고, **단방향 포레스트 트러스트** 또는 **단방향 도메인 트러스트**를 생성하여 Microsoft Active Directory용 AWS Directory Service를 사용하여 회사 자체 관리형 MAD를 AWS SSO와 연결.
    > * AWS SSO를 사용하여 모든 회사 계정에 대한 단일 로그인(SSO) 솔루션을 구현하여 보안 강화 가능. 
    > * AWS Single Sign-On = AWS IAM Identity Center
    > * 온프레미스에서 관리되는 Microsoft Active Directory와 AWS SSO 간의 통합을 통해 기존의 사용자 및 그룹 관리 체계를 유지할 수 있음.

## AWS Systems Manager

* 1000개의 EC2 Linux 인스턴스에서 실행되는 워크로드가 있는데, 이는 타사 소프트웨어에 의해 구동됨. 회사는 중요한 보안 취약성을 수정하기 위해 가능한 한 빨리 모든 EC2 인스턴스에서 타사 소프트웨어 패치를 원할 때 방법.
    > * **AWS Systems Manager Run Command**를 사용하여 모든 EC2 인스턴스에 패치를 적용하는 사용자 지정 명령을 실행.
    > * 대규모 인프라에서 매우 빠르고 효율적으로 특정 스크립트나 명령을 실행할 수 있는 기능 제공.
    > * 수천 대의 EC2 인스턴스에 대해 동시에 명령을 실행할 수 있어 패치를 빠르게 적용 가능.
    > * 제 3자 소프트웨어 패치는 일반적으로 **AWS Systems Manager Pacth Manager**의 기본 기능에 포함되지 않음. Patch Manager는 주로 운영체제 패치를 위해 설계 되었음.

## API Gateway

* Amazon Route 53에 도메인 이름을 등록하고, 한 Region에 Amazon API Gateway를 백엔드 마이크로서비스 API의 공용 인터페이스로 사용중임. 타사 서비스에서 API를 안전하게 이용하고, HTTPS를 사용할 수 있도록 회사의 도메인 이름 및 해당 인증서로  API 게이트웨이 URL을 설계하기 위한 방법.
    > * Region API 게이트웨이 엔드포인트를 생성.
    > * API Gateway 엔드포인트를 회사의 도메인 이름과 연결. 도메인 이름과 연결된 공인 인증서를 **동일한 리전**의 AWS Certificate Manger(ACM)로 가져옴.
    > * API Gateway 엔드포인트에 인증서 연결.
    > * API Gateway 엔드포인트로 트래픽을 라우팅하도록 Route 53을 구성.
    > * **지역 일관성**: 인증서를 API Gateway가 위치한 동일한 지역에 가져와야 함. API Gateway와 ACM간의 통합이 원활하게 해줌.
    > * **보안 HTTPS**: API Gateway 엔드포인트에 회사의 도메인 이름과 관련된 인증서를 연결하여 HTTPS를 통한 보안 보장.

## NAT Gateway

* VPC에 퍼블릭 및 프라이빗 서브넷이 존재. 고가용성을 위해 세 개의 가용 영역(AZ) 각각에 하나의 퍼블릭 서브넷과 하나의 프라이빗 서브넷이 존재. **인터넷 게이트웨이**는 퍼블릭 서브넷에 대한 인터넷 액세스를 제공하는데 사용. 프라이빗 서브넷은 인터넷에 액세스할 수 있어야 할 때의 방법.
    > * 각 AZ의 각 **퍼블릭 서브넷**에 대해 하나씩 3개의 **NAT 게이트웨이**생성.
    > * 비 VPC 트래픽을 해당 AZ의 NAT 게이트웨이로 전달하는 각 AZ에 대한 **프라이빗 라우팅 테이블**생성.
    > * **NAT Gateway**는 각 가용 영역에 하나씩 배치되어, 특정 AZ에 문제가 발생하더라도 다른 AZ의 NAT Gateway가 대체할 수 있어 고가용성 제공.
    > * **NAT Gateway**는 프라이빗 서브넷 인스턴스가 인터넷에 접근할 수 있도록 하면서도, 외부로부터의 직접적인 접근을 막음.
    > * **Internet Gateway**
    > * IGW는 VPC가 인터넷과 통신할 수 있도록 하는 게이트웨이. VPC 내의 **퍼블릭 서브넷** 인스턴스가 인터넷에 접근할 수 있도록 함.
    > * **IGW는 VPC에 연결**되며, **퍼블릭 서브넷의 라우팅 테이블**에 설정되어야 함.
    > * **NAT Gateway**
    > * NAT 게이트웨이는 프라이빗 서브넷 내의 인스턴스가 인터넷에 접근할 수 있도록 하면서, 외부에서 프라이빗 서브넷 인스턴스로의 직접적인 접속을 차단.
    > * NAT 게이트웨이는 **퍼블릭 서브넷**에 배치되며, **프라이빗 서브넷의 라우팅 테이블**에 설정되어야함.

## Amazon Rekognition

* 소셜 미디어 웹사이트를 운영 중이며, 웹사이트는 사용자가 이미지를 업로드하여 다른 사용자와 공유할 수 있는 기능을 제공함. 이 때 부적절한 콘텐츠가 포함되었는지 확인하는데 개발 노력을 최소화 하는 방법.
    > * **Amazon Rekognition**을 사용하여 부적절한 콘텐츠를 감지하고, 신뢰도가 낮은 예측에는 인적 검토를 사용.
    > * **Amazon Rekognition**
    > * 이미지를 자동으로 분석하고 부적절한 콘텐츠를 감지할 수 있음.
    > * 사용자 경험을 보호하고, 플랫폼의 안정성을 높일 수 있음.

## AWS Certificate Manager(ACM)

* AWS 에서 웹 애플리케이션을 배포하는데, 해당 애플리케이션은 외부 CA(인증기관)에서 발급한 SSL/TLS를 사용함. 애플리케이션은 ALB 뒤에서 실행하고, 매년 인증서를 갱신해야할 때 사용할 수 있는 방법.
    > * **AWS ACM**을 사용하여 SSL/TLS 인증서를 가져옴.
    > * 인증서를 ALB에 적용하고, Amazon Event Bridge(Amazon CloudWatch Events)를 사용하여 인증서가 만료될 때 알림을 보내 수동으로 교체.
    > * **ACM**: Amazon Web Services 서비스 및 내부 연결된 리소스에 사용할 공개 SSL/TLS 인증서를 쉽게 프로비저닝, 관리 및 배포할 수 있는 서비스.
    > * ACM은 외부 CA에서 발급받은 SSL/TLS 인증서를 **자동으로 갱신하는 기능이 없음**.
    > * ACM에서 자동 갱신이 가능한 인증서는 AWS 자체에서 발급한 인증서에 한함.

## Amazon Textract

* 병원에서 Amazon API Gateway 및 AWS Lambda와 함께 RESTful API를 배포함. API는 PDF 형식 및 JPEG 형식의 보고서를 업로드하는데, 특정 정보를 식별하기 위해 Lambda 코드를 수정해야 함. 최소한의 운영 오버헤드로 해결하는 방법.
    > * **Amazon Textract**를 사용하여 보고서에서 텍스트를 추출.
    > * **Amazon Comprehend Medical**을 사용하여 추출된 텍스트에서 특정 정보를 식별.
    > * **Amzaon Textract**
    > * 스캔한 문서에서 텍스트와 데이터, 표 및 양식을 자동으로 추출하는 AWS 서비스.
    > * 머신 러닝을 사용하여 텍스트인식, 문서 구조 이해 등을 제공.
    > * HIPAA 규정 준수가 필요한 의료 및 생명 과학 워크로드에 적합.
    > * **Amazon Comprehend Medical**
    > * 의료 텍스트에서 유의미한 정보를 추출하는 데 특화된 자연어 처리 서비스.
    > * 의학적 문서에서 환자의 상태, 투약, 검사 결과 등 다양한 의료 정보를 인식하고 추출 가능.

## Security Group

* 프라이빗 서브넷의 Amazon EC2에서 Linux 기반 애플리케이션 인스턴스를 시작함. VPC의 퍼블릭 서브넷에서는 Linux 기반 **Bastion Host**를 시작함. 이 때, 사내 네트워크에서 회사의 인터넷 연결을 통해 배스천 호스트 및 애플리케이션 서버에 연결해야 함. 모든 EC2 인스턴스의 보안 그룹이 해당 액세스를 허용하는지 확인하는 방법.
* [Public Internet] -> [Bastion Host/Public Subnet] -> [EC2 Instance/Private Subnet]
    > * 배스천 호스트의 현재 보안 그룹을 회사의 외부 IP 범위에서만 인바운드 액세스를 허용하는 보안그룹으로 교체.
    > * 애플리케이션 인스턴스의 현재 보안 그룹을 배스천 호스트의 개인 IP 주소에서만 인바운드 SSH 액세스를 허용하는 보안 그룹으로 교체.
    > * **Bastion Host**
    > * 출입 차단 소프트웨어가 설치되어 내부와 외부 네트워크 사이에서 일종의 게이트 역할을 수행하는 호스트.
    > * 주로 보안이 중요한 네트워크 환경에서 외부의 관리자가 내부 시스템에 접근할 때 사용됨.
    > * 내부 내트워크로의 모든 접속 시도를 기록하고 모니터링할 수 있음.
    > * 외부 IP만 Bastion Host를 통과할 수 있도록 하여 외부 공격에 대한 방어 제공.
    > * 내부 인스턴스에 대한 모든 접근은 Bastion Host를 통해서만 이뤄지므로 보안 관리를 단순화하고 접근 제어를 업격하게 할 수 있음.

* 퍼블릭 서브넷에서 Amazon EC2 인스턴스로 애플리케이션을 호스팅하고, 프라이빗 서브넷에서 Microsoft SQL Server로 구성된 데이터베이스 계층을 구성함. 보안이 최우선일 때, 보안 그룹을 구성하는 방법.
    > * **웹 계층**에서는 0.0.0.0/0에서 **포트 443**의 인바운드 트래픽을 허용.
    > * HTTPS 트래픽을 처리하기 위해 포트 443을 사용.
    > * **데이터베이스 계층**에서는 웹 계층에 대한 보안 그룹에서 **포트 1433**의 인바운드 트래픽을 허용.
    > * Microsoft SQL Server는 기본적으로 포트 1433을 통해 통신함.
    > * **MS SQL**: 포트 1433
    > * **MySQL, Aurora**: 포트 3306
    > * **Redshift**: 포트 5439
    > * **PostgreSQL**: 포트 5432
    > * **Oracle**: 포트 1521

## AWS Shield

* Amazon EC2 인스턴스에서 실행되는 웹 서버를 위한 고가용성 인프라를 설계하고, 대규모 DDoS 공격을 완화할 수 있는 솔루션을 구축하는 방법.
    > * **AWS Shield Advanced**를 사용하여 DDoS 공격을 차단.
    > * 정적 및 동적 콘텐츠 모두에 **Amazon CloudFront**를 사용하도록 웹사이트를 구성.
    > * **AWS Shield Advanced**
    > * DDoS 공격을 실시간으로 모니터링하고, 공격 트래픽을 자동으로 탐지하고 완화함.
    > * 대규모 DDoS 공격으로부터 애플리케이션을 보호할 수 있는 고급 방어 메커니즘을 제공.
    > * DDoS Response Team(DRT)의 지원을 받아, 공격 발생 시 빠르게 대응하고 복구할 수 있음.
    > * **AWS CloudFront**
    > * 전 세계에 분산된 엣지 로케이션을 통해 콘텐츠를 캐싱하고 제공하여, 트래픽 부하을 분산시키고 웹 서버의 부담을 줄임(고가용성).
    > * 자체적으로 DDoS 공격에 대한 방어 메커니즘을 제공하며, 트래픽을 분산시켜 공격의 영향을 최소화 함.

## AWS CloudFront

* Amazon CloudFront 배포를 통해 Amazon S3 버킷을 스토리지로 하는 파일을 제공하려 함. 이 때, S3 URL에 대한 직접 탐색을 통해 파일에 액세스하는 것을 원하지 않을 때의 방법.
    > * **원본 액세스 ID**(Origin Access Identity)를 생성하고, CloudFront 배포에 OAI를 할당.
    > * OAI만 읽기 권한을 갖도록 S3 버킷을 구성.
    > * OAI는 Amazon CloudFront가 S3 버킷과 안전하게 통합되도록 돕는 메커니즘임. 이를 통해 CloudFront가 S3 버킷의 콘텐츠에 대한 권한을 가지도록 할 수 있음.

## AWS Control Tower

* 온프레미스 데이터 센터를 AWS로 마이그레이션 하려고 함. 규정 준수 요구 사항에 따라 회사는 ap-northeast-3 지역만 사용할 수 있음. 회사 관리자는 VPC를 인터넷에 연결할 수 없음. 이를 충족하는 방법.
    > * **AWS Control Tower**를 사용하여 **데이터 상주 가드레일**을 구현하여 인터넷 액세스를 거부하고, ap-northeast-3를 제외한 모든 AWS 리전에 대한 액세스를 거부.
    > * **AWS Organization**을 사용하여 VPC가 인터넷에 액세스하지 못하도록 **서비스 제어 정책**(SCPS)를 구성. ap-northeast-3을 제외한 모든 AWS 리전에 대한 액세스를 거부.
    > * **AWS Control Tower**
    > * **데이터 레지던스 가드레일**: AWS Control Tower는 자동으로 여러 AWS 계정과 리소스에 보안 및 규정 준수 정책을 적용할 수 있는(AWS 환경의 지속적인 거버넌스를 위한) 데이터 레지던스 가드레일을 제공. 또한, 인터넷 액세스를 차단하는 정책을 쉽게 설정할 수 있음.
    > * **자동화된 설정**: 표준 보안 설정을 자동으로 적용하여 설정 시간을 단축하고 인적 오류를 줄임. 이로 인해 보안 및 규정 준수 요구 사항을 더 쉽게 충족할 수 있음.
    > * **종합적인 관리**: 계정 생성을 자동화하고, 여러 게정에 걸쳐 일관된 보안 정책을 적용할 수 있도록 도움. 이를 통해 중앙 집중식으로 보안 관리가 가능하며, 규정 준수 요구사항을 더 효과적으로 충족할 수 있음.
    > * 잘 설계된 새로운 다중 계정 환경을 쉽게 설정하고 보안, 운영 및 내부 규정 준수를 위한 규칙으로 AWS 워크로드를 관리할 수 있는 단일 위치 제공.
    > * 기준선을 설정하기 위한 **AWS CloudFormation**, 구성 변경을 방지하기 위한 **AWS Organizations 서비스 정책**(SCP), 부적합을 지속적으로 감지하기 위한 **AWS Config** 규칙과 같은 여러 빌딩 블록을 사용하여 가드레일을 자동으로 구현.
    > * **AWS Organizations SCP**
    > * SCP를 사용하여 계층별로 정책을 설정하고 적용할 수 있음. SCP를 통해 VPC가 인터넷에 접근하지 못하도록 제한할 수 있음.
    > * **Organization**를 사용하면 여러 계정을 중앙에서 관리할 수 있으며, **SCP**를 통해 모든 계정에 걸쳐 일관된 보안 정책을 적용할 수 있음. 이는 보안 정책의 일관성을 보장하고 관리의 복잡성을 줄임.