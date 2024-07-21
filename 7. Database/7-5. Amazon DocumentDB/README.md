# [Amazon DocumentDB](https://docs.aws.amazon.com/documentdb/latest/developerguide/what-is.html)

## <img src = "https://github.com/user-attachments/assets/7933efca-f795-4760-9004-702791323416" width = "25" height = "25"> Amazon DocumentDB

**Amazon DocumentDB** (with MongoDB compatibility)는 AWS에서 제공하는 **완전 관리형 문서형 데이터베이스 서비스**임. 

**높은 가용성, 확장성 및 성능**을 제공하도록 설계되었으며, **MongoDB(NoSQL)와의 호환성**을 지원함으로써 MongoDB를 사용하는 애플리케이션이 쉽게 마이그레이션할 수 있도록 돕는 서비스임.

MongoDB는 데이터 저장, 쿼리, index JSON Data에 사용됨.

## 특징

### 완전 관리형 서비스

Amazon DocumentDB는 **백업, 패치, 모니터링, 복구 등 데이터베이스 관리 작업을 자동으로 처리**함.  

이를 통해 **관리 오버헤드를 줄이고 애플리케이션 개발에 집중**할 수 있음.

### MongoDB 호환성

DocumentDB는 MongoDB 3.6, 4.0 및 4.2 버전과 호환되며, **MongoDB 클라이언트 및 도구를 사용**할 수 있음.  

이를 통해 기존 **MongoDB 애플리케이션을 손쉽게 마이그레이션**할 수 있음.

### 확장성

필요에 따라 **스토리지 및 컴퓨팅 리소스를 독립적으로 확장**할 수 있음.  

**스토리지는 자동으로 확장**되며 최대 10GB까지 지원함. 

컴퓨팅 리소스는 수 분 내에 변경할 수 있음.

### 고가용성

Amazon DocumentDB는 기본적으로 **여러 가용 영역(accross 3 AZ)에 걸쳐 데이터를 복제**하여 높은 가용성을 제공함. 

**자동 복구 기능**을 통해 장애 발생 시에도 데이터의 가용성을 유지할 수 있음.

### 보안

Amazon **VPC를 통한 네트워크 격리**, AWS **Identity and Access Management** (IAM)를 통한 접근 제어, **AWS Key Management Service** (KMS)를 통한 데이터 암호화 등을 제공하여 데이터의 보안을 보장함.

### 백업 및 복구

**지속적인 백업 기능**을 통해 특정 시점으로의 복구(Point-in-Time Recovery)를 지원함. 

또한, **스냅샷 기능**을 사용하여 데이터베이스의 특정 상태를 저장하고 복원할 수 있음.

## Use case

* **콘텐츠 관리 시스템(CMS)**
    문서, 이미지, 비디오 등 다양한 유형의 데이터를 저장하고 빠르게 검색해야 하는 시스템에 적합함.

* **카탈로그 관리**  
    전자상거래 사이트의 제품 **카탈로그를 관리**하는 데 사용될 수 있음. 
    
    다양한 속성의 제품 정보를 유연하게 저장하고 검색할 수 있음.

* **모바일 및 웹 애플리케이션**  
    사용자 프로필, 세션 데이터, 사용자 생성 콘텐츠 등을 저장하고 빠르게 액세스할 수 있음.

## Summary

* Amazon DocumentDB는 **높은 성능과 확장성을 제공하는 완전 관리형 문서형 데이터베이스 서비스**로서, **MongoDB와의 호환성**을 통해 쉽게 마이그레이션할 수 있으며, 다양한 데이터 관리 작업을 자동화하여 **운영 오버헤드를 줄일 수 있음**. 

* 이를 통해 기업은 더 효율적으로 애플리케이션을 개발하고 운영할 수 있음.






