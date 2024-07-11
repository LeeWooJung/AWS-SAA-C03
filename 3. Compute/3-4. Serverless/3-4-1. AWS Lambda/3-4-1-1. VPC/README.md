# VPC

AWS Lambda는 **서버리스 컴퓨팅 서비스**로, 코드를 실행하기 위해 별도의 서버를 관리할 필요 없이 이벤트에 따라 자동으로 트리거되어 실행됨.  

Lambda 함수는 **기본적으로 퍼블릭 인터넷**을 통해 실행되어 VPC 내부의 자원에 접근할 수 없지만, 특정 시나리오에서는 VPC (Virtual Private Cloud) 내의 리소스에 접근할 필요가 있음.  

이때 Lambda 함수는 VPC에 연결되어 해당 리소스에 접근할 수 있음.

## Lambda와 VPC의 연결

Lambda 함수를 VPC에 연결하면 VPC 내의 리소스(예: RDS 인스턴스, ElastiCache 클러스터, EC2 인스턴스 등)에 안전하게 접근할 수 있음.  

이는 Lambda 함수가 **VPC의 서브넷과 보안 그룹을 사용하여 네트워크 트래픽을 제어**할 수 있음을 의미함.

## Lambda와 VPC의 연결 과정

* **VPC 설정**: Lambda 함수가 연결될 VPC를 생성하고, 필요한 **서브넷과 보안 그룹**을 설정함.

* **Lambda 함수 생성 및 설정**:
Lambda 콘솔에서 새로운 함수를 생성함.  
함수 설정 시 **VPC(Define VPC ID), 서브넷, 보안 그룹을 선택**함.

* **서브넷 및 보안 그룹 설정**:
Lambda 함수가 배치될 **서브넷은 인터넷 게이트웨이 또는 NAT 게이트웨이를 통해 외부 네트워크에 접근**할 수 있어야 함.  
보안 그룹은 Lambda 함수가 접근해야 하는 리소스에 대한 인바운드/아웃바운드 규칙을 설정해야 함.

## VPC에 연결된 Lambda 함수의 아키텍처

* **Lambda 함수 실행**: Lambda 함수가 VPC의 특정 서브넷에서 실행됨.

* **네트워크 인터페이스 생성**: Lambda 함수는 실행 시 **[ENI](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-1.%20ENI)** (Elastic Network Interface)를 생성하여 VPC와 통신함.

* **리소스 접근**: 생성된 ENI를 통해 VPC 내의 RDS, ElastiCache 등 리소스에 접근함.

* **인터넷 접근**: Lambda 함수가 외부 인터넷에 접근하려면 NAT 게이트웨이 또는 퍼블릭 서브넷을 통해야 함.

## 장점

* **보안 강화**: Lambda 함수를 VPC에 연결함으로써 민감한 데이터와 리소스에 대한 접근을 제한할 수 있음.

* **내부 리소스 접근**: 퍼블릭 인터넷에 노출되지 않은 VPC 내부 리소스에 안전하게 접근 가능함.

* **네트워크 제어**: 서브넷과 보안 그룹을 통해 Lambda 함수의 네트워크 트래픽을 세밀하게 제어할 수 있음.

## 단점

* **네트워크 설정 복잡성**: Lambda 함수와 VPC를 연결하는 과정에서 네트워크 설정이 복잡해질 수 있음.

* **실행 시간 지연**: ENI 생성과 네트워크 초기화로 인해 Lambda 함수의 콜드 스타트 시간이 길어질 수 있음.

* **인터넷 접근 제한**: Lambda 함수가 VPC에 연결된 경우, 별도의 설정 없이는 퍼블릭 인터넷에 접근할 수 없음.

## Architecture Example

![Lambda in VPC architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/62d1e8bb-0a69-4a55-ad4f-428ec4df26d1)
