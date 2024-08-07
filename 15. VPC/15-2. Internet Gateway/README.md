# [Internet Gateway](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_Internet_Gateway.html)

## <img src = "https://github.com/user-attachments/assets/aa0d529f-df20-4368-b407-bc85e113d712" width = "25" height = "25"> Internet Gateway(IGW)

Internet Gateway는 **VPC와 인터넷 간의 네트워크 트래픽을 라우팅하는 네트워크 구성 요소**로, **VPC 내의 리소스가 인터넷과의 양방향 통신을 가능**하게 함. 

인터넷 게이트웨이는 논리적 장치로서 AWS 인프라의 일부이며, **VPC에 하나의 인터넷 게이트웨이를 연결**할 수 있음. 반대도 마찬가지임. 따라서 VPC와 **1:1**의 관계를 가짐.

VPC와 별개로 생성되어야함.

Internet Gateway는 그 자체로는 **Internet에 접근할 수 없음**. Route table이 수정되어야함.

## 특징

### 양방향 통신

VPC 내의 리소스가 **인터넷과 양방향 통신**을 할 수 있게 해줌.

### 고가용성

인터넷 게이트웨이는 **AWS 리전 내에서 고가용성을 제공**하도록 설계됨.

### 확장성

**자동으로 확장(Scales Horizontally)되며, 추가적인 설정 없이 고용량의 트래픽을 처리**할 수 있음.

### 고유한 IP 주소 사용

**퍼블릭 IP 주소 또는 엘라스틱 IP 주소를 통해 VPC 내 리소스가 인터넷과 통신**할 수 있음.

### VPC 내의 라우팅 테이블

**인터넷 게이트웨이와 연결된 서브넷의 라우팅 테이블에 기본 라우트(destination: 0.0.0.0/0)를 추가**해야 함.

## 구성요소

* **Internet Gateway**

    **VPC와 인터넷 간의 트래픽을 라우팅**하는 논리적 장치임.

* **라우팅 테이블**

    서브넷의 트래픽을 인터넷 게이트웨이로 라우팅하기 위해 필요한 경로를 설정함.

* **퍼블릭 IP 주소**

    **VPC 내의 리소스가 인터넷과 통신하기 위해 필요한 IP 주소**임.

* **서브넷**

    인터넷 게이트웨이와 연결된 퍼블릭 서브넷을 통해 인터넷 통신이 가능함.

## 아키텍처

### 인터넷 게이트웨이 생성

VPC에 인터넷 게이트웨이를 생성하고 연결함.

### 라우팅 테이블 설정

**퍼블릭 서브넷의 라우팅 테이블에 인터넷 게이트웨이로의 경로를 추가**함.

### 퍼블릭 IP 주소 할당

**인터넷과 통신할 인스턴스에 퍼블릭 IP 주소 또는 엘라스틱 IP 주소를 할당**함.

### 보안 설정

보안 그룹과 네트워크 ACL을 통해 인터넷에서의 접근을 제어함.

## Use case

* **웹 서버 호스팅**

    퍼블릭 서브넷에 웹 서버를 배치하여 인터넷에서 접근 가능하게 함.

* **API 서버**

    인터넷에서 접근할 수 있는 API 서버를 배치하여 외부 애플리케이션과의 통신을 지원함.

* **소프트웨어 업데이트**

    VPC 내의 인스턴스가 인터넷을 통해 소프트웨어 업데이트를 받을 수 있도록 함.

* **데이터 수집 및 분석**

    외부에서 데이터를 수집하고 분석하는 애플리케이션을 지원함.

## Summary

AWS의 Internet Gateway는 **VPC와 인터넷 간의 양방향 통신을 가능하게 하는 고가용성 네트워크 구성 요소**임. 

이는 **퍼블릭 서브넷을 통해 VPC 내의 리소스가 인터넷과 통신**할 수 있도록 하며, **퍼블릭 IP 주소나 엘라스틱 IP 주소**를 통해 접근할 수 있게 함. 

인터넷 게이트웨이는 고가용성과 확장성을 제공하며, 간편한 설정으로 인터넷 연결을 지원함. 

그러나 보안 설정과 관련된 위험이 있을 수 있으며, 엘라스틱 IP 주소 사용 시 추가 비용이 발생할 수 있음. 

주요 사용 사례로는 웹 서버 호스팅, API 서버, 소프트웨어 업데이트, 데이터 수집 및 분석 등이 있음.