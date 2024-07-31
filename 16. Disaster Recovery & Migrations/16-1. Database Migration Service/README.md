# [Database Migration Service](https://docs.aws.amazon.com/ko_kr/dms/latest/userguide/Welcome.html)

## <img src = "https://github.com/user-attachments/assets/174fa80e-8cb9-4620-9ae8-ccf63e88abf4" width = "25" height = "25"> DMS

AWS Database Migration Service(AWS DMS)는 온프레미스, 다른 클라우드 서비스, 또는 AWS 내의 **데이터베이스를 AWS 클라우드로 쉽게 마이그레이션할 수 있도록 도와주는 완전 관리형 서비스**임. 

이 서비스는 **데이터베이스를 중단 없이 연속적으로 복제(using CDC)**하여 **데이터베이스 마이그레이션 과정에서 다운타임을 최소화**하고, **소스와 대상 데이터베이스 간의 호환성 문제를 해결하여 안전하고 효율적인 데이터 이전**을 지원함.

**지원하는 데이터베이스는 관계형 데이터베이스, NoSQL 데이터베이스, 데이터 웨어하우스 등이 포함**됨. 

Homogeneous Migration(Oracle to Oracle 등), Heterogeneous Migration(MS SQL to Aurora 등) 을 지원함.

DMS를 통해서 Database 복제를 진행하기 위해서는 DMS를 실행할 **EC2 Instance**를 생성해야함.

## 특징

### 다양한 데이터베이스 지원

MySQL, PostgreSQL, Oracle, Microsoft SQL Server, MariaDB, Amazon Aurora, MongoDB, 그리고 Amazon Redshift 등을 지원함.

### 연속적 데이터 복제

**실시간으로 데이터를 복제하여 마이그레이션 과정에서 데이터 동기화를 유지**함.

### 자동 변환

**AWS Schema Conversion Tool**(AWS SCT)을 사용하여 소스 데이터베이스 스키마를 대상 데이터베이스에 맞게 **자동 변환**할 수 있음.

### 완전 관리형 서비스

AWS가 인프라를 관리하여 사용자에게 **고가용성 및 내결함성을 제공**함.

### 보안

데이터 전송 중 암호화와 AWS Identity and Access Management(IAM)를 통해 보안을 강화함.

### 유연한 배포 옵션

온프레미스, AWS, 다른 클라우드 서비스 간에 유연하게 배포할 수 있음.

## 구성요소

* **소스 데이터베이스**(Source Database)

    마이그레이션할 데이터가 저장된 데이터베이스임.

    * On-premise & EC2 Instances: Oracle, MS SQL Server, MySQL, MariaDB, PostgreSQL, MongoDB, SAP, DB2

    * Azure: Azure SQL Database

    * Amazon RDS: Aurora도 포함.

    * Amazon S3

    * Document DB

* **대상 데이터베이스**(Target Database)

    데이터를 마이그레이션할 대상 데이터베이스임.

    * On-premise & EC2 Instances: Oracle, MS SQL Server, MySQL, MariaDB, PostgreSQL, SAP

    * Amazon RDS

    * Redshift, DynamoDB, S3

    * OpenSearch Service

    * Kinesis Data Streams

    * Apache Kfaka

    * DocumnetDB & Amazon Neptune

    * Redis & Babelfish

* **Replication Instance**

    소스와 대상 데이터베이스 간의 **데이터 마이그레이션을 처리하는 AWS DMS의 컴퓨팅 리소스**임.

* **엔드포인트(Endpoints)**

    소스 및 대상 데이터베이스의 연결 정보를 정의함.

* **마이그레이션 작업**(Migration Tasks)

    데이터베이스 마이그레이션 프로세스를 설정하고 실행하는 작업임.

## AWS Schema Conversion Tool

하나의 DB Engine에서 다른 DB Engine으로 Database의 스키마(Schema)를 변환해줌.

* **OLTP**

    SQL Server 또는 Oracle에서 MySQL, PostgreSQL, Aurora로 변경

* **OLAP**

    Teradata 또는 Oracle에서 Amazon Redshift로 변경

같은 DB Engine을 사용하고, 데이터베이스를 복제하는 경우에는 **SCT를 사용할 필요가 없음**.

## Multi-AZ Deployment

Multi-AZ가 활성화 되면, DMS는 **Standard Replica**를 Synchronously 다른 AZ로 복제함.

## 아키텍처

### Replication Instance 설정

AWS Management Console에서 Replication Instance를 생성하여 **소스와 대상 데이터베이스 간의 데이터 마이그레이션을 처리**함.

### 엔드포인트 설정

소스 및 대상 데이터베이스의 연결 정보를 설정함.

### 마이그레이션 작업 생성

마이그레이션 작업을 생성하고, 마이그레이션 방법(**전체 로드, CDC, 전체 로드 + CDC**)을 선택함.

### 데이터 변환 및 로드

AWS DMS가 소스 데이터베이스에서 데이터를 추출하여 대상 데이터베이스로 변환하고 로드함.

### 연속적 데이터 복제

마이그레이션 작업이 진행되는 동안 **실시간 데이터 복제를 통해 데이터 동기화를 유지**함.


## Use case

* **온프레미스 데이터베이스 마이그레이션**

    온프레미스 데이터베이스를 AWS 클라우드로 마이그레이션하여 클라우드의 장점을 활용함.

* **데이터베이스 업그레이드**

    기존 데이터베이스를 **최신 버전으로 업그레이드하면서 데이터를 마이그레이션**함.

* **하이브리드 클라우드 아키텍처**

    온프레미스와 AWS 클라우드 간의 하이브리드 클라우드 환경을 구축하고 데이터를 동기화함.

* **다양한 데이터 소스 통합**

    여러 데이터 소스를 **Amazon Redshift와 같은 데이터 웨어하우스로 통합하여 분석**함.

## Summary

AWS Database Migration Service는 **다양한 데이터베이스를 AWS 클라우드로 마이그레이션할 수 있는 완전 관리형 서비스**임. 

이를 통해 데이터베이스 마이그레이션 과정에서 **다운타임을 최소화하고, 데이터 동기화를 유지하며, 보안을 강화**할 수 있음. 

AWS DMS는 **다양한 데이터베이스 유형을 지원하며, 실시간 데이터 복제와 자동 스키마 변환 기능을 제공**함. 