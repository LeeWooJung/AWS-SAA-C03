# [CloudFront Origins](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/DownloadDistS3AndCustomOrigins.html)

* AWS CloudFront의 오리진(Origin)은 CloudFront 배포에 콘텐츠를 제공하는 소스임.  
* CloudFront는 두 가지 유형의 오리진을 지원.

## [S3 Bucket](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3)

Amazon S3 버킷을 CloudFront의 오리진으로 사용할 때, **정적 콘텐츠**(예: 이미지, 동영상, HTML 파일)를 저장하고 사용자에게 배포할 수 있음.

### 특징

* **정적 파일 배포**  
    * S3는 **정적 파일을 저장하고 제공하는 데 최적화**되어 있음.  
    * CloudFront와 결합하면, 전 세계적으로 빠르고 안정적으로 콘텐츠를 배포할 수 있음.
    * **보안**  
        * S3 버킷에 대한 액세스를 제어할 수 있음.  
        * CloudFront **오리진 액세스 제어**([OAC](https://aws.amazon.com/ko/blogs/korea/amazon-cloudfront-introduces-origin-access-control-oac/))를 사용하여 S3 버킷을 보호하고, CloudFront를 통해서만 버킷에 접근할 수 있도록 설정할 수 있음.
    * **버전 관리**  
        * S3 버킷의 객체 버전 관리를 통해 콘텐츠의 변경 내역을 추적하고 복원할 수 있음.
    * **비용 효율성**  
        * S3는 사용한 만큼 비용을 지불하는 모델로, **대용량 데이터를 효율적으로 저장하고 배포**할 수 있음.

## 커스텀 오리진(HTTP 서버)

커스텀 오리진은 HTTP 서버(예: **Amazon EC2 인스턴스, 온프레미스 서버, Application Load Balancer, S3 Website, 다른 클라우드 제공자의 서버**)를 CloudFront의 오리진으로 사용하는 것임.

### 특징

* **동적 콘텐츠**  
        * 커스텀 오리진을 사용하면 **동적 콘텐츠**(예: API 응답, 데이터베이스 조회 결과)를 배포할 수 있음.
    * **유연성**  
        * HTTP 서버를 오리진으로 사용하면, **다양한 애플리케이션과 기술 스택을 지원**할 수 있음.
    * **보안**  
        * HTTPS를 통해 콘텐츠를 전송하여 데이터의 무결성과 기밀성을 보호할 수 있음.  
        * 또한, **AWS WAF**를 통해 웹 애플리케이션 방화벽 규칙을 적용할 수 있음.
    * **로드 밸런싱**  
        * Elastic Load Balancing(ELB)과 함께 사용하여 트래픽을 여러 서버에 분산시킬 수 있음.

## Summary

* S3 버킷을 오리진으로 사용하면 **정적 파일**을 효율적으로 배포할 수 있으며, 커스텀 오리진을 사용하면 **동적 콘텐츠와 다양한 서버 애플리케이션을 배포**할 수 있음.  
* 두 오리진 유형 모두 CloudFront의 글로벌 네트워크를 활용하여 콘텐츠를 빠르고 안전하게 제공하는 데 중점을 둠.  
* 선택한 오리진 유형에 따라 설정과 관리 방식이 다르므로, 사용 사례에 맞는 오리진을 선택하여 최적의 성능과 보안을 달성해야 함.

