# [Gateway Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/gateway/introduction.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/1933ce66-05ec-41cc-bb09-13a7a7fadac3" width = "30" height = "30"> Gateway Load Balancer    

### 설명

AWS 게이트웨이 로드 밸런서(**GWLB**)는 AWS 환경에서 **VPC 엔드 포인트와 함께 사용**되어 타사 가상 어플라이언스를 배포, 확장 및 관리할 수 있는 관리형 서비스. 

## 특징

### 기능
- **네트워크 계층**(OSI 모델의 계층 3 - IP Packet)에서 작동.
- **모든 포트에서 모든 IP 패킷을 수신**하고 리스너 규칙에 따라 정의된 대상 그룹에 트래픽을 보냄.
- **역할**  
GWLB는 **투명한 네트워크 게이트웨이와 로드 밸런서를 결합**하여 가상 어플라이언스를 배포, 규모 조정 및 관리.
- 여러 가상 어플라이언스에 트래픽을 분산하기 위한 **단일 게이트웨이**(단일 입/출구)를 제공.
- **엔드 포인트**  
GWLB는 Gateway Load Balancer 엔드포인트를 사용하여 **VPC 경계 전체에서 트래픽을 안전하게 교환**.  
이 엔드포인트는 서비스 공급자 VPC의 가상 어플라이언스와 서비스 소비자 VPC의 애플리케이션 서버 간에 프라이빗 연결을 제공.
- **새로운 기능**  
   GWLB는 **사용자 정의 로직**이나 **3rd 파티 솔루션**을 네트워킹 경로에 추가할 수 있는 새로운 기회를 제공.  
   예를 들어, VPC 간에 암호화되지 않은 트래픽이나 TLS1.0/TLS1.1 트래픽이 있는지 확인하는 간단한 응용 프로그램을 작성할 수 있음.

### 장점
- **더 빠른 배포**  
   GWLB는 배포 프로세스를 간소화하여 AWS Marketplace와 파트너가 가상 어플라이언스를 더 빠르게 제공할 수 있도록 함.
- **비용 관리**  
   수요에 따라 가상 어플라이언스를 **자동으로 확장**하여 비용을 효과적으로 관리할 수 있음.
- **가용성 향상**  
   GWLB는 상태 확인을 실행하고 비정상 인스턴스로부터 트래픽을 다시 라우팅하여 계획된 또는 계획되지 않은 가동 중지 시간 동안 정상적인 장애 조치를 보장.
- **거버넌스 분리**  
GWLB는 어플라이언스와 어플리케이션 계정을 분리할 수 있음. 모든 트래픽이 단일 지점으로 중앙집중 관리되며, 보안 정책을 일관되게 적용할 수 있음.

### Use case
- **중앙 집중화**  
   여러 VPC와 사용자 계정에 걸쳐 타사 가상 어플라이언스를 통합하여 운영 오버헤드를 줄이고 일관된 보안 정책을 보장.
- 보안 검사, 컴플라이언스, 정책 제어 등을 위해 가상 어플라이언스를 투명하게 배치.
- Firewalls, Intrusion Detection & Prevention Systems, Deep Packet Inspection Systems, payload manipulation 등

### Protocol
- GWLB와 등록된 가상 어플라이언스 인스턴스는 **포트 6081의 GENEVE 프로토콜**을 사용하여 애플리케이션 트래픽을 교환.  
- 이 프로토콜은 서로 다른 VPC 간에 트래픽을 안전하게 전달하는 데 사용됨.

### Cross-Zone Load Balancing

* Disabled by Default
* 활성화 시, AZ 간 Load Balancing은 **유료**

## Architecture

![GWLB Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/295d388e-f1ac-4738-8932-7c4d32c78137)
