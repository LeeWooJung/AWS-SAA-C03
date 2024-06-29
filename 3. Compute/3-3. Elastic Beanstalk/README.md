# [Elastic Beanstalk](https://aws.amazon.com/ko/elasticbeanstalk/?gclid=CjwKCAjwvIWzBhAlEiwAHHWgvTo_7t2fB17IG7otWlErbDhhivGfiQD5K90-JuWtCxszeRmvFFOFQhoCQGoQAvD_BwE&trk=3d211853-d899-491e-bd5a-fb5f17de6f0f&sc_channel=ps&ef_id=CjwKCAjwvIWzBhAlEiwAHHWgvTo_7t2fB17IG7otWlErbDhhivGfiQD5K90-JuWtCxszeRmvFFOFQhoCQGoQAvD_BwE:G:s&s_kwcid=AL!4422!3!651510175878!e!!g!!amazon%20elastic%20beanstalk!19835789747!147297563979)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/0f824b59-9a21-4c1f-b411-4de9befeccb4" width = "25" height = "25"> Elastic Beanstalk

### 정의 및 개념
* **Amazon Elastic Beanstalk**는 애플리케이션을 쉽고 빠르게 배포, 관리 및 확장할 수 있도록 돕는 플랫폼 서비스(**PaaS**).  
* 개발자가 **애플리케이션 코드를 업로드하면 Elastic Beanstalk는 필요한 인프라(서버, 네트워크, 로드 밸런서, 스토리지)를 자동으로 프로비저닝하고 애플리케이션을 배포**.

### 특징

* **자동 프로비저닝**  
필요한 인프라 리소스를 자동으로 설정하고 배포.
* **자동 스케일링**  
트래픽 패턴에 따라 인스턴스를 자동으로 스케일링.
* **통합 모니터링**  
애플리케이션 성능을 모니터링하고 로그를 수집.
* **다양한 프로그래밍 언어 지원**  
Java, .NET, PHP, Node.js, Python, Ruby, Go, Pcker Builder, Single Container/Multi-Container/Preconfigured Docker.
* **관리형 서비스**  
패치 적용, 백업, 유지보수 등의 작업을 관리형 서비스로 제공.

### 장단점

#### 장점

* **간편한 배포**  
개발자는 **애플리케이션 코드를 업로드하기만 하면** 나머지 작업은 Elastic Beanstalk가 처리.
* **자동화된 관리**  
인프라 관리 작업을 자동화하여 개발자가 애플리케이션 개발에 집중할 수 있음.
* **유연성**  
기본 설정을 사용하거나 직접 구성하여 원하는 방식으로 인프라를 관리할 수 있음.
* **비용 효율성**  
사용한 리소스에 대해서만 비용을 지불하며, 자동 스케일링을 통해 효율적으로 리소스를 사용할 수 있음.
* **통합 모니터링 및 로깅**  
Amazon CloudWatch를 통해 애플리케이션 성능을 모니터링하고 로그를 분석할 수 있음.

#### 단점

* **제한된 제어**  
완전한 인프라 제어가 필요한 경우 Elastic Beanstalk의 자동화된 관리 기능이 제한적일 수 있음.
* **복잡성**  
대규모 애플리케이션이나 특정 요구사항이 있는 경우 설정 및 관리가 복잡해질 수 있음.
* **비용 관리**  
자동 스케일링이 잘못 설정되면 예상치 못한 비용이 발생할 수 있음.

### 아키텍처
Elastic Beanstalk의 아키텍처는 다음과 같은 주요 구성 요소로 이루어져 있음

* **환경**(Environment)  
애플리케이션을 배포하고 실행하는 독립된 인프라 세트.
* **애플리케이션**(Application)  
Elastic Beanstalk에서 관리되는 코드, 설정, 인프라 구성 요소들의 집합.
* **애플리케이션 버전**(Application Version)  
애플리케이션의 특정 버전으로, Amazon S3에 저장된 **소스 코드 배포 패키지**.
* **환경 구성**(Environment Configuration)  
애플리케이션을 실행하기 위한 구성 설정으로 티어,  인스턴스 유형, 스케일링 정책, 로드 밸런서 설정 등을 포함.

### Tier

Amazon Elastic Beanstalk의 환경(environments) 구성 요소 중에서 tiers는 애플리케이션이 실행될 환경의 유형을 정의하는 중요한 개념.

1. **Web Server Environment Tier** (웹 서버 환경 티어)
    * **목적**  
    주로 웹 애플리케이션을 호스팅하는 데 사용.
    * **기능**  
    HTTP/HTTPS 요청을 처리하고, 사용자와의 상호작용을 관리.
    * **구성 요소**  
        * **EC2 인스턴스**  
        애플리케이션 코드가 실행되는 서버 인스턴스.
        * **로드 밸런서**  
        트래픽을 여러 EC2 인스턴스에 분산시켜 애플리케이션의 가용성과 확장성을 높임.
        * **오토스케일링 그룹**  
        트래픽에 따라 EC2 인스턴스의 수를 자동으로 조정.
        * **보안 그룹**  
        인스턴스의 네트워크 트래픽을 제어하여 보안을 강화.
    * **사용 사례**  
    웹 사이트, 웹 애플리케이션, RESTful API 서버 등.
2. **Worker Environment Tier** (워크 환경 티어)
    * **목적**  
    백그라운드 작업이나 비동기 작업 처리를 위한 환경.
    * **기능**  
    메시지 큐(SQS)에서 메시지를 수신하여 작업을 처리.
    * **구성 요소**  
        * **EC2 인스턴스**  
        작업이 실행되는 서버 인스턴스.
        * **SQS** (Simple Queue Service)  
        작업 요청을 큐로 받아들이고 이를 처리할 수 있도록 함.
        * **오토스케일링 그룹**  
        작업량에 따라 EC2 인스턴스의 수를 자동으로 조정.
        * **IAM 역할**  
        SQS 큐와 상호작용하기 위한 권한을 관리.
    * **사용 사례**  
    데이터 처리, 이미지 변환, 이메일 처리, 비디오 트랜스코딩 등 백그라운드 작업.

Elastic Beanstalk는 이러한 구성 요소들을 조합하여 애플리케이션을 자동으로 배포하고, 필요에 따라 인프라를 확장하거나 축소함.

### Use Case

* **웹 애플리케이션**  
Django, Flask, Express, Spring 등의 웹 프레임워크를 사용하는 웹 애플리케이션.
* **API 서버**  
RESTful API 또는 GraphQL API 서버 배포.
* **마이크로서비스**  
각 마이크로서비스를 독립적으로 배포하고 관리.
* **백엔드 서비스**  
모바일 애플리케이션 백엔드, 데이터 처리 워크로드 등.

## Web Server Tier Architecture

![web server tier architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/2721e401-f634-43bc-a243-6e7b5fdec3ee)

## Worker Server Tier Architecture

![worker server tier architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/53e5229e-e01d-47f4-a3c5-b49a86b7f742)


## Summary

Elastic Beanstalk는 개발자가 애플리케이션 코드 작성에 집중하고, 인프라 관리 작업을 최소화할 수 있도록 도와줌.  
자동화된 관리 기능과 다양한 프로그래밍 언어 지원을 통해 빠르고 유연하게 애플리케이션을 배포하고 운영할 수 있음.