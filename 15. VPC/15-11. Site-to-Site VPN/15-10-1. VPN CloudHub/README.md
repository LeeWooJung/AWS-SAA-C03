# [VPN CloudHub](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-vpn-cloudhub.html)

AWS의 VPN CloudHub는 **여러 지사와 본사 간의 안전하고 확장 가능한 네트워크 연결을 제공하는 서비스**임. 

**여러 지사 간에 안전한 통신을 가능**(안전한 Multiple VPN Connections)하게 하여 각 지사와 본사가 AWS를 통해 연결되고 서로 통신할 수 있게 함.

VPN CloudHub는 지사들이 **AWS를 통해 서로 연결되도록 지원**하며, 다양한 **지사 네트워크 간의 저렴한 요금의 허브-스포크(hub-and-spoke) 토폴로지를 제공**함. 

VPN 연결이기 때문에 Public Internet을 사용함.

이 서비스는 **AWS Virtual Private Gateway(VGW)를 사용**하여 각 지사가 AWS VPC와 연결되고, 지사 간의 라우팅을 통해 모든 지사 네트워크가 상호 연결됨.

## 특징

### 확장성

다양한 지사를 쉽게 연결할 수 있음.

### 보안성

**IPsec VPN 터널을 통해 데이터 전송이 암호화되어 보안성이 강화**됨.

### 간편한 관리

AWS Management Console을 통해 쉽게 설정 및 관리 가능함.

### 고가용성

여러 VPN 터널을 통해 고가용성을 보장함.

### 비용 효율성

전용 회선보다 비용 효율적임.

## 구성요소

* **Virtual Private Gateway** (VGW)

    AWS 측에서 VPN 터널을 종료하는 지점.

* **Customer Gateway** (CGW)

    각 지사 측에서 VPN 터널을 종료하는 지점.

* **VPN 연결**

    각 지사와 VGW 간에 설정된 IPsec VPN 터널.

* **라우팅 테이블**

    각 지사의 라우팅 테이블을 통해 다른 지사와의 통신 경로를 설정함.

## 아키텍처

### 지사 네트워크 설정

각 지사에 Customer Gateway를 구성함.

### AWS VPC 연결

Virtual Private Gateway를 생성하고 AWS VPC에 연결함.

### VPN 터널 설정

각 지사와 VGW 간에 IPsec VPN 터널을 설정함.

### 라우팅 설정

각 지사와 본사 간의 통신을 가능하게 하기 위해 라우팅 테이블을 설정함.

### 허브-스포크 토폴로지

VGW를 허브로 사용하여 각 지사가 스포크로 연결됨.

## Use case

* **지사 간 연결**

    여러 지사를 안전하게 연결하여 데이터 및 애플리케이션에 접근할 수 있음.

* **하이브리드 네트워크**

    온프레미스 데이터 센터와 AWS 간의 안전한 연결을 통해 하이브리드 네트워크를 구현할 수 있음.

* **백업 및 복구**

    지사 데이터의 안전한 백업 및 복구를 위해 사용함.

* **통합 네트워크 관리**

    여러 지사를 AWS를 통해 중앙에서 관리할 수 있음.

## Summary

AWS의 VPN CloudHub는 여러 **지사와 본사 간의 안전하고 확장 가능한 네트워크 연결을 제공하는 서비스**임. 

이를 통해 **지사들이 AWS를 통해 서로 연결되고 안전하게 통신**할 수 있음. 

IPsec VPN 터널을 통해 데이터 전송이 암호화되어 보안성을 강화하고, AWS Management Console을 통해 쉽게 설정 및 관리할 수 있음. 

주요 사용 사례로는 지사 간 연결, 하이브리드 네트워크 구현, 백업 및 복구 등이 있음. 

인터넷 의존성과 성능 제한 등의 단점이 있지만, 보안 강화, 비용 절감, 확장 용이성 등의 장점이 있음.