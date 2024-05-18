# [Classic Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/introduction.html)

## Classic Load Balancer    

* 기본적인 로드 밸런싱을 제공하는 AWS 서비스입니다.  
* 연결 수준과 요청 수준에서 작동하며, 여러 Amazon EC2 인스턴스 간의 기본적인 부하 분산을 수행함.

### Layer 
**Classic Load Balancer**는 OSI 모델의 **Layer 4**(전송 계층, TCP)와 **Layer 7**(응용 계층, HTTP & HTTPS)에서 작동.  
이는 IP 주소, 포트, 프로토콜 및 내용을 기반으로 트래픽을 분산할 수 있음을 의미.

### Health Check
**Classic Load Balancer**는 등록된 대상의 상태를 모니터링(TCP or HTTP Based)하고, 트래픽을 오직 건강한 대상으로만 보냄.

아키텍처: Classic Load Balancer는 여러 Availability Zone에서 여러 EC2 인스턴스에 들어오는 애플리케이션 트래픽을 분산시킵니다. 이로써 애플리케이션의 내결함성을 높입니다1.
Classic Load Balancer는 기본적인 로드 밸런싱을 제공하며, EC2 인스턴스를 추가하거나 제거하여 애플리케이션의 요청 흐름을 방해하지 않고 필요에 따라 확장할 수 있습니다

### 장단점

#### 장점

1. 간단한 설정  
CLB는 간편하게 설정할 수 있으며, 기본적인 로드 밸런싱을 제공.
2. 고가용성  
여러 Availability Zone에서 인스턴스를 분산하여 고가용성을 확보함.  
3. 부하 분산  
트래픽을 여러 인스턴스에 분산하여 성능을 향상시킴.

#### 단점

1. 제한된 기능  
CLB는 기본적인 로드 밸런싱만 지원하며, 고급 기능은 제공하지 않음.
2. 스케일링 한계  
대규모 애플리케이션에는 부적합할 수 있음.
3. SSL 처리 부담  
SSL 암복호화를 처리하는 데 부담이 있을 수 있음.
4. Cross Load Balancing  
Default로 설정되어 있지 않아, Enable 후 설정해야 진행할 수 있음.  
