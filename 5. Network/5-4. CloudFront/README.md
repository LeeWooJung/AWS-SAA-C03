# [CloudFront](https://aws.amazon.com/ko/cloudfront/)

## <img src = "https://github.com/LeeWooJung/baekjoon/assets/31682438/7dc7fb7e-7fac-4b10-8b97-cb1006bb7cc9" width = "30" height = "30"> CloudFront

* **Amazon CloudFront**는 AWS의 글로벌 콘텐츠 전송 네트워크(Content Delivery Network, **CDN**) 서비스로, 웹 사이트, 애플리케이션, 동영상, API 등의 콘텐츠를 전 세계 사용자에게 더 빠르고 안전하게 전달함.  
* CloudFront는 AWS의 다른 서비스와 긴밀하게 통합되어, 개발자와 기업이 **콘텐츠 배포를 쉽게 관리하고 최적화**할 수 있게 함.

### 역할

* **빠른 콘텐츠 전달**  
글로벌 네트워크의 엣지 로케이션을 사용해 사용자와 가까운 위치에서 콘텐츠를 제공함으로써 **지연 시간을 최소화**함.
* **보안 강화**  
**DDoS 방어, SSL/TLS 암호화, AWS WAF**(Web Application Firewall)와 통합하여 콘텐츠 전송의 보안을 강화함.
* **확장성 및 고가용성**  
전 세계적으로 분산된 인프라를 사용하여 트래픽 급증 시에도 안정적인 성능을 제공함.
* **비용 효율성**  
사용량 기반의 과금 모델을 통해 필요한 만큼만 비용을 지불하게 함.

### 아키텍처

CloudFront의 아키텍처는 다음과 같은 주요 구성 요소로 이루어짐

* **엣지 로케이션**(Edge Locations)  
전 세계에 분산된 데이터 센터로, **콘텐츠를 캐시하여 사용자에게 더 가까운 위치에서 콘텐츠를 제공**함.
* **오리진 서버**(Origin Servers)  
**원본 콘텐츠가 저장된 서버**로, Amazon S3 버킷, HTTP 서버, Elastic Load Balancer 등이 포함될 수 있음.
* **배포(Distribution)**  
CloudFront를 통해 **콘텐츠를 제공하기 위해 설정된 구성**으로, 웹 배포(Web Distribution)와 RTMP 배포(Real-Time Messaging Protocol Distribution) 두 가지 유형이 있음.
* **캐싱 및 TTL(Time to Live)**  
엣지 로케이션에서 콘텐츠를 **얼마나 오랫동안 캐시할지를 결정하는 설정**으로, TTL 값을 통해 캐시 만료 시간을 제어할 수 있음.

## CloudFront vs. S3 Cross Region Replication

Amazon CloudFront와 Amazon S3 Cross Region Replication는 모두 콘텐츠 전달과 관련된 AWS 서비스이지만, 각각의 목적과 기능은 다름.

### 목적

* **CloudFront**  
전 세계 사용자에게 빠르고 안전하게 콘텐츠를 전달하기 위한 CDN 서비스.
* **S3 Cross Region Replication**  
S3 버킷 간 데이터를 자동으로 복제하여 다른 리전에서 데이터의 가용성과 내구성을 높이기 위한 서비스.

### 기능

* **CloudFront**  
    * 글로벌 엣지 로케이션을 통해 콘텐츠를 캐시하고, 사용자와 가장 가까운 엣지 로케이션에서 콘텐츠를 제공하여 지연 시간을 줄임.
    * Cached 된 파일은 TTL동안 유지됨.
    * 전 세계 각지에 사용될 정적 컨텐츠를 배포하기 유리함.
* **S3 Cross Region Replication**  
    * S3 버킷 간 객체를 자동으로 복제하여 재해 복구, 데이터 이행, 규정 준수 등의 목적을 달성함.
    * Replication을 진행할 각 Region에 설치 되어야 함.
    * Read Only
    * 적은 Region에 빠르게 접근할 수 있는 **동적** 컨텐츠에 유리함.

### 사례

* **CloudFront**  
웹 사이트, 동영상 스트리밍, API, 소프트웨어 배포 등 사용자에게 빠르고 효율적인 콘텐츠 전달이 필요한 경우.
* **S3 Cross Region Replication**  
데이터 백업, 재해 복구, 규정 준수, 글로벌 애플리케이션의 데이터 동기화 등 데이터의 가용성과 내구성을 보장해야 하는 경우.

### Summary

* Amazon CloudFront는 **AWS의 CDN 서비스**로, 전 세계 사용자에게 콘텐츠를 빠르고 안전하게 전달하는 데 중점을 둠. 
* CloudFront의 글로벌 네트워크, 보안 기능, 확장성 및 고가용성은 사용자 경험을 최적화하는 데 중요한 역할을 함.  
* 반면, Amazon S3 Cross Region Replication은 **S3 버킷 간 데이터 복제를 통해 데이터 가용성과 내구성을 높이는 데 중점**을 둠.  
* 이 두 서비스는 서로 보완적이지만, 각각의 고유한 목적과 기능을 이해하고 사용해야 함.

## Architecture Example

### Basic Architecture

![Basic Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/881e9f7e-62c7-4e25-a8e8-23b2bd06c3c9)

### S3 as an Origin

![S3 as an Origin](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/49df12e2-52db-4075-9552-2ba4aa2ca6c8)
