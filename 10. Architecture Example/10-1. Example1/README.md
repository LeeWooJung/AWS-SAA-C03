# Example 1

## 요구 사항

다음 요구 사항을 만족하는 모바일 애플리케이션의 아키텍처.

* HTTPS를 사용하여 REST API로 노출
* 서버리스 아키텍처
* 사용자는 S3에 있는 자신의 폴더와 직접 상호 작용할 수 있어야 함.
* 사용자는 관리형 서버리스 서비스를 통해 인증해야 함.
* 사용자는 to-tods에 쓰기 및 읽기가 가능하지만 대부분 읽기를 사용.
* 데이터베이스는 확장성이 있어야 하며 읽기 처리량이 높아야 함.

## 아키텍처 구성

### AWS API Gateway

* REST API를 **HTTPS로 노출**하기 위해 사용함.

* **API Gateway는 서버리스로 운영**되며, 요청을 **AWS Lambda로 라우팅**해줌.

* 인증 및 권한 부여를 **Amazon Cognito와 통합**할 수 있음.

### AWS Lambda

* 비즈니스 로직을 처리하기 위한 **서버리스 컴퓨팅 서비스**임.

* API Gateway와 통합되어 **각 요청에 대해 필요한 Lambda 함수를 호출**함.

* Lambda 함수는 **데이터베이스와 상호작용하며, S3 버킷에 대한 접근을 처리**함.

### Amazon S3

* 사용자들이 자신의 폴더에 직접 접근할 수 있도록 함.

* 각 사용자는 **IAM 정책을 통해 자신의 폴더에 대한 읽기/쓰기 권한을 부여**받음.

* S3 버킷을 사용하여 사용자 데이터(예: to-dos)를 저장함.

### Amazon Cognito

* 사용자 인증 및 관리 서비스를 제공함.

* 사용자는 **Cognito를 통해 로그인하고 인증을 받음**.

* 인증된 사용자는 자신만의 S3 폴더에 접근할 수 있음.

### Amazon DynamoDB

* 고성능, 확장 가능한 NoSQL 데이터베이스임.

* 높은 읽기 처리량을 제공하여 사용자가 주로 데이터를 읽는 작업에 적합함.

* Lambda 함수와 통합되어 to-dos 데이터를 저장 및 조회함.

## 아키텍처

![example1 architecture1](https://github.com/user-attachments/assets/2fe4cd20-a364-4947-9843-d6fd9faeb695)

### 읽기 처리량을 더 늘리기 위한 방법

* **Amazon DynamoDB Accelerator** (DAX)
    
    Amazon DynamoDB Accelerator (DAX)는 DynamoDB에 대해 **완전 관리형 인메모리 캐시**를 제공하여 읽기 처리량을 대폭 향상시킬 수 있음.

    DAX는 캐시 히트율을 높여 읽기 성능을 최대 10배까지 향상시킬 수 있음.

    **애플리케이션에서 변경할 코드가 거의 없으므로, 기존 DynamoDB 쿼리와 호환성을 유지**하면서 성능을 개선할 수 있음.

* **Amazon ElastiCache**

    Amazon ElastiCache는 **Redis 또는 Memcached를 사용한 인메모리 캐싱**을 제공함.

    자주 조회되는 **데이터를 캐시하여 데이터베이스의 읽기 부하를 줄이고 성능을 향상**시킬 수 있음.

    특히, 복잡한 쿼리나 빈번한 읽기 요청이 있는 경우 ElastiCache를 사용하여 데이터베이스의 부담을 줄일 수 있음.

* **Amazon CloudFront**

    Amazon CloudFront는 콘텐츠 배포 네트워크(CDN) 서비스로, **정적 콘텐츠와 API 응답을 캐시하여 지연 시간을 줄이고 읽기 성능을 향상**시킬 수 있음.

    전 세계적으로 분산된 엣지 로케이션을 통해 사용자에게 더 빠른 응답을 제공할 수 있음.

    CloudFront는 **S3와 통합하여 정적 콘텐츠를 캐시할 수 있으며, API Gateway와 통합하여 API 응답을 캐**시할 수도 있음.

## DAX 가 추가된 아키텍처

![example1 architecture2](https://github.com/user-attachments/assets/80b6edbf-7c2f-4bcf-809f-201c2e8ff53b)
