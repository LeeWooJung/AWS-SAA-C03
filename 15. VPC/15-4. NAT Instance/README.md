# NAT Instance

AWS의 NAT 인스턴스(NAT Instance)는 퍼블릭 서브넷에 위치하며 **프라이빗 서브넷에 위치한 인스턴스가 인터넷으로 아웃바운드 트래픽을 보낼 수 있도록 하면서도 인바운드 트래픽은 차단**하는 **네트워크 주소 변환**(Network Address Translation, NAT) 기능을 제공하는 **EC2 인스턴스**임. 

이는 주로 보안 강화를 위해 **프라이빗 서브넷의 인스턴스가 직접 인터넷과 통신하지 않도록 하는 데 사용**됨.

EC2 Setting(Souce/Destination Check)를 비활성화 해야함.

NAT Instance를 사용하기 위해서는 **Elastic IP**를 NAT Instance에 추가해주어야함.

**Outdated**된 것이지만, SAA 시험에 종종 나옴.

미리 구성된 Amazon Linux AMI를 사용할 수 있음(**2020.12.31**이후로 지원이 종료됨).


## 특징

### 퍼블릭 서브넷에 배치

NAT 인스턴스는 **퍼블릭 서브넷에 배치되어 퍼블릭 IP 주소**를 가짐.

### 보안 그룹

NAT 인스턴스에 대한 접근을 제어하는 **보안 그룹**을 설정할 수 있음.

* **Inbound**

    * Private Subnet에서 전송되는 트래픽에대한 HTTP/HTTPS를 허용해야함.

    * Internet Gateway에서 전송되는 SSH를 허용해야함.

* **Outbound**

    * Internet으로의 HTTP/HTTPS Outbound를 허용해야함.

### 라우팅 테이블

프라이빗 서브넷의 라우팅 테이블에 NAT 인스턴스로의 경로를 추가해야 함.

### 고가용성

NAT 인스턴스를 고가용성으로 설정하려면 **여러 가용 영역에 인스턴스를 배포하고, 자동 장애 조치를 구성**해야 함.

즉, **ASG**를 생성하고, Multi-AZ 구성을 직접 작성해야함.

## 구성요소

* **퍼블릭 서브넷**

    NAT 인스턴스가 위치한 서브넷으로, 인터넷 게이트웨이를 통해 외부와 연결됨.

* **프라이빗 서브넷**

    인터넷과 직접 연결되지 않는 서브넷으로, NAT 인스턴스를 통해 인터넷에 접근함.

* **인터넷 게이트웨이**

    퍼블릭 서브넷과 인터넷 간의 연결을 제공함.

* **라우팅 테이블**

    프라이빗 서브넷의 트래픽을 NAT 인스턴스로 라우팅함.

* **보안 그룹**

    NAT 인스턴스의 인바운드 및 아웃바운드 트래픽을 제어함.

## 아키텍처

### NAT 인스턴스 생성

퍼블릭 서브넷에 NAT 인스턴스를 생성하고 **퍼블릭 IP 주소를 할당**함.

### 보안 그룹 설정

NAT 인스턴스에 대한 접근을 제어하는 보안 그룹을 설정함.

### 라우팅 테이블 구성

프라이빗 서브넷의 라우팅 테이블에 **0.0.0.0/0 대상으로 NAT 인스턴스를 향하는 경로를 추가**함.

### 프라이빗 서브넷 리소스 구성

프라이빗 서브넷의 **리소스가 NAT 인스턴스를 통해 인터넷에 접근할 수 있도록 설정**함.

## Use case

* **소프트웨어 업데이트**

    프라이빗 서브넷의 인스턴스가 인터넷을 통해 **소프트웨어 업데이트**를 받을 수 있도록 함.

* **데이터 수집 및 전송**

    프라이빗 서브넷의 애플리케이션이 외부 API와 통신하거나 데이터를 전송할 수 있도록 지원함.

* **보안 강화**

    중요한 데이터나 서비스가 위치한 프라이빗 서브넷을 보호하면서도 인터넷 접근을 제공함.

## Summary

AWS의 NAT 인스턴스는 **프라이빗 서브넷 내의 리소스가 인터넷으로 아웃바운드 트래픽을 보낼 수 있도록 하면서도 인바운드 트래픽을 차단**하는 네트워크 주소 변환 기능을 제공하는 **퍼블릭 서브넷에 배치된 EC2 인스턴스**임. 

이를 통해 보안이 중요한 네트워크 환경에서 프라이빗 리소스가 직접 인터넷에 노출되지 않도록 보호할 수 있음. 

보안 강화, 네트워크 주소 변환, 유연성 등의 장점을 제공하지만, 관리 오버헤드, 고가용성 설정 필요, 성능 한계 등의 단점이 있음. 

주요 사용 사례로는 소프트웨어 업데이트, 데이터 수집 및 전송, 보안 강화 등이 있음.