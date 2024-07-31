# [Transit Gateway](https://docs.aws.amazon.com/ko_kr/vpc/latest/tgw/what-is-transit-gateway.html)

## <img src = "https://github.com/user-attachments/assets/0f4786f5-21b4-4b46-bb27-1881a90b97b1" width = "25" height = "25"> Transit Gateway

AWS Transit Gateway는 **여러 Virtual Private Cloud(VPC)와 온프레미스 데이터 센터, AWS Direct Connect 및 VPN 연결(Star Connection)을 중앙 허브를 통해 연결하는 관리형 네트워크 트랜짓 서비스**임. 

이를 통해 **복잡한 네트워크 토폴로지를 단순화하고, 스케일링과 관리 효율성**을 높일 수 있음.

Regional Resource 이지만, Cross-Region에서도 작동할 수 있음.

RAM(Resource Access Manager)를 사용하여 Cross-account를 가능하게 함.

다른 AWS Service에서는 지원하지 않는 **IP Multicast**를 지원함.

## 특징

### 중앙 허브

다수의 VPC 및 온프레미스 네트워크를 중앙 허브를 통해 연결함.

### 확장성

수천 개의 VPC 및 온프레미스 네트워크 연결을 지원함.

### 고가용성

**AWS 리전 내에서 고가용성을 제공**하며, 자동으로 장애 복구를 처리함.

### 보안 및 규정 준수

트래픽을 중앙에서 모니터링하고 제어할 수 있음.

### 간편한 관리

여러 네트워크 연결을 중앙에서 관리할 수 있어 관리 효율성을 높임.

### 대역폭

고성능 네트워크 연결을 지원하여 대규모 데이터 전송을 효율적으로 처리할 수 있음.

## 구성요소

* **Transit Gateway**

    중앙 허브 역할을 하며, 여러 네트워크를 연결하고 라우팅함.

* **Transit Gateway Attachment**

    VPC, 온프레미스 네트워크, Direct Connect, VPN 연결 등을 Transit Gateway에 연결하는 논리적 구성 요소임.

* **Transit Gateway Route Table**

    연결된 네트워크 간의 트래픽 경로를 정의함.

    어떤 VPC가 다른 VPC와 연결될 수 있는지를 정함.

* **Transit Gateway Peering** 

    **다른 리전의 Transit Gateway와 피어링**하여 글로벌 네트워크 연결을 지원함.

## Site-to-Site VPN ECMP

ECMP는 **Equal-cost Multi-path Routing**을 뜻함.

On-premise와 AWS Transit Gateway 사이에 **여러 Site-to-Site VPN**을 연결하는 것을 뜻함.

이를 이용하여 AWS와 연결된 네트워크의 Bandwidth를 증가시키는 데 사용될 수 있음.

너무 많은 연결을 설정하면, 데이터 사용량에 따라 비용이 증가함.

## 아키텍처

### Transit Gateway 설정

AWS Management Console에서 Transit Gateway를 생성함.

### Attachment 설정

연결하려는 VPC, Direct Connect, VPN 등을 Transit Gateway에 연결함.

### 라우팅 설정

Transit Gateway Route Table을 구성하여 각 연결 간의 트래픽 경로를 정의함.

### 보안 그룹 및 네트워크 ACL

각 VPC의 보안 그룹 및 네트워크 ACL을 구성하여 트래픽 제어 및 보안을 강화함.

### Architecture Example

![transit gateway architecture](https://github.com/user-attachments/assets/c76cebef-03d2-462e-9111-3f182975b7e7)


## Use case

* **하이브리드 클라우드**

    온프레미스 데이터 센터와 여러 VPC를 중앙에서 연결하여 하이브리드 클라우드 아키텍처를 구현함.

* **다중 계정 관리**

    여러 AWS 계정의 VPC를 중앙에서 관리하고 연결함.

* **글로벌 네트워크**

    여러 리전 간의 VPC를 연결하여 글로벌 네트워크를 구축함.

* **데이터 마이그레이션**

    온프레미스 데이터 센터에서 AWS 클라우드로 데이터를 안전하게 전송함.

## Sumamry

AWS Transit Gateway는 **여러 VPC와 온프레미스 데이터 센터, AWS Direct Connect 및 VPN을 중앙 허브를 통해 연결하여 복잡한 네트워크 토폴로지를 단순화**하고, 네트워크 관리 효율성을 높이는 서비스임. 

이를 통해 **네트워크를 확장하고 고성능 및 고가용성을 제공하며, 보안 및 비용 효율성을 강화**할 수 있음. 

다양한 사용 사례에 적용할 수 있어 기업의 네트워크 인프라를 효과적으로 관리할 수 있음.