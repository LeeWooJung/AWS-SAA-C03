# [Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/7eb7e3ec-3ae4-464e-9310-4d9b6d638322" width = "25" height = "25"> Load Balancer

### 설명    

**AWS Load Balancer**는 AWS에서 제공하는 관리형 서비스로, 클라이언트와 서버 그룹 사이에 위치하여 **서버에 가해지는 트래픽을 여러 대의 서버에 고르게 분배**하여 특정 서버의 부하를 덜어주는 역할을 함.  
EC2 인스턴스, 컨테이너, IP 주소, 마이크로서비스, Lambda 함수 등 다양한 서비스와 연계하여 부하를 분배할 수 있음.

### 사용 이유

* 부하를 다수의 다운 스트림 인스턴스로 분산함.  
* 애플리케이션에 단일 액세스 지점을 노출.  
* 다운스트림 인스턴스의 장애를 처리.  
* 인스턴스 상태를 확인할 수 있음.  
* 웹 사이트에 SSL Termination을 제공함.  
* 쿠키로 stickiness를 강화함.  
* 고가용성을 제공함.  
* 클라우드 내에서 개인 트래픽과 공공 트래픽을 분리함.  

### How to Health Check

* AWS에서는 대상 그룹의 대상에 대한 상태 확인을 구성할 수 있음.  
* **로드 밸런서**는 등록된 대상으로 요청을 주기적으로 전송하여 상태를 확인함.  
* 대상이 응답하는 데 걸리는 시간은 다음 상태 확인 요청의 간격에 영향을 미치지 않음.  
* 대상이 초기 상태 확인을 통과한 후에는 상태가 **Healthy**가 됨.
* 대상이 상태 확인에 응답하지 않거나 상태 확인에 실패하면 로드 밸런서는 대상을 서비스 중단시킴.  
* 상태 확인의 HealthyThresholdCount 연속 성공 횟수를 초과하면 로드 밸런서는 대상을 다시 서비스 상태로 전환.

### 종류

* **ALB** (Application Load Balancer)  
복잡한 최신 애플리케이션에 적합하며, 단일 애플리케이션 기능을 전담하는 여러 서버를 포함하는 서버 팜에 사용됨.
    * HTTP, HTTPS, WebSocket
* **NLB** (Network Load Balancer)  
성능이 매우 높으며, 초당 수백만 건의 요청을 처리하고 지연 시간도 ALB에 비해 짧음.  
    * TCP, TLS, UDP
* **GLB** (Gateway Load Balancer)  
Network Layer에서 작동함.  
    * Layer3, IP Protocol
* **CLB** (Classic Load Balancer)  
과거 버전이며, 현재는 사용되지 않음.

### Integrated AWS Services

* EC2(Elastic Compute Cloud)
    * EC2
    * EC2 Auto Scaling Groups
    * ECS
* Containers
* Lambda Functions
* VPC(Virtual Private Cloud)
* AWS Outposts
* ACM(Amazon Certificate Manager)
* Cloud Watch
* Route 53
* AWS WAF
* AWS Global Accelerator

### Load Balancer with Security Group

AWS Load Balancer의 Security Group은 **로드 밸런서와 연결된 백엔드 인스턴스 간의 연결을 제어하는 역할**을 함.  

* **Frontend Security Groups**  
클라이언트가 로드 밸런서에 액세스할 수 있는지 결정.  
* **Backend Security Groups**  
로드 밸런서가 대상, 예를 들어 EC2 인스턴스나 ENIs 등에 연결할 수 있도록 허용.

### Link with EC2

* EC2 인스턴스와 연결된 보안 그룹은 로드 밸런서로부터의 트래픽만 수락하도록 제한할 수 있음(대상 보안 그룹의 **인바운드 규칙**에서 로드 밸런서의 보안 그룹을 원본으로 설정하여 달성할 수 있음).  
* Network Load Balancer의 경우, 로드 밸런서를 만들 때 보안 그룹을 선택할 필요가 없음.  
* 그러나 보안 그룹 없이 Network Load Balancer를 만드는 경우 나중에 보안 그룹을 연결할 수 없음.  
* EC2 보안 그룹은 ELB 액세스를 허용해야 함. 즉, **ELB 보안 그룹 ID를 정의하는 규칙을 포트 80 및 443에 추가**해야 함.

### Simple Architecture

![Simple Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/60821600-5703-43d7-8bb8-3080d83ca648)

### Architecture with Security Group

![Security Group](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/526a4c33-26be-4db9-ac59-9ee15aea32ad)


