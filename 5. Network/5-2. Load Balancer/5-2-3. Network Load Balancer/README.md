# [Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/9be75430-b203-4add-b571-8148af569286" width = "30" height = "30"> Network Load Balancer    

### 설명

**Network Load Balancer**(NLB)는 **Amazon Elastic Load Balancing**(ELB)에서 제공하는 서비스.  
**Amazon EC2 인스턴스**, 컨테이너 및 IP 주소와 같은 여러 대상에 수신 트래픽을 **자동으로 분산**하여 애플리케이션 가용성을 향상시킴. 

### 특징

1. **고성능**  
NLB는 **OSI(개방형 시스템 상호 연결) ​​모델**의 **4번째 계층**에서 작동하므로 **초당 수백만 개의 요청**을 처리하는 데 적합함.

2. **장기 TCP 연결**  
NLB는 장기 **TCP 연결**을 지원하므로 **WebSockets**과 같은 애플리케이션에 이상적.

3. **AWS 서비스와의 통합**  
NLB는 **Auto Scaling**, **Elastic Container Service(ECS)**, **CloudFormation** 등을 포함한 다양한 AWS 서비스와 통합됨.

4. **교차 AZ 로드 밸런싱**  
NLB는 교차 가용 영역(AZ) 로드 밸런싱을 활성화하여 **여러 AZ**에 등록된 모든 대상에 트래픽을 분산시켜 애플리케이션 복원력을 향상시킴.

5. **대상 그룹**(Target Group)  
NLB는 **대상 그룹**을 사용하여 지정된 프로토콜 및 포트 번호를 기반으로 등록된 대상으로 요청을 라우팅함.  
트래픽이 정상 대상으로만 라우팅되도록 대상 그룹에 대한 상태 확인을 구성할 수 있음.

6. **클라이언트 IP 보존**  
NLB는 클라이언트의 **원래 IP 주소를 보존**할 수 있으며 이는 클라이언트 IP 정보에 의존하는 애플리케이션에 유용.

NLB는 Elastic Load Balancing에서 제공하는 로드 밸런서 유형 중 하나일 뿐임.  
특정 요구 사항에 따라 **[Application Load Balancers](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-2.%20Application%20Load%20Balancer)**, **Gateway Load Balancers** 또는 [Classic Load Balancers](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-1.%20Classic%20Load%20Balancer(deprecated))와 같은 가장 적합한 로드 밸런서 유형을 선택할 수 있음.

### Layer

NLB는 **Transport Layer**(계층 4)에서 작동.  
이 계층은 송신자와 수신자 간의 논리적인 연결을 담당하며, **TCP와 UDP** 프로토콜을 사용하여 데이터를 전송.  
NLB는 IP 프로토콜 데이터를 기반으로 Amazon VPC 내의 대상으로 연결을 라우팅함.

### AZ 별 IP
NLB는 각 가용 영역 (Availability Zone, AZ)마다 **고정된 Private IP 주소**를 가지며, 이를 통해 트래픽을 분산.

### 요금
NLB는 실행된 시간과 처리된 데이터 양에 따라 요금이 부과됨.

### 프로토콜
NLB는 TCP 및 UDP 프로토콜을 지원. 이를 통해 다양한 유형의 트래픽을 처리할 수 있음.

### Target Group
NLB는 Target Group을 통해 연결된 대상을 관리함. 이를 통해 트래픽을 라우팅하고 상태 확인(Health Check)을 수행.

* **AWS Services**  
1. EC2 Instances
2. IP Address(Private IPs)
3. [Application Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-2.%20Application%20Load%20Balancer)

### Health Check
NLB는 대상 그룹에 등록된 대상의 상태를 모니터링하면서 상태가 양호한 대상으로만 트래픽을 라우팅함.

### Cross-Zone Load Balancing

* Disabled by Default
* 활성화 시, AZ 간 Load Balancing은 **유료**

## Architecture

![NLB Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/10c2567c-704c-4365-820a-53149ba28dc4)