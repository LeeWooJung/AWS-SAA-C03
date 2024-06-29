# [S3 File Gateway](https://docs.aws.amazon.com/ko_kr/filegateway/latest/files3/what-is-file-s3.html)

## S3 File Gateway

* AWS S3 File Gateway는 **온프레미스 애플리케이션이 Amazon S3를 파일 시스템으로 사용할 수 있게 해주는 하이브리드 클라우드 스토리지 솔루션**임.  
* 이를 통해 로컬 네트워크에서 NFS(Network File System) 또는 SMB(Server Message Block) 프로토콜을 사용하여 **S3 버킷에 파일을 저장하고 액세스**할 수 있음.  
* S3 File Gateway는 **파일을 S3 객체로 변환하여 저장**하며, 클라우드 네이티브 애플리케이션과의 통합을 용이하게 함.  
* S3 Standard, S3 Standard IA, S3 One Zone IA, S3 Intelligent Tiering을 모두 사용할 수 있음.  
* **Lifecycle Policy**를 적용하여 S3 bucket에 저장된 객체를 S3 Glacier로 이동할 수 있음.
* 각 File Gateway에 **IAM Role**을 부여하여 Bucket에 대한 액세스를 조율할 수 있음.

## 구성 요소 및 특징

### 파일 시스템 인터페이스

* **NFS 또는 SMB 프로토콜**을 사용하여 온프레미스 파일 시스템으로 동작함.  
* 온프레미스 애플리케이션은 파일 시스템을 통해 파일을 읽고 쓸 수 있음.

### S3와의 통합

* 저장된 파일은 **S3 객체로 변환**되어 S3 버킷에 저장됨.  
* 파일 메타데이터는 **S3 객체 메타데이터**로 저장됨.

### 로컬 캐싱

* **자주 액세스되는 파일은 로컬에 캐싱**되어 빠른 접근 속도를 제공함.  
* 캐시 크기는 설정 가능하며, 사용자의 요구에 맞춰 조정할 수 있음.

### 데이터 암호화 및 보안

* 파일은 S3로 전송되는 동안 **SSL/TLS로 암호화**됨.
* 저장 시에는 **S3 서버 측 암호화(SSE-S3, SSE-KMS)를 지원**함.

### 게이트웨이 관리

* AWS Management Console, AWS CLI, 또는 AWS SDK를 통해 관리 가능함.  
* **사용량 및 성능 메트릭을 모니터링**할 수 있음.


## 장점

* **원활한 통합**  
기존 파일 기반 애플리케이션을 **변경하지 않고도 S3 스토리지를 사용**할 수 있음.
* **확장성**  
S3의 무제한 스토리지 용량을 활용하여 **대규모 데이터를 저장**할 수 있음.  
* **보안**  
전송 중 및 저장 시 **데이터 암호화를 통해 보안을 강화**함.
* **데이터 보호**  
S3의 **버전 관리 및 Lifecycle 정책을 통해 데이터 보호 및 보관을 관리**할 수 있음.

## 단점

* **네트워크 종속성**  
네트워크 연결 상태에 따라 성능이 영향을 받을 수 있음.
* **지연 시간**  
파일 접근 시 네트워크 지연이 발생할 수 있음.

## Use Case

* **백업 및 복구**  
로컬 파일을 **S3로 백업하여 데이터 보호 및 재해 복구 시나리오**에 활용할 수 있음.
* **데이터 공유**  
여러 지역에 걸친 **파일 공유 및 협업을 위한 스토리지 솔루션**으로 사용 가능함.
* **데이터 분석**  
S3에 저장된 파일을 기반으로 클라우드 네이티브 데이터 분석 및 머신 러닝 워크로드에 활용할 수 있음.

## 아키텍처

### 온프레미스 환경

* NFS 또는 SMB 프로토콜을 지원하는 파일 서버가 설정됨.  
* **파일 게이트웨이가 온프레미스 서버와 통합되어 파일을 로컬 캐시에 저장**함.

### AWS 환경

* 파일 게이트웨이는 S3 버킷과 연결되어 있음.  
* 온프레미스에서 업로드된 파일은 S3 객체로 변환되어 버킷에 저장됨.  
* S3 버킷에 저장된 파일은 클라우드 애플리케이션 및 서비스에서 접근 가능함.  

## Architecture Example

![S3 File Gateway architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/6f9b43e6-c4ef-4690-8798-1358362d38fe)


----
AWS S3 File Gateway는 온프레미스 파일 시스템과 S3를 원활하게 연결하여 **하이브리드 클라우드 환경을 구현**할 수 있는 강력한 솔루션임.  
이를 통해 기업은 클라우드 스토리지의 **확장성과 보안을 온프레미스 파일 워크로드에 적용**할 수 있음.