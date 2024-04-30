# [ENI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html)

## Elastic Network Interface

### 설명    

가상 네트워크 카드를 나타내는 **논리적 네트워킹 구성 요소**.  
ENI는 인스턴스가 AWS 서비스, 다른 인스턴스, 온프레미스 서버, 인터넷 등 다른 네트워크 리소스와 통신할 수 있도록 함.  
ENI는 다음과 같은 속성을 포함할 수 있음.

### 속성

* VPC의 IPv4 주소 범위 중 기본 프라이빗 IPv4 주소
* VPC의 IPv6 주소 범위 중 기본 IPv6 주소
* VPC의 IPv4 주소 범위 중 하나 이상의 보조 프라이빗 IPv4 주소
* 프라이빗 IPv4 주소당 한 개의 탄력적 IP 주소(IPv4)
* 한 개의 Public IPv4 주소
* 한 개 이상의 IPv6 주소
* 하나 이상의 보안 그룹
* MAC 주소

### 특징
* ENI는 인스턴스에 연결하고, 인스턴스에서 분리한 후 다른 인스턴스에 연결할 수 있음.  
* 인스턴스에 연결하거나 분리한 후 다른 인스턴스에 다시 연결하면 네트워크 인터페이스의 속성이 해당 네트워크 인터페이스를 따름.
*  네트워크 인터페이스를 인스턴스 간에 이동하면 네트워크 트래픽이 새 인스턴스로 리디렉션됨
* 각 인스턴스는 기본 네트워크 인터페이스라는 기본 네트워크 인터페이스를 갖고 있고 주 네트워크 인터페이스는 인스턴스에서 분리할 수 없음.  
하지만, 추가 네트워크 인터페이스를 만들고 연결할 수 있음.  
사용 가능한 최대 네트워크 인터페이스 수는 인스턴스 유형에 따라 다름.

### [보안 그룹](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/4.%20Security%20Group)

AWS의 **Elastic Network Interface**(ENI)는 보안 그룹을 필요로 함.  

보안 그룹이 EC2 인스턴스나 ENI에 연결되지 않은 경우, 이는 연결되지 않은 상태로 간주되며, 이는 보안 및 규정 준수에 영향을 미칠 수 있음.  
따라서, **보안 그룹**을 **Amazon EC2 인스턴스**나 **ENI**에 연결하는 것은 AWS 클라우드 인프라를 보호하고 EC2 워크로드가 잠재적 보안 위협으로부터 보호되도록 하는 데 필수적임.

### Architecture Example
* ENI  
![ENI](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/1777503e-8297-40d7-ac8a-b22861cf958c)
* Fail Over  
![failover](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/f3d9cd7c-cfc6-40dc-a576-a47129200354)
