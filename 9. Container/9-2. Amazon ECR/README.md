# [Amazon ECR](https://docs.aws.amazon.com/ko_kr/AmazonECR/latest/userguide/what-is-ecr.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/0959531c-f09e-40c4-b0f4-c9536551aff8" width = "30" height = "30"> AWS ECR

Amazon ECR (Elastic Container Registry)는 **Docker 컨테이너 이미지를 저장, 관리, 배포하기 위한 완전관리형 Docker 컨테이너 레지스트리 서비스**임.  

이는 **Amazon ECS** (Elastic Container Service)와 **완전히 통합**되어 있어, 개발자들이 애플리케이션의 컨테이너 이미지를 쉽게 저장하고 배포할 수 있도록 함. 또한 Amazon S3로 백업 가능함.

Private & Pulblic Repository가 존재함([Amazon ECR Public Gallery](https://gallery.ecr.aws)).

## 특징

### 완전관리형

**사용자가 인프라를 관리할 필요 없이** Docker 컨테이너 이미지를 저장, 관리, 배포할 수 있음.

### 통합된 경험

**Amazon ECS, AWS Fargate, AWS Lambda와 통합**되어 있어 쉽게 이미지를 배포할 수 있음.  

**IAM을 통해 접근 제어**를 쉽게 관리할 수 있음.

### 안전성

**이미지 암호화와 이미지 스캔을 통해 보안**을 강화할 수 있음.  

Amazon ECR은 저장된 모든 이미지를 **AWS KMS를 사용하여 자동으로 암호화**함.

### 확장성

수백만 개의 이미지를 저장할 수 있으며, **트래픽 증가에 따라 자동으로 확장**됨.

**사용량에 따라 과금되므로 초기 비용이 들지 않음**.

## 주요 기능

### 이미지 저장소 관리

Docker 이미지의 **저장소를 생성하고 관리**할 수 있음.  

이미지 태그와 버전 관리가 용이함.

### 이미지 스캔

저장된 이미지를 자동으로 스캔하여 **취약점을 발견**할 수 있음.

스캔 결과는 Amazon Inspector와 통합되어 관리됨.

### 이미지 복제

**AWS 리전 간에 이미지 복제**를 설정할 수 있어, **다중 리전에 걸친 배포가 쉬워짐**.

### API 및 CLI 지원

AWS Management Console, AWS CLI, AWS SDK를 통해 쉽게 ECR을 관리할 수 있음.

## 아키텍처

### 이미지 저장소  
Docker 이미지를 저장하는 **리포지토리**로 구성됨.

### IAM 역할  
이미지에 접근하는 사용자 및 애플리케이션을 제어함.

### Amazon ECS와의 통합  
**ECR에서 이미지를 가져와 ECS 클러스터에 배포**함.

### 이미지 스캔  
이미지를 스캔하여 보안 취약점을 확인함.

## Architecture Example

![ecr architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/c5564c3d-2bab-42e9-8fe4-3227e1a2af0f)


## 장점

* **보안 강화**  
이미지 암호화 및 취약점 스캔을 통해 보안을 강화할 수 있음.

* **비용 효율성**  
**사용한 만큼만 지불하는 모델로 초기 비용이 없음**.

* **확장성**  
트래픽 증가에 따라 자동으로 확장됨.

* **통합성**  
AWS의 다른 서비스들과 원활하게 통합되어 쉽게 사용할 수 있음.

## 단점

* **리전 종속성**  
리전 간 이미지 복제 설정이 필요할 수 있음.

* **비용**  
대량의 이미지 스캔 및 저장소 사용 시 비용이 발생할 수 있음.

## Summary
AWS ECR은 Docker **컨테이너 이미지를 효율적으로 저장, 관리, 배포할 수 있는 완전관리형 서비스**임.  

이는 Amazon ECS, AWS Fargate, AWS Lambda와 통합되어 있어, 개발자들이 애플리케이션을 쉽게 배포하고 관리할 수 있도록 돕는 강력한 도구임.  

또한 보안, 확장성, 통합성 등의 장점을 가지고 있어 다양한 애플리케이션 배포 시나리오에 적합함.