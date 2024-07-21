# [Amazon DynamoDB](https://docs.aws.amazon.com/ko_kr/amazondynamodb/latest/developerguide/Introduction.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/dbaaf70b-93cd-4844-b041-0bc13fbbab60" width = "25" height = "25"> Amazon DynamoDB

Amazon DynamoDB는 **완전 관리형 NoSQL 데이터베이스 서비스**로, 일관되고 짧은 지연 시간과 유연한 확장성을 제공함.  

테이블 기반 데이터 모델을 사용하며, **자동으로 데이터 복제와 분산을 통해 높은 가용성과 내구성을 보장**함.

## 특징

### 완전 관리형  
인프라 관리 없이 데이터베이스를 운영할 수 있음.

### 높은 확장성  
읽기 및 쓰기 처리량을 자동으로 확장하여 애플리케이션 요구사항을 충족할 수 있음.

### 짧은 지연 시간  
일관되고 짧은 지연 시간으로 빠른 데이터 액세스를 보장함. 수백만 요청을 몇 초만에 처리.

### 데이터 모델  
키-값 및 문서 데이터 모델을 지원함.

### 내구성 및 가용성  
여러 AWS 리전에 데이터 복제를 통해 내구성과 가용성을 제공함.

### 보안  
[IAM](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/2.%20Identity%20and%20Access(IAM))과 통합되어 세부적인 접근 제어를 가능하게 함. 데이터 암호화와 함께 사용됨.

## 장점

### 확장성  
**자동 확장 기능**을 통해 애플리케이션의 요구 사항에 따라 유연하게 확장할 수 있음.

### 성능  
짧은 지연 시간과 고성능을 제공함.

### 간편한 관리   
서버 관리와 같은 운영 작업 없이 데이터베이스를 관리할 수 있음.

### 비용 효율성  
사용한 만큼만 비용을 지불하는 요금 모델을 제공함.

### 통합성  
**AWS Lambda, AWS AppSync 등 다른 AWS 서비스와 쉽게 통합**할 수 있음.

## 단점

### 복잡한 데이터 모델  
관계형 데이터베이스와 다르게 **조인이 불가능하여 복잡한 쿼리를 수행하는 데 제약**이 있음.

### 비용 관리  
대량의 읽기 및 쓰기 요청이 있는 경우 비용이 증가할 수 있음.

## 아키텍처

### 테이블  
데이터는 테이블에 저장되며, 각 테이블은 **고유한 기본 키**를 가짐. 각 키는 테이블 생성 당시에 정의 되어야 함.

무한개의 Item을 가질 수 있음.

Standard & Infrequent Access(IA) Table Class가 존재.

### 아이템  
테이블의 각 행을 아이템이라 부르며, **속성의 집합**으로 구성됨.

### 속성  
각 아이템의 데이터 요소로, **속성 값은 스칼라 값(Scalar - String, Number, Binary, Boolean, Null), 문서(List, Map), Set(String Set, Number Set, Binary Set)또는 배열**이 될 수 있음.

속성은 지속적으로 추가될 수 있으며 null 값을 가질 수 있음.

### 프로비저닝된 처리량  
각 테이블은 설정된 읽기 및 쓰기 처리량에 따라 **자동으로 확장 및 축소**됨.

### 글로벌 테이블  
여러 리전 간에 데이터를 자동으로 복제하여 전 세계적으로 높은 가용성과 내구성을 제공함.

이와 같은 특성 덕분에 **DynamoDB에서는 Schema를 빠르게 확장**할 수 있음.

## Use case

### 실시간 애플리케이션  
높은 처리량과 짧은 지연 시간이 필요한 실시간 게임, IoT, 금융 애플리케이션.

### 세션 관리  
사용자 세션 데이터를 저장하고 관리하는 데 적합함.

### 이벤트 추적  
이벤트 로그와 같은 대규모 데이터를 처리하고 분석하는 데 사용됨.

### 제품 카탈로그  
다양한 속성을 가진 제품 정보를 저장하고 빠르게 검색하는 데 유용함.

## Summary 

* Amazon DynamoDB는 **완전 관리형 NoSQL 데이터베이스 서비스**로, 높은 확장성, 성능, 가용성을 제공함. 

* 다양한 AWS 서비스와 통합이 쉬우며, 비용 효율적인 운영이 가능함. 단, 복잡한 데이터 모델링과 비용 관리에 주의가 필요함.

* **관리형 서버리스 NoSQL Database**. millisecond 이내의 지연시간.

* **Capacity Mode**: Optional Auto Scaling 혹은 On-demand Capacity를 적용하는 Provisioned Capacity.

* Higly Available, Multi AZ(default), 읽기/쓰기 분리.

* Read Cache를 위한 **DAX Cluster**, microsecond 지연시간.

* **IAM**을 이용하여 Security, Authentication, Authorization 가능.

* **Event 처리**: AWS Lambda 혹은 Kinesis Data Streams와 연결할 수 있는 **DynamoDB Streams**.

* **Global Tables**: Active-Active Setup

* Point in time Restore(PITR) to New Table(~35일), On-Demand Backup 가능.

* PITR Window를 사용하여 S3로 Export 가능, S3로 부터 import 가능.

* **빠르게 증가하는 스키마**에 적용하기 좋음.
