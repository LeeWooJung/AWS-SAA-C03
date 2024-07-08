# Load Balancer

## Load Balancer Integration

Amazon ECS(Elastic Container Service)는 **컨테이너화된 애플리케이션을 관리하고 배포하는 서비스**임.  

ECS는 다양한 종류의 Load Balancer와 통합될 수 있으며, 이를 통해 **애플리케이션의 가용성과 확장성을 높일 수 있음**.

## Application Load Balancer (ALB)

[ALB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-2.%20Application%20Load%20Balancer)는 HTTP와 HTTPS 트래픽을 대상으로 하는 계층 7의 로드 밸런서임.  

애플리케이션의 경로 기반 라우팅, 호스트 기반 라우팅, 웹소켓 및 HTTP/2를 지원함.

### 특징

* **경로 기반 라우팅**: URL 경로를 기반으로 트래픽을 다른 대상 그룹으로 라우팅할 수 있음.
* **호스트 기반 라우팅**: 호스트 헤더를 기반으로 트래픽을 라우팅할 수 있음.
* **웹소켓 및 HTTP/2 지원**: 최신 웹 기술을 지원하여 실시간 통신이 가능함.
* **대상 그룹**: ALB는 ECS 서비스의 태스크를 대상으로 지정할 수 있는 대상 그룹을 지원함.

## Network Load Balancer (NLB)

[NLB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-3.%20Network%20Load%20Balancer)는 TCP, UDP 및 TLS 트래픽을 대상으로 하는 계층 4의 로드 밸런서임.  

높은 성능과 낮은 지연 시간을 제공함.

### 특징

* **고성능**: 초당 수백만 요청을 처리할 수 있음.
* **고정 IP**: NLB는 고정된 IP 주소를 제공하며 Elastic IP와 통합될 수 있음.
* **TLS 종료**: TLS 트래픽을 종료하고 복호화할 수 있음.
* **대상 그룹**: ECS 서비스의 태스크를 대상으로 지정할 수 있는 대상 그룹을 지원함.

## Classic Load Balancer (CLB)

[CLB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-1.%20Classic%20Load%20Balancer(deprecated))는 계층 4 및 계층 7에서 트래픽을 처리할 수 있는 로드 밸런서임.  

HTTP/HTTPS 및 TCP 트래픽을 모두 처리할 수 있음.

그러나, 사용이 권장되지 않음.