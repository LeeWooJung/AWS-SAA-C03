# [Direct Connect](https://docs.aws.amazon.com/ko_kr/directconnect/latest/UserGuide/Welcome.html)

## <img src = "https://github.com/user-attachments/assets/85e5933c-9867-4317-bc00-5f98acc12b59" width = "25" height = "25"> Direct Connect

AWS Direct Connect는 사용자의 **온프레미스 데이터 센터와 AWS 클라우드(VPC) 간에 물리적인 전용 네트워크 연결(Private)을 제공하는 서비스**임. 

이를 통해 **인터넷을 거치지 않고 안정적이고 일관된 네트워크 성능(네트워크 지연 시간, 패킷 손실 최소화)을 제공하며, 데이터 전송 비용을 절감**할 수 있음.

대역폭 요구 사항에 따라 1Gbps에서 100Gbps까지 다양한 속도의 연결을 제공함.

VPC와 On-Premise를 연결하는 것이기 때문에, VPC에 **Virtual Private Gateway**를 셋업해야함.

같은 Direct Connect 연결로도 **AWS의 Public Resource(S3 등)와 Private Resource(EC2)에 연결**할 수 있음. 이 때, Public Resource와의 연결을 위해서 **Public Virtual Interface**가 필요하고, Private Resource와의 연결을 위해서 **Private Virtual Interface**가 필요.

IPv4와 IPv6 모두 지원함.

## 특징

### 고성능

**전용 회선을 통해 일관된 네트워크 성능**을 제공함.

### 보안성

**인터넷을 경유하지 않기 때문에 데이터 전송의 보안성이 강화**됨.

### 비용 효율성

대량의 데이터 전송 시 데이터 전송 비용을 절감할 수 있음.

### 유연성

다양한 대역폭 옵션을 통해 유연한 네트워크 구성 가능함.

### 하이브리드 클라우드 지원

온프레미스 인프라와 AWS 클라우드를 쉽게 통합할 수 있음.

## 구성요소

* **Direct Connect 위치**

    AWS와 사용자의 네트워크가 연결되는 물리적 위치.

* **AWS Direct Connect 연결**

    사용자의 네트워크 장비와 AWS Direct Connect 로케이션 간의 전용 네트워크 연결.

* **가상 인터페이스**(VIF)

    Direct Connect 연결을 통해 AWS 리소스에 접근하기 위한 **논리적 인터페이스**.

* **공용 가상 인터페이스**(Public Virtual Interface)

    퍼블릭 AWS 서비스에 접근하기 위해 사용됨.

* **사설 가상 인터페이스**(Private Virtual Interface)

    VPC에 직접 접근하기 위해 사용됨.

* **트랜짓 가상 인터페이스**

    AWS Transit Gateway와 연결하기 위해 사용됨.

* **라우팅 설정**

    온프레미스와 AWS 간의 트래픽 라우팅을 위한 BGP(Border Gateway Protocol) 설정.

## Direct Connect Gateway

같은 계정에서 사용되는 서로 다른 Region에 존재하는 한 개 이상의 VPC와 연결하고 싶을 때, **Direct Connect**를 설정해야함.

Direct Connect Gateway는 여러 VPC와 Direct Connect 사이에서 연결을 도움.

## Encryption

물리적이고 Private한 연결을 통해 데이터가 전송되므로 **암호화되지 않음**.

Data의 암호화를 위해서는 **VPN Connection**을 같이 사용하여야함.

> [VPC] <--> [AWS Direct Connect Endpoint] <--> [VPN Connection] <--> [On-Premise]

위와 같이 연결하면 **IPsec-encrypted**를 제공받을 수 있음. 하지만 복잡한 설치 과정을 거쳐야함.

## Resiliency

**AWS Direct Connect Location**을 여러 개 두고, 각 Data Center와 따로 연결하여 Resiliency를 획득할 수 있음.

혹은, **AWS Direct Connect Location**에서 On-premise와 여러 연결을 설정하여 Resiliency를 최대로 획득할 수도 있음.

## with Site-to-Site VPN (Backup)

On-premise와 AWS VPC에 **Direct Connect**와 **VPN**을 모두 연결하여, **Site-to-Site VPN** 연결을 Direct Connect 연결에 문제가 생겼을 때의 **백업**으로 사용할 수 있음.

이는, On-premise와 VPC 사이에 여러 Direct Connect를 두어 Backup을 설정하는 것보다 **비용면에서 유리**함.

## 아키텍처

### Direct Connect 로케이션

AWS Direct Connect 로케이션에 네트워크 장비를 설치함.

### 전용 회선 설정

사용자의 온프레미스 네트워크와 Direct Connect 로케이션 간에 전용 회선을 설정함.

### 가상 인터페이스 설정

퍼블릭, 사설 또는 트랜짓 가상 인터페이스를 설정하여 AWS 리소스에 접근함.

### 라우팅 설정

BGP를 사용하여 온프레미스와 AWS 간의 트래픽 라우팅을 구성함.

### Architecture Example

![direct connect architecture](https://github.com/user-attachments/assets/a9a05da9-7f91-4d7a-8272-ac2497b85755)

## 장점

* **안정성**

    인터넷의 변동성에 영향을 받지 않기 때문에 일관된 네트워크 성능을 제공함.

* **보안**

    인터넷을 통하지 않기 때문에 데이터 전송 시 보안이 강화됨.

* **비용 절감**

    대량의 데이터 전송 시 데이터 전송 비용을 절감할 수 있음.

* **고속 전송**

    최대 100Gbps의 고속 연결을 제공하여 대용량 데이터 전송에 적합함.

* **유연한 네트워크 구성**

    다양한 가상 인터페이스 옵션을 통해 유연한 네트워크 구성을 지원함.

## 단점

* **초기 설치 비용**

    전용 회선 설치 및 구성에 초기 비용이 발생할 수 있음.

* **제한된 접근성**

    Direct Connect 로케이션이 특정 지역에 한정되어 있을 수 있음.

* **구성 복잡성**

    네트워크 설정 및 라우팅 구성이 복잡할 수 있음.

## Use case

* **데이터 마이그레이션**

    온프레미스 데이터 센터에서 AWS로 대량의 데이터를 빠르고 안전하게 전송함.

* **하이브리드 클라우드**

    온프레미스 인프라와 AWS 클라우드를 통합하여 일관된 하이브리드 환경을 구축함.

* **백업 및 복구**

    온프레미스 데이터를 AWS로 백업하고 복구하는 데 사용함.

* **고성능 컴퓨팅**

    고성능 컴퓨팅 워크로드를 AWS 클라우드로 확장함.

## Sumamry

AWS Direct Connect는 **온프레미스 데이터 센터와 AWS 클라우드 간에 전용 네트워크 연결을 제공하는 서비스**임. 

**인터넷을 경유하지 않고** 안정적이고 일관된 네트워크 성능을 제공하며, 보안성과 비용 효율성을 높임. 

다양한 대역폭 옵션과 유연한 네트워크 구성을 지원하여 **하이브리드 클라우드, 데이터 마이그레이션, 백업 및 복구** 등 다양한 사용 사례에 적합함.

초기 설치 비용과 설정의 복잡성 등이 단점이 될 수 있지만, 고성능과 안정성을 제공하는 것이 큰 장점임.






