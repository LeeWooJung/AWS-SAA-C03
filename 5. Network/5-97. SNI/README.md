# SNI(Server Name Indication)

## SNI

### 설명

* **SNI**(Server Name Indication)는 **TLS**(Transport Layer Security) 프로토콜의 확장 기능으로, 하나의 IP 주소에서 **여러 도메인의 SSL/TLS 인증서를 지원**하기 위해 사용됨.
* SNI는 클라이언트가 서버에 연결할 때 어느 호스트 이름(도메인)에 접근하고자 하는지 **미리 서버에 알리는 기능을 제공**합니다. 이를 통해 서버는 적절한 SSL/TLS 인증서를 선택할 수 있음.

### Client 측에서의 SNI 작동 원리

1. **클라이언트 요청**
    - 클라이언트가 HTTPS를 통해 웹 서버에 연결을 시도할 때, 연결 초기 단계에서 TLS 핸드셰이크가 발생.
    - 클라이언트는 접속하려는 서버의 호스트 이름을 SNI 확장 필드를 통해 서버에 전달.

2. **서버 처리**
    - 서버는 SNI 확장 필드에 포함된 호스트 이름을 확인하고, 해당 호스트 이름에 맞는 SSL/TLS 인증서를 선택.
    - 서버가 선택한 인증서를 클라이언트에 제공하여 TLS 세션을 설정.

3. **암호화된 연결 설정**
    - TLS 핸드셰이크 과정이 완료되면, 클라이언트와 서버 간에 암호화된 통신이 시작.

### 중요성

1. **다중 호스팅 환경**  
SNI는 **하나의 서버에서 여러 도메인을 호스팅할 때 필수적**.  
하나의 IP 주소로 다수의 도메인을 지원하는 경우, SNI가 없다면 서버는 클라이언트가 어떤 도메인에 접근하려는지 알 수 없어 올바른 인증서를 제공할 수 없음.

2. **비용 절감**  
SNI를 사용하면 각 **도메인마다 별도의 IP 주소를 할당할 필요가 없어 IP 주소 자원을 절약**할 수 있음.  
이는 특히 IPv4 주소가 부족한 상황에서 중요.

3. **보안 강화**  
SNI를 통해 각 도메인마다 고유한 인증서를 사용할 수 있어, 개별 도메인에 대한 보안 관리가 용이.

### 요약

SNI는 클라이언트가 접속하려는 도메인을 서버에 알림으로써, **하나의 IP 주소에서 여러 도메인을 지원하는 서버 환경에서 올바른 SSL/TLS 인증서를 선택할 수 있도록 도와주는 중요한 기능**.  
이를 통해 다중 호스팅 환경, 비용 절감, 보안 강화 등의 장점을 제공함.  
대부분의 최신 클라이언트는 SNI를 지원하며, 이를 통해 사용자 경험을 향상시키고, 보안을 강화할 수 있음.

## [Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer)

### SNI with Load Balancer

1. **클라이언트 요청**  
    - 클라이언트가 HTTPS 요청을 보내기 위해 Load Balancer의 IP 주소와 포트(일반적으로 443)를 지정하여 연결을 시도.
    - TLS 핸드셰이크 초기 단계에서 클라이언트는 SNI 확장 필드를 사용하여 연결하려는 호스트 이름(도메인 이름)을 Load Balancer에 전달.

2. **Load Balancer의 SNI 처리**  
    - Load Balancer는 클라이언트로부터 받은 SNI 호스트 이름을 분석.
    - ALB나 NLB는 설정된 호스트 이름과 일치하는 인증서를 선택.

3. **인증서 선택 및 TLS 핸드셰이크**  
    - Load Balancer는 SNI에서 지정한 도메인 이름과 일치하는 SSL/TLS 인증서를 선택.
    - 올바른 인증서를 사용하여 TLS 핸드셰이크를 완료.  
    이 과정에서 클라이언트와 Load Balancer 간에 암호화된 통신 채널이 설정됨.

4. **트래픽 라우팅**  
    - TLS 핸드셰이크가 완료된 후, Load Balancer는 요청된 호스트 이름을 기반으로 트래픽을 백엔드 서버로 라우팅.
    - ALB의 경우, 호스트 기반 라우팅 또는 경로 기반 라우팅 규칙에 따라 요청을 적절한 대상 그룹(Target Group)으로 보냄.
    - NLB의 경우, 대상 그룹 내의 적절한 인스턴스나 IP 주소로 트래픽을 전달.

### CLB vs. ALB vs. NLB

1. **[CLB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-1.%20Classic%20Load%20Balancer(deprecated))**
    - SNI를 지원하지 않음.
2. **[ALB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-2.%20Application%20Load%20Balancer)**
    - SNI를 지원함.
3. **[NLB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer/5-2-3.%20Network%20Load%20Balancer)**
    - SNI를 지원함.