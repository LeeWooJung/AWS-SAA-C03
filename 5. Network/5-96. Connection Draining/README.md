# Connection Draining

## Connection Draining

### 설명

* **Connection Draining**  
1. 기존에 연결된 클라이언트 요청을 처리 완료할 수 있도록 하면서 백엔드 서버를 교체하거나 업데이트할 수 있는 기능.  
2. **Elastic Load Balancer**(ELB)에서 주로 사용.  
서버를 종료하거나 제거할 때 새로운 요청을 다른 서버로 전달하면서 기존 요청은 계속 처리할 수 있게 하여 사용자에게 서비스를 중단 없이 제공할 수 있도록 함.

### 주요 기능 및 작동 방식

1. **현재 활성된 연결 유지**  
    - 서버를 교체하거나 업데이트하기 위해 제거할 때, Connection Draining은 **기존에 활성된 연결이 있는 요청을 서버가 완료할 때까지 기다림**.
    - 새로운 요청은 더 이상 해당 서버로 전달되지 않고, 다른 활성 서버로 전달됨.

2. **타임 아웃**
    - Connection Draining에는 타임아웃을 설정할 수 있음(1~3600 sec).  
    이 타임아웃 기간 동안 서버가 요청을 완료하지 못하면 요청이 종료됨.
    - Default Time out: 300 sec.
    - 0 sec으로 설정 시, disabled 가능.

3. **Load Balancing**
    - Connection Draining이 활성화된 상태에서 서버를 교체하면, ELB는 **새로운 요청을 다른 가용한 서버로 분산시킴**.
    - 기존 요청이 완료될 때까지 ELB는 해당 서버와의 연결을 유지함.

## 중요성

1. **무중단 서비스 제공**  
유지보수, 업데이트 또는 서버 교체 시 서비스 중단을 최소화할 수 있음.

2. **사용자 경험 개선**  
클라이언트 요청이 갑자기 중단되지 않고, 서버 교체 시에도 안정적으로 서비스가 제공됨.

3. **운영 효율성 향상**  
서버를 점진적으로 제거하거나 교체하면서도 모든 클라이언트 요청을 처리할 수 있음.

**Connection Draining**은 고가용성 시스템을 설계하고 유지하는 데 매우 중요한 역할을 함.  
**ELB와 연계**하여 이 기능을 활용하면, 서비스를 중단 없이 유지보수하고 업데이트할 수 있음.

## Load Balancer

**Elastic Load Balancer** (ELB)는 Connection Draining을 통해 **높은 가용성과 무중단 서비스 제공을 지원**.  

1. Deregistration for **[ALB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-2.%20Application%20Load%20Balancer)**  
주로 **HTTP/HTTPS 트래픽**에 사용되며, Connection Draining을 통해 세션 기반의 연결 유지 및 클라이언트 요청 완료를 지원.
2. Deregistration for **[NLB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-3.%20Network%20Load%20Balancer)**  
높은 처리량과 저지연이 요구되는 **TCP 트래픽**에 사용되며, Connection Draining을 통해 기존 TCP 연결을 안정적으로 종료.
3. Connection Draining for **[CLB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-1.%20Classic%20Load%20Balancer(deprecated))**  
전통적인 ELB 유형으로, **HTTP/HTTPS 및 TCP 트래픽을 지원**하며 Connection Draining 기능을 포함.