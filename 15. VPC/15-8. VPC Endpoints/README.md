# [VPC Endpoints](https://docs.aws.amazon.com/whitepapers/latest/aws-privatelink/what-are-vpc-endpoints.html)

## <img src = "https://github.com/user-attachments/assets/7c4a3b81-3828-4463-8993-9f1cfeb55d91" width = "25" height = "25"> VPC Endpoints

AWS의 VPC 엔드포인트는 **VPC 내 리소스가 인터넷 게이트웨이, NAT 디바이스, VPN 연결 없이 AWS 서비스와 안전하게 통신할 수 있도록 하는 기능**임. 

VPC 엔드포인트(Powered by AWS PrivateLink)를 사용하면 **프라이빗 네트워크 내부에서 AWS 서비스에 대한 접근을 제공하여 보안성과 성능을 향상**시킬 수 있음.

중복되어 설정될 수 있으며, 높은 가용성(Scale horizontally)을 가짐.

VPC 엔드포인트는 두 가지 유형이 있음.

### 게이트웨이 엔드포인트 (Gateway Endpoint)

S3 및 DynamoDB와 같은 서비스에 사용되며, **라우팅 테이블을 통해 설정**됨.

보안 그룹(Security Group)을 사용하지 않음.

**비용**: 무료

### 인터페이스 엔드포인트 (Interface Endpoint)

**Elastic Network Interface**(ENI)를 사용하여 VPC 내의 서비스에 대한 프라이빗 IP 주소를 제공함.

ENI에는 보안그룹을 설정해야함.

대부분의 AWS Service와 연결할 수 있음.

On-premis(Site to Site VPN, Direct Connect)와 다른 VPC 혹은 다른 Region에 연결할 때 선호됨.

**비용**: 시간당, 전송되는 데이터 GB당 금액이 설정됨.

## 특징

### 인터넷 연결 불필요

VPC 내부에서 AWS 서비스에 접근하기 위해 **인터넷 연결이 필요 없음**.

### 보안성 향상

**트래픽이 AWS 네트워크 내에서만 이동하므로 보안성이 높아짐**.

### 네트워크 비용 절감

**인터넷 게이트웨이나 NAT 디바이스를 사용하지 않으므로 데이터 전송 비용이 절감**됨.

### 간편한 설정

VPC 라우팅 테이블이나 ENI를 통해 간편하게 설정할 수 있음.

### 고가용성

**AWS 관리형 서비스**로서 높은 가용성과 안정성을 제공함.

## 구성요소

* **VPC**

    엔드포인트가 설정될 가상 프라이빗 클라우드.

* **게이트웨이 엔드포인트**

    **S3 및 DynamoDB와 같은 서비스에 대해 라우팅 테이블을 통해 설정**됨.

* **인터페이스 엔드포인트**

    **ENI를 통해 VPC 내의 서비스에 대한 프라이빗 IP 주소를 제공**함.

* **라우팅 테이블**

    게이트웨이 엔드포인트의 경우, 라우팅 테이블에 엔드포인트를 통해 접근할 경로를 추가함.

* **보안 그룹**

    **인터페이스 엔드포인트의 경우, ENI에 보안 그룹을 적용**하여 트래픽을 제어함.

## 아키텍처

### 게이트웨이 엔드포인트 설정

**라우팅 테이블에 경로를 추가**하여 S3 또는 DynamoDB와 같은 서비스에 대한 접근을 설정함.

### 인터페이스 엔드포인트 설정

**ENI를 생성하고 해당 ENI에 프라이빗 IP 주소를 할당하여 서비스에 대한 접근을 설정**함.

### 보안 그룹 적용

**인터페이스 엔드포인트의 ENI에 보안 그룹을 적용**s하여 트래픽을 제어함.

### 라우팅 테이블 구성

트래픽이 엔드포인트를 통해 전달되도록 라우팅 테이블을 구성함.


## Use case

* **데이터 보안**

    중요한 데이터가 있는 VPC 내에서 S3와 같은 서비스에 접근할 때 보안을 강화하기 위해 사용함.

* **비용 절감**

    인터넷 게이트웨이 및 NAT 디바이스 사용을 최소화하여 비용을 절감하기 위해 사용함.

* **성능 최적화**

    **인터넷을 경유하지 않고 빠른 네트워크 통신이 필요**한 경우 사용함.

* **애플리케이션 호스팅**

    **프라이빗 서브넷에서 호스팅된 애플리케이션이 S3와 같은 AWS 서비스에 접근**해야 할 때 사용함.

## Summary

AWS의 VPC 엔드포인트는 **VPC 내 리소스가 인터넷을 거치지 않고 AWS 서비스와 안전하게 통신할 수 있도록 하는 기능**임. 

**게이트웨이 엔드포인트와 인터페이스 엔드포인트**의 두 가지 유형이 있으며, 이를 통해 프라이빗 네트워크 내부에서 AWS 서비스에 대한 접근을 제공하여 보안성과 성능을 향상시킬 수 있음. 

**보안 강화, 비용 절감, 성능 향상 등의 장점**이 있지만, 서비스 제한과 추가 구성 필요 등의 단점도 있음. 

주요 사용 사례로는 데이터 보안, 비용 절감, 성능 최적화 등이 있음.