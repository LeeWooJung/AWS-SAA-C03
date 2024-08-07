# [Amazon Glue](https://docs.aws.amazon.com/ko_kr/glue/latest/dg/what-is-glue.html)

## <img src = "https://github.com/user-attachments/assets/c23b2097-c06a-44f0-8186-305e361d6e63" width = "30" height = "30"> Amazon Glue

Amazon Glue는 **AWS의 fully managed ETL** (Extract, Transform, Load) 서비스로, **데이터 준비 및 로딩을 자동화하여 분석을 위해 데이터를 변환하고 이동**할 수 있게 해줌. 

Glue는 **데이터 카탈로그, ETL 작업, 데이터 탐색 및 스키마 발견 기능**을 제공함.

## 특징

### 서버리스

**인프라 관리 없이 ETL 작업**을 실행할 수 있음(운영 오버헤드 감소).

### 자동 스키마 인퍼런스

데이터 소스에서 자동으로 스키마를 추론하고 데이터 카탈로그를 구축함.

### ETL 자동화

**파이프라인을 자동으로 설정하고 실행**할 수 있음.

### 확장성

데이터 양에 따라 자동으로 확장됨.

### AWS 서비스 통합

**S3, RDS, Redshift 등 다양한 AWS 서비스와 원활하게 통합**됨.


## 구성요소

* **Glue Data Catalog**

    데이터의 메타데이터를 저장하고 관리함.

* **Glue Crawlers**

    데이터 소스를 탐색하여 스키마를 자동으로 생성함.

* **Glue Jobs**

    데이터를 변환하고 로드하는 작업을 정의함.

* **Glue Development Endpoints**

    개발자가 코드를 작성하고 디버깅할 수 있는 환경을 제공함.

* **Glue Triggers**

    특정 이벤트에 따라 작업을 자동으로 실행하도록 설정할 수 있음.

## 아키텍처

Amazon Glue는 **다양한 데이터 소스에서 데이터를 가져와 ETL 작업을 수행하고, 결과를 데이터 웨어하우스나 데이터 레이크로 로드하는 구조**로 설계됨. 

Glue Crawlers가 데이터를 탐색하여 Glue Data Catalog에 메타데이터를 저장하고, Glue Jobs가 데이터를 변환하여 최종 목적지로 로드함.


## 장점

* **관리 용이성**

    서버리스 구조로 관리 부담을 줄임.

* **자동화**

    데이터 탐색, 스키마 생성 및 ETL 작업을 자동화하여 효율성을 높임.

* **확장성**

    데이터 양에 따라 자동으로 확장됨.

* **통합성**

    AWS의 다른 서비스와 쉽게 통합됨.


## 단점

* **학습 곡선**

    복잡한 ETL 작업의 경우 학습 곡선이 존재함.

* **비용**

    대규모 작업에서는 비용이 증가할 수 있음.

* **제한된 커스터마이징**

    특정한 커스터마이징이 필요할 경우 제약이 있을 수 있음.


## Use case

* **데이터 레이크 구축**

    **다양한 소스에서 데이터를 수집하여 S3에 저장**하고, 데이터 레이크를 구축함.

* **데이터 웨어하우스 로딩**

    데이터를 변환하여 **[Redshift](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-11.%20Amazon%20Redshift)와 같은 데이터 웨어하우스**로 로드함.

* **실시간 분석**

    실시간 데이터를 수집하고 변환하여 분석 플랫폼으로 전달함.

* **데이터 통합**

    **여러 데이터 소스를 통합하여 일관된 데이터 뷰**를 제공함.

## Architecture Example



### AWS Glue

![glue architecture1](https://github.com/user-attachments/assets/8a5f2bb4-ebcb-4435-8ed5-a851080e5f5a)

### Convert data into Parquet format

![glue architecture2](https://github.com/user-attachments/assets/9706f0f5-114c-439a-b057-f5a95640450f)

### Glue Data Catalog

![glue architecture3](https://github.com/user-attachments/assets/7bfd4b60-d810-4621-bcb7-d4c318bd615f)


## Summary

Amazon Glue는 AWS의 **fully managed ETL 서비스로, 데이터 탐색, 스키마 생성, 데이터 변환 및 로딩을 자동화**하여 데이터 준비 과정을 효율화함. 

**서버리스 구조**로 관리 부담을 줄이며, **자동화 및 확장성 기능**을 통해 다양한 데이터 통합 및 분석 작업에 활용될 수 있음.

Glue는 **AWS의 다른 서비스와 원활하게 통합**되어 데이터 레이크 및 데이터 웨어하우스 구축, 실시간 분석 등 다양한 사용 사례에서 유용하게 사용될 수 있음.