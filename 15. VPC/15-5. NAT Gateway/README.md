# [NAT Gateway](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-nat-gateway.html)

## <img src = "https://github.com/user-attachments/assets/96f7b663-2379-4a8b-81c1-04543374cedc" width = "25" height = "25"> NAT Gateway

AWS의 NAT Gateway는 AWS에서 제공하는 완전 관리형 서비스로, 퍼블릭 서브넷에 배치되어 퍼블릭 IP 주소를 가지며, **VPC 내 프라이빗 서브넷에 위치한 인스턴스가 인터넷으로 아웃바운드 트래픽을 보낼 수 있도록 하면서도 인바운드 트래픽은 차단**하는 네트워크 주소 변환(**Network Address Translation, NAT**) 서비스임. 

이는 주로 **보안 강화를 위해 프라이빗 서브넷의 인스턴스가 직접 인터넷과 통신하지 않도록 하는 데 사용**됨.

Bandwidth와 사용 시간에 따라 **비용**을 지불함.

NAT Gateway는 **Elastic IP**를 사용하는 특정 **가용 영역**(AZ)에 생성됨.

동일 Subnet에 있는 EC2 인스턴스는 NAT Gateway를 사용할 수 없음. 오로지 **다른 Subnet**에 존재하는 EC2 인스턴스만이 사용할 수 있음.

NAT Instance와 달리 **관리해야 할 Security Group이 존재하지 않음**.

## 특징

### 고가용성

NAT Gateway는 **자동으로 고가용성을 제공하며, AWS가 이를 관리**함.

하지만, **하나의 가용 영역**에서만 가능함.

여러 AZ에서 가용성을 지키기 위해서는(Fault-tolerance) **여러 가용영역에 각각 여러 NAT Gateway**를 생성해야 함.

각 가용영역에 NAT Gateway를 따로 생성해주어야 하므로, **Cross-AZ FailOver**가 필요하지 않음(AZ가 다운되면 NAT Gateway가 필요 없어지므로).

### 확장성

**필요에 따라 자동으로 확장되어 높은 트래픽을 처리**할 수 있음.

### Bandwidth

Higher Bandwidth를 제공함.

5Gbps of Bandwidth에서 자동으로 100Gbps까지 Scale up 가능함.

### 퍼블릭 IP 주소

퍼블릭 서브넷에 배치되며, **퍼블릭 IP 주소 또는 엘라스틱 IP 주소**를 가짐.

### 관리 용이성

AWS에서 **완전 관리형**으로 제공되어 사용자 관리가 필요 없음(운영 오버헤드 감소).

### 보안

인바운드 트래픽은 차단되고 아웃바운드 트래픽만 허용됨.

## 구성요소

* **퍼블릭 서브넷**

    NAT Gateway가 위치한 서브넷으로, 인터넷 게이트웨이를 통해 외부와 연결됨.

* **프라이빗 서브넷**

    NAT Gateway를 통해 인터넷에 접근하는 리소스가 위치한 서브넷.

* **인터넷 게이트웨이**

    퍼블릭 서브넷과 인터넷 간의 연결을 제공함.

* **라우팅 테이블**

    **프라이빗 서브넷의 트래픽을 NAT Gateway로 라우팅**하기 위해 구성됨.

* **NAT Gateway**

    **네트워크 주소 변환을 수행하는 관리형 서비스**.

## 아키텍처

### NAT Gateway 생성

퍼블릭 서브넷에 NAT Gateway를 생성하고 **퍼블릭 IP 주소를 할당**함.

### 라우팅 테이블 설정

프라이빗 서브넷의 라우팅 테이블에 **0.0.0.0/0 대상으로 NAT Gateway를 향하는 경로**를 추가함.

### 프라이빗 서브넷 리소스 구성

**프라이빗 서브넷의 리소스가 NAT Gateway를 통해 인터넷에 접근**할 수 있도록 설정함.


## Use case

* **소프트웨어 업데이트**

    프라이빗 서브넷의 인스턴스가 인터넷을 통해 소프트웨어 업데이트를 받을 수 있도록 함.

* **데이터 수집 및 전송**

    프라이빗 서브넷의 애플리케이션이 외부 API와 통신하거나 데이터를 전송할 수 있도록 지원함.

* **보안 강화**

    중요한 데이터나 서비스가 위치한 프라이빗 서브넷을 보호하면서도 인터넷 접근을 제공함.

## vs. NAT Instance

|특징|NAT Gateway|NAT Instance|
|:---|:---|:---|
|Availability|자동 High Availability within AZ|Instance 간의 FailOver를 위해 직접 스크립트 작성|
|BandWidth|5~100Gbps|EC2 인스턴스 타입에 따라 다름|
|Maintenance|AWS가 관리|사용자가 직접 관리|
|Cost|시간당 사용량, Bandwidth|시간당 EC2 instance 사용, 타입, 크기 & Network 사용량|
|Public IPv4|가능|가능|
|Private IPv4|가능|가능|
|Security Group|없음|사용|
|Bastion Host|없음|사용|

## Summary

AWS의 NAT Gateway는 **프라이빗 서브넷 내의 리소스가 인터넷으로 아웃바운드 트래픽을 보낼 수 있도록 하면서도 인바운드 트래픽을 차단하는 관리형 네트워크 주소 변환 서비스**임. 

**퍼블릭 서브넷에 배치**되며, **자동으로 고가용성 및 확장성을 제공**하고, 관리 용이성과 보안 강화를 특징으로 함. 

주요 사용 사례로는 소프트웨어 업데이트, 데이터 수집 및 전송, 보안 강화 등이 있음. 

NAT Gateway는 비용이 발생할 수 있으며, **정적 IP 주소 제공과 사용자 정의 설정에 제한**이 있을 수 있음.