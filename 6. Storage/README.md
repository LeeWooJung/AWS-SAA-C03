# EBS vs EFS

AWS의 **EBS**(Elastic Block Storage)와 **EFS**(Elastic File System)는 둘 다 AWS에서 제공하는 스토리지 서비스이지만, 그들의 사용 사례, 성능, 가용성, 내구성 등에는 몇 가지 중요한 차이점이 있음.

## EBS
EC2(Elastic Compute Cloud) 인스턴스에 연결되는 블록 스토리지 서비스임.  
EBS는 **단일 인스턴스에만 연결 가능**하며, 빠른 입출력 성능을 제공함. EBS는 **데이터에 빠르게 액세스하고 장기적으로 지속**해야 하는 경우에 적합하며, 부팅 볼륨, 트랜잭션 및 NoSQL 데이터베이스, 데이터 웨어하우징 및 ETL 등에 사용될 수 있음.  
하지만, EBS는 단일 가용 영역(AZ)에 중복 저장되므로, 다른 AZ에서의 고가용성을 제공하지는 않음.

## EFS
AWS 클라우드 서비스와 온프레미스 리소스에서 사용할 수 있는 간단하고 **확장 가능하며 탄력적인 완전 관리형 탄력적 NFS 파일 시스템**임.  
EFS는 수천 개의 EC2 인스턴스를 위한 스토리지이며 동시에 액세스 할 수 있음.  
EFS는 웹 서비스 및 컨텐츠 관리, 엔터프라이즈 어플리케이션, 홈 디렉터리, 데이터베이스 백업, 개발자 도구, 컨테이너 스토리지, 빅데이터 분석 등에 적합하며, **여러 AZ에 중복 저장되므로 높은 가용성을 제공**함.

# Storage Comparison

|Name|Distinction|  
|:---:|:---|  
|S3|Object Storage|
|S3 Glacier|Object Archival|
|EBS Volumes|하나의 EC2 인스턴스를 위한 네트워크 스토리지, Block Storage|
|Instance Storage|EC2 인스턴스를 위한 물리적 스토리지(High IOPS)|
|EFS|Linux 인스턴스를 위한 네트워크 파일 시스템, POSIX 파일 시스템, File Storage|
|FSx for Windows|Windows 서버를 위한 네트워크 파일 시스템|
|FSx for Lustre|고성능 컴퓨팅 Linux 파일 시스템|
|FSx for NetAPP ONTAP|높은 OS 호환성|
|FSx for Open ZFS|관리형 ZFS 파일 시스템|
|Storage Gateway|S3 & FSx File Gateway, Volume Gateway(cache & stored), Tape Gateway, 온프레미스와 동기화|
|Transfer Family|Amazon S3, EFS 위에 FTP, FTPS, SFTP 인터페이스 / 온프레미스와 동기화|
|DataSync|온프레미스에서 AWS로 또는 AWS에서 AWS로 데이터 동기화 일정 예약|
|Snowcone/Snowball/Snowmobile|대량의 데이터를 클라우드로 물리적으로 이동하기 위해 사용|