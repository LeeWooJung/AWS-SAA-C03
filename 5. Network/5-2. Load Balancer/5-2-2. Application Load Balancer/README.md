# [Application Load Balancer](https://docs.aws.amazon.com/ko_kr/elasticloadbalancing/latest/application/introduction.html)

## Application Load Balancer    

ALB(Application Load Balancer)는 애플리케이션 계층의 여러 대상에 수신 트래픽을 분산시키는 Amazon Web Services(AWS)에서 제공하는 서비스임.

* **Load Balancing**  
ALB는 다양한 가용 영역에 있는 여러 대상(예: EC2 인스턴스, 컨테이너 또는 IP 주소)에 걸쳐 트래픽을 자동으로 밸런싱함.  
이를 통해 애플리케이션 가용성이 향상되고 정상적인 대상이 트래픽을 수신할 수 있음.

* **리스너 규칙**  
ALB에 하나 이상의 리스너를 구성할 수 있음. 리스너는 **구성된 프로토콜과 포트를 기반으로 들어오는 연결 요청을 확인**.  
리스너 규칙은 ALB가 요청을 **등록된 대상으로 라우팅하는 방법을 결정**.  
각 규칙은 우선 순위, 하나 이상의 작업 및 조건으로 구성됨.

* **대상 그룹**(Target Group): 대상(예: EC2 인스턴스)은 **지정된 프로토콜 및 포트 번호**를 기반으로 그룹화됨. 여러 대상 그룹에 대상을 등록할 수 있음. 상태 점검은 대상 그룹 수준에서 구성할 수 있음.

* **라우팅 알고리즘**: ALB는 다양한 라우팅 알고리즘을 지원함. 기본적으로 **라운드 로빈 라우팅**을 사용하지만 **최소 미해결 요청**을 알고리즘으로 지정할 수도 있음. 이를 통해 ALB는 각 대상 그룹에 대해 독립적으로 요청을 라우팅할 수 있음.

* **고급 기능**: ALB는 상호 TLS, HTTP/2, gRPC, TLS 오프로딩, 고정 세션 등과 같은 기능을 지원함. OSI 모델의 애플리케이션 계층(**7계층**)에서 작동.

## Routing

**AWS Application Load Balancer**(ALB)은 여러 타겟 그룹을 사용하여 라우팅 테이블을 구성할 수 있음. 각 타겟 그룹은 하나 이상의 등록된 타겟으로 요청을 라우팅함.  
Health Check는 Target Group Level에서 진행 됨.

### 예시

1. 일반 요청과 마이크로서비스 요청 분리  
애플리케이션의 **일반 요청**과 **마이크로서비스 요청**을 분리하려면 각각 다른 타겟 그룹을 생성. 일반 요청을 처리하는 타겟 그룹과 마이크로서비스를 위한 타겟 그룹을 만들어서 요청을 분리함.

2. 서브도메인별 타겟 그룹 설정  
서브도메인마다 다른 타겟 그룹을 사용하려면 **리스너 규칙을 설정**. 예를 들어, staging.example.com 서브도메인은 특정 타겟 그룹으로 라우팅되도록 리스너 규칙을 설정할 수 있음.

3. 가중치를 사용한 타겟 그룹 설정  
**가중치**를 사용하여 특정 타겟 그룹에 더 많은 트래픽을 라우팅하려면 리스너 규칙에서 가중치를 설정

4. URL 경로 기반 라우팅  
**URL 경로**를 기준으로 요청을 특정 타겟 그룹으로 라우팅. 예를 들어, /api 경로의 요청은 API 서비스를 처리하는 타겟 그룹으로 전달될 수 있음.

5. 호스트명 기반 라우팅  
**호스트명을 기준**으로 요청을 다른 타겟 그룹으로 라우팅합니다. 예를 들어, api.example.com 도메인은 API 서비스를 처리하는 타겟 그룹으로 라우팅될 수 있음.

6. QueryString 기반 라우팅  
**URL의 QueryString 매개변수**를 기준으로 요청을 다른 타겟 그룹으로 라우팅합니다. 예를 들어, ?version=2 매개변수가 있는 요청은 버전 2를 처리하는 타겟 그룹으로 전달될 수 있음.

### Routing to AWS Services

1. **Amazon EC2 인스턴스**  
가장 일반적인 타겟으로 EC2 인스턴스를 등록할 수 있음(HTTP). 이는 애플리케이션 서버, 웹 서버, 데이터베이스 서버 등을 포함. Auto Scaling Group에 의해 관리 될 수 있음.

2. **ECS** (Elastic Container Service) 서비스  
컨테이너화된 애플리케이션을 실행하는 ECS 서비스를 타겟으로 등록할 수 있음(HTTP).

3. **Lambda 함수**  
Lambda 함수를 타겟으로 등록하여 서버리스 아키텍처에서 요청을 처리할 수 있음. HTTP 요청이 JSON Event로 번역됨.

4. **IP 주소**  
특정 IP 주소를 타겟으로 등록하여 직접 트래픽을 라우팅할 수 있음.

5. **Network Load Balancer** (NLB)  
다른 NLB를 타겟으로 등록하여 라우팅할 수 있음.

## Architecture

![alb architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/4076f6d0-edc1-45f1-a431-9d27107fb7cb)

## Architecture with target group

![alb architecture with target group](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/30af2ce3-f5c9-4560-8984-155c388dd05e)
