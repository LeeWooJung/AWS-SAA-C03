# Integration with API Gateway

Amazon Certificate Manager (ACM)를 사용하여 API Gateway와 통합하면, **SSL/TLS 인증서를 손쉽게 관리**할 수 있으며, **HTTPS를 통해 API 트래픽을 보호**할 수 있음. 

이를 통해 **사용자는 신뢰할 수 있는 HTTPS 엔드포인트를 통해 API를 호출**할 수 있음.

### ACM 인증서

ACM을 사용하여 **SSL/TLS 인증서를 생성, 관리 및 배포**함. 

API Gateway와 통합하여 **HTTPS 엔드포인트를 설정**할 수 있음.

### API Gateway

**RESTful APIs를 구축, 배포 및 관리할 수 있는 AWS 서비스**임. 

HTTPS를 통해 API를 보호하기 위해 ACM 인증서를 사용할 수 있음.

[API Gateway Endpoint Type](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-7.%20AWS%20API%20Gateway/8-7-1.%20Endpoint%20Types) 중에 **Edge-Optimized**와 **Regional** Endpoint와 결합될 수 있음.

## ACM과 API Gateway 통합 방법

### ACM에서 인증서 생성

AWS Management Console에서 ACM으로 이동함.

"Request a certificate"를 선택하고, **도메인 이름을 입력하여 인증서를 요청**함.

인증 과정을 완료하여 인증서를 발급받음.

### API Gateway 설정

AWS Management Console에서 API Gateway로 이동함.

**새로운 API를 생성하거나 기존 API를 선택**함.

* **Custom Domain Name 설정**

    "Custom Domain Names"를 선택하고 "Create"를 클릭함.

    **도메인 이름을 입력하고, ACM에서 발급받은 인증서를 선택**함.

    "Endpoint Configuration"에서 Edge-Optimized 또는 Regional을 선택함.

* **API Mapping 설정**

    "API Mappings"에서 생성한 도메인을 API Gateway 엔드포인트에 매핑함.

    API 스테이지를 선택하여 도메인과 연결함.

## With Edge-Opimized Endpoint

Global Clients에게 서비스를 제공할 때 사용함.

사용자의 요청은 **CloudFront Edge Locations**를 통해 라우트 되어 지연시간을 줄임.

**API Gateway**는 오직 **하나의 Region**에 있음.

**TLS Certificate**는 CloudFront와 같이 **US-EAST-1** Region에 존재해야 함

그 후, CNAME 혹은 A-Alias Record가 Route53에서 정의되어야 함.

## With Regional

같은 Region에 있는 Clients에게 서비스를 제공할 때 사용함.

API Stage와 **같은 Region에 존재하는 API Gateway에서 TLS Certificate가 Import** 되어야 함.

그 후, CNAME 혹은 A-Alias Record가 Route53에서 정의되어야 함.

## Architecture Example

![integration with api gateway](https://github.com/user-attachments/assets/5f5b66bb-1b7a-40f0-bab7-6e1a3ff5744c)