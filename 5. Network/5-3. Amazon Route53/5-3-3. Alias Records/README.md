# Alias Records

## Alias Records

### 설명

* AWS Route 53에서 **Alias Records**는 특정 AWS 리소스와 연결되는 특별한 유형의 DNS 레코드.  
* 일반적인 CNAME 레코드와 유사하지만, 몇 가지 중요한 **차이점**이 있음.  
* Alias Records는 주로 **AWS 서비스와의 통합을 위해 사용되며, 비용 효율성, 성능, 편의성을 제공**함.
* **TTL**을 설정할 수 없음.

### 특징

1. **AWS 서비스와의 통합**  
    * Alias Records는 AWS 서비스의 도메인 이름 대신 IP 주소를 반환.
    * AWS 서비스에 대한 Alias Records를 쉽게 설정할 수 있으며, Route 53은 해당 서비스의 현재 IP 주소를 자동으로 반환.
    * 항상 **A/AAAA** Type (IPv4/IPv6) 임.
    * 주요 통합 대상  
        * Amazon S3 버킷  
        * Amazon CloudFront 배포  
        * AWS Elastic Load Balancer (ELB)  
        * Amazon API Gateway  
        * AWS Global Accelerator  
        * Route 53 호스티드 존  
        * CloudFront  
        * Elastic Beanstalk env  
        * VPC Interface Endpoints
        * **EC2 DNS Name**은 불가능.

2. **비용 효율성**  
    * **Alias Records는 DNS 쿼리당 요금을 부과하지 않음**.  
    * 일반적인 CNAME 레코드는 쿼리당 요금을 부과할 수 있지만, Alias Records는 무료로 제공.

3. **루트 도메인 지원**  
    * Alias Records는 **루트 도메인(root domain)에서 사용**할 수 있음.  
    * 예를 들어, "example.com"을 "www.example.com"으로 **리디렉션**할 수 있음.
    * **CNAME 레코드는 루트 도메인에서 사용할 수 없지만**, Alias Records는 이를 가능하게 함.

4. **자동 갱신**  
    * AWS 서비스의 IP 주소가 변경되더라도, Alias Records는 **자동으로 최신 IP 주소를 반환**.  
    * 수동으로 업데이트할 필요가 없음.

### 작동 방식

* Alias Records는 AWS 서비스의 DNS 네임 서버와 통합.  
* 예를 들어, **Amazon S3**에 호스팅된 정적 웹사이트를 가리키는 Alias Record를 설정할 수 있음.  
* Route 53은 S3 버킷의 현재 IP 주소를 조회하여 클라이언트에게 반환함.

#### 예시

* **S3 버킷과의 통합**  
    * 정적 웹사이트를 호스팅하는 Amazon S3 버킷.
    * 도메인 이름 "example.com"을 S3 버킷으로 리디렉션하기 위해 Alias Record를 생성.

* **CloudFront 배포와의 통합**  
    * CloudFront 배포를 통해 콘텐츠를 배포.
    * 도메인 이름 "cdn.example.com"을 CloudFront 배포로 리디렉션하기 위해 Alias Record를 생성.

* **Elastic Load Balancer (ELB)와의 통합**  
    * 애플리케이션을 여러 인스턴스에 걸쳐 로드 밸런싱하는 ELB.
    * 도메인 이름 "app.example.com"을 ELB로 리디렉션하기 위해 Alias Record를 생성.

## Alias Records vs CNAME

* **CNAME**  
    * 도메인 이름을 다른 도메인 이름으로 리디렉션.
    * **루트 도메인에서 사용할 수 없음**.

* **Alias Records**
    * AWS 리소스와 통합되어 IP 주소를 반환.
    * **루트 도메인에서 사용할 수 있음**.

## Summary

* Alias Records는 **AWS 서비스와의 통합을 단순화**하고, **루트 도메인에서 사용할 수 있으며**, **비용 효율적**이고, 자동으로 업데이트되는 장점을 제공.  
* 이러한 특징은 특히 AWS 기반 애플리케이션의 DNS 설정을 최적화하는 데 매우 유용함.