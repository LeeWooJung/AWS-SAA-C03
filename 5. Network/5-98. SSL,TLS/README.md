# SSL & TLS

* 웹 통신의 보안을 위해 설계된 암호화 프로토콜.
* 데이터를 암호화하고, 서버와 클라이언트의 인증을 제공하여 안전한 데이터 전송 채널을 구축함.
* 대칭키 암호화와 비대칭키 암호화를 결합하여 사용하며, 안전한 통신을 제공함. 
* SSL/TLS는 웹 사이트의 원본 서버에 설치된 SSL 인증서를 사용하여 트래픽을 암호화함.

## SSL(Secure Socket Layer)

### 설명

* 사용자와 웹 브라우저 간 통신을 암호화하는데 사용됨.
* SSL 인증서를 통해 상호간의 암호화 통신을 만들어냄.
* 인증서에 포함된 웹 서버의 **공개키**를 바탕으로 **상호간의 키 교환/공유**를 통해 암호화 통신을 이끌어냄.
* SSL 인증서는 **제 3의 신뢰 기관에서 인증을 받아 만들어짐**.
* 전자 상거래와 같은 웹 보안이 중요한 분야에서 많이 사용됨.
* 만기(expiration date)가 있음.

## TLS(Transport Layer Security)

### 설명

* SSL에서 개선된 신규 모델 프로토콜.
* SSL과 유사한 방식으로 동작하며, 상호간의 통신을 암호화함.
* TLSv1.3은 최신 버전으로, 보안성과 효율성을 높임.
* 만기(expiration date)가 있음.

## [Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer)

### Load Balancer에서 SSL 사용

1. **SSL 인증서 생성 및 관리**  
    - AWS Certificate Manager(ACM)을 사용하여 SSL/TLS 인증서를 생성.
    - ACM에서 인증서를 관리하고 자동으로 갱신.

2. **로드 밸런서 구성**
    - ALB 또는 NLB를 생성하고, **리스너**를 추가.
    - 리스너는 포트와 프로토콜을 정의하며, SSL/TLS 종료를 설정.

3. **대상 그룹 설정**
    - 대상 그룹을 생성하고, EC2 인스턴스 또는 컨테이너를 대상으로 추가.
    - 로드 밸런서는 대상 그룹에 트래픽을 분산.

4. **보안 그룹 및 네트워크 구성**
    - 로드 밸런서와 대상 그룹의 보안 그룹을 구성하여 필요한 포트를 열고 보안을 강화.

### ALB vs. NLB vs. CLB

1. **[ALB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-2.%20Application%20Load%20Balancer)**
    - HTTP/HTTPS(SSL) 트래픽을 처리.
    - Layer 7에서 작동하며, URL 기반 라우팅, 호스트 기반 라우팅, SSL 종료, 클라이언트 인증 등을 지원.
    - 웹 애플리케이션에 적합.
    - 다수의 SSL certificate를 가지는 다수의 listener를 지원.

2. **[NLB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-3.%20Network%20Load%20Balancer)**
    - TCP, UDP, TLS 트래픽을 처리.
    - Layer 4에서 작동하며, 고성능, 고가용성, 정적 IP 주소를 제공.
    - 빠른 속도와 대규모 트래픽 처리에 적합.
    - 다수의 SSL certificate를 가지는 다수의 listener를 지원.

3. **[CLB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-1.%20Classic%20Load%20Balancer(deprecated))**
    - 오직 하나의 SSL certificate만 지원.
    - 다수의 SSL certificate를 가지는 여러 hostname을 사용하기 위해서는 다수의 CLB를 사용해야 함.

## HTTPS Listener

1. **개요**  
HTTPS 리스너는 SSL/TLS 프로토콜을 사용하여 클라이언트와 로드 밸런서 간의 트래픽을 암호화함.  
로드 밸런서는 클라이언트와의 연결을 처리하고, 이후 백엔드 서버와의 통신을 위해 다른 연결을 설정함.  
이 과정에서 SSL/TLS 인증서를 사용하여 보안을 강화함.

2. **구성요소**  
    - **리스너(Listener)**  
리스너는 로드 밸런서에서 수신하는 요청을 처리하는 구성 요소.  
리스너는 특정 포트(예: 443)에서 수신 대기하며, 수신된 요청을 백엔드 서버로 라우팅.  
HTTPS 리스너의 경우, 로드 밸런서는 클라이언트와의 트래픽을 암호화하기 위해 SSL/TLS 인증서를 사용함.
    - **SSL/TLS 인증서**  
HTTPS 리스너를 설정하려면 유효한 SSL/TLS 인증서가 필요.  
AWS에서는 **ACM**(AWS Certificate Manager)을 통해 인증서를 관리할 수 있음.  
인증서를 사용하여 클라이언트와의 연결을 암호화하고, 데이터의 무결성과 기밀성을 보장.
    - **리스너 규칙**(Listener Rules)  
리스너 규칙은 **수신한 요청을 어떻게 처리할지 정의**.  
규칙에는 조건과 작업이 포함됨. 예를 들어, 특정 경로 또는 호스트 헤더를 기반으로 트래픽을 특정 대상 그룹(Target Group)으로 라우팅할 수 있음.
    - **대상 그룹(Target Group)**  
대상 그룹은 트래픽을 수신할 백엔드 서버의 집합. 로드 밸런서는 리스너 규칙에 따라 트래픽을 대상 그룹으로 라우팅함.  
각 대상 그룹은 특정 프로토콜(예: HTTP, HTTPS)과 포트를 사용하여 구성.

## Architecture

![SSL architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/c4a797c2-e5c7-49a7-8d6a-f5afa04da55e)
