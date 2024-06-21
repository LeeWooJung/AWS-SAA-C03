# CloudFront vs. Global Accelerator

AWS Global Accelerator와 Amazon CloudFront는 둘 다 AWS의 네트워크 서비스를 이용하여 애플리케이션의 성능을 최적화하고 가용성을 높이는 데 사용됨. 하지만 둘은 다른 목적과 기능을 제공함.

## 공통점

* **글로벌 서비스**  
    * 둘 다 전 세계에 걸친 AWS의 **글로벌 인프라를 사용**하여 트래픽을 전달하고, 사용자에게 최적의 응답 시간을 제공함.

* **Anycast IP**  
    * Global Accelerator와 CloudFront 모두 **Anycast IP 주소**를 사용하여 여러 위치에 걸쳐 트래픽을 분산함.  
    * 이를 통해 사용자 요청이 가장 가까운 엣지 로케이션으로 전달됨.

* **고가용성**  
    * 둘 다 **고가용성을 보장**하며, 여러 지리적 위치에 분산된 인프라를 사용하여 장애 시에도 트래픽이 자동으로 다른 경로를 통해 전달됨.

* **보안 통합**  
    * **AWS Shield와 통합**되어 DDoS 공격으로부터 보호됨.
    * IAM(Identity and Access Management)을 통해 리소스 접근을 제어함.

## 차이점

* **기본 목적**  
    * **Amazon CloudFront**  
        * 주로 **정적 및 동적 콘텐츠의 전송 속도를 최적화**하기 위한 CDN(Content Delivery Network) 서비스임.  
        * S3 버킷, EC2 인스턴스, HTTP 서버와 같은 다양한 소스에서 콘텐츠를 캐싱하여 사용자에게 빠르게 제공함.
    * **AWS Global Accelerator**  
        * 주로 **TCP 및 UDP** 트래픽의 성능 최적화 및 고가용성을 제공함.  
        * **정적 Anycast IP 주소**를 통해 사용자 트래픽을 글로벌 인프라로 전달하여 엔드포인트로 라우팅함.

* **콘텐츠 캐싱**  
    * **Amazon CloudFront**  
        * **캐시된 콘텐츠를 사용하여 사용자에게 빠른 응답을 제공**함.  
        * **TTL**(Time to Live) 설정을 통해 캐시 정책을 관리할 수 있음.
        * Contents는 Edge에서 serve됨.
    * **AWS Global Accelerator**  
        * **캐싱 기능이 없으며**, 대신 사용자 트래픽을 최적의 경로로 전달하여 성능을 최적화함.

* **트래픽 유형**  
    * **Amazon CloudFront**  
        * HTTP 및 HTTPS 트래픽을 최적화하며, 웹 사이트, 동영상 스트리밍, API 응답 속도 향상 등에 사용됨.
    * **AWS Global Accelerator**  
        * TCP 및 UDP 트래픽을 최적화함.  
        * 이는 주로 웹 애플리케이션, API 호출, 리얼타임 애플리케이션 등에 사용됨.

* **엔드포인트 유형**  
    * **Amazon CloudFront**  
        * S3 버킷, EC2 인스턴스, Elastic Load Balancing, HTTP 서버 등을 지원함.
    * **AWS Global Accelerator**  
        * Elastic IP, Network Load Balancer, Application Load Balancer, EC2 인스턴스 등 다양한 AWS 리소스를 지원함.

* **정적 IP 주소**  
    * **Amazon CloudFront**  
        * 특정 도메인 이름을 통해 콘텐츠를 전달하며, Anycast 네트워크를 통해 엣지 로케이션으로 트래픽을 분산함.
    * **AWS Global Accelerator**  
        * 두 개의 정적 Anycast IP 주소를 제공하여 트래픽을 분산시킴.

## Architecture Example

**Amazon CloudFront**  
* 사용자가 웹 사이트에 접속하면, CloudFront는 사용자의 위치에 가장 가까운 엣지 로케이션에서 콘텐츠를 제공함.  
* **캐시되지 않은 콘텐츠는 원본 서버(S3 버킷, EC2 인스턴스 등)에서 가져와 엣지 로케이션에 캐**시함.  
* 이후 동일한 콘텐츠 요청은 엣지 로케이션에서 바로 제공되어 응답 시간이 빨라짐.

**AWS Global Accelerator**  
* 사용자가 특정 애플리케이션에 접속하면, Global Accelerator는 사용자의 위치에 가장 가까운 엣지 로케이션으로 트래픽을 라우팅함.  
* 트래픽은 AWS 글로벌 네트워크를 통해 최적의 경로로 목적지(예: EC2 인스턴스, ALB, NLB)로 전달됨.
* 엔드포인트의 상태를 지속적으로 모니터링하여 비정상적인 경우 트래픽을 다른 정상 엔드포인트로 자동 전환함.