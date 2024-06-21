# [Amazon Snow Family](https://aws.amazon.com/ko/snow/)

## AWS Snow Family

* AWS의 Snow Family는 **대규모 데이터 전송(offline), 저장, 처리 요구**를 충족하기 위해 설계된 **포터블 데이터 전송 및 엣지 컴퓨팅 디바이스 시리즈**임.  
* Snow Family에는 **Snowcone, Snowball, Snowmobile**이라는 세 가지 주요 제품이 있음.  
* 이들은 다양한 데이터 처리 및 전송 요구 사항에 맞춰 설계되었으며, 각 제품은 특정 시나리오에 최적화되어 있음.

## [AWS Snowcone](https://aws.amazon.com/ko/snowcone/)

Snowcone은 Snow Family 중 가장 작은 디바이스로, **소형 및 저전력 환경에서의 데이터 전송 및 엣지 컴퓨팅**을 지원함.

### 특징
* **크기와 무게**  
작고 가벼운 디자인으로, 크기는 9.0 x 6.0 x 3.0 인치이며, 무게는 약 4.5 파운드.  
* **저장 용량**  
8TB의 사용 가능 스토리지 제공.  
* **네트워킹**  
2개의 USB-C 포트와 1개의 10GBASE-T 이더넷 포트 지원.  
* **엣지 컴퓨팅**  
AWS IoT Greengrass 및 EC2 컴퓨팅 기능을 지원하여 엣지에서의 데이터 처리 가능.
* **AWS DataSync**  
인터넷에 연결하여 AWS DataSync를 사용해서 데이터를 보낼 수 있음.

### Use Case  
* 원격 위치에서의 데이터 수집 및 처리.
일시적인 데이터 저장 및 전송.
* 네트워크 연결이 제한된 환경에서의 데이터 전송.

## [AWS Snowball](https://aws.amazon.com/ko/snowball/)
* Snowball은 중간 크기의 디바이스로, **대규모 데이터 전송과 엣지 컴퓨팅 기능**을 지원함.  
* Snowball Edge Storage Optimized와 Snowball Edge Compute Optimized 두 가지 변형이 있음.

### 특징
* **크기와 무게**  
견고한 디자인으로, **이동 및 운반이 용이**함.  
* **저장 용량**  Storage Optimized는 최대 80TB의 사용 가능 스토리지 제공, Compute Optimized는 최대 42TB의 사용 가능 스토리지 제공.  
* **네트워킹**  
10Gbps, 25Gbps, 및 40Gbps 네트워크 연결 지원.  
* **엣지 컴퓨팅**  
AWS Lambda, EC2 컴퓨팅 기능 및 S3 호환 API를 지원하여 엣지에서의 데이터 처리 가능.

### Use case
* 대규모 데이터 전송(예: **데이터 센터 마이그레이션, 백업 및 복구**).
* 엣지에서의 데이터 수집 및 분석.
일시적 네트워크 연결 시 대량 데이터 전송.

## [AWS Snowmobile](https://aws.amazon.com/ko/blogs/korea/aws-snowmobile-move-exabytes-of-data-to-the-cloud-in-weeks/)
Snowmobile은 가장 큰 디바이스로, 페타바이트 및 엑사바이트 규모의 대규모 데이터 전송을 위한 트럭 기반 솔루션임.

### 특징
* **크기와 무게**  
45피트 길이의 견고한 컨테이너 트럭.
* **저장 용량**  
최대 100PB의 저장 용량 제공하여 10PB 이상의 데이터는 **Snowball** 대신 **Snowmobile**을 사용하는 것이 좋음.
* **보안**  
256비트 암호화 및 내구성 있는 보안 아키텍처.
* **네트워킹**  
고속 네트워크 연결 지원.

### Use case
* 대규모 데이터 센터 마이그레이션.
* 페타바이트 및 엑사바이트 규모의 데이터 백업 및 복구.
* 클라우드로의 대규모 데이터 전송.

## 공통 특징
* **보안**  
모든 Snow Family 디바이스는 전송 중 데이터 암호화, 암호화된 디스크, 역할 기반 액세스 제어 및 데이터 삭제 후 검증 기능을 포함한 강력한 보안 기능을 제공함.
* **관리**  
AWS Management Console 및 AWS CLI를 통해 간편하게 디바이스 관리 가능.
* **데이터 전송**  
대량의 데이터를 신속하고 효율적으로 AWS로 전송할 수 있도록 설계됨.
* **엣지 컴퓨팅**  
AWS Lambda와 EC2 인스턴스를 통해 엣지에서 데이터 처리 및 분석 가능.

## 차이점
* **크기 및 용량**  
    * Snowcone은 소형 장치로 소규모 데이터 전송 및 **엣지 컴퓨팅**에 적합.  
    * Snowball은 중간 규모 데이터 전송에 적합.  
    * Snowmobile은 대규모 데이터 전송에 적합.
* **용도**  
    * Snowcone은 저전력 및 소규모 환경에 적합.  
    * Snowball은 대규모 전송과 **엣지 컴퓨팅**에 적합.  
    * Snowmobile은 초대규모 데이터 전송에 사용됨.

|**특징**|**Snowcone**|**Snowball Edge Storage Optimized**|**Snowmobile**|
|:---|:---:|:---:|:---:|
|**Storage Capacity**|8TB HDD|80TB usable|< 100PB|
|**Migration Size**|Up to 24 TB, online & offline|Up to petabytes, offline|Up to exabytes, offline|
|**DataSync**|Pre-installed|||

## 사용 과정

**장치 주문 및 준비**

* **주문**  
    * AWS Management Console에서 Snow Family 디바이스(Snowcone, Snowball, Snowmobile)를 주문함.
    * 필요한 저장 용량과 디바이스 유형을 선택함.

* **디바이스 준비**  
    * **AWS가 디바이스를 구성하고 사용자에게 배송**함.
    * 디바이스에는 데이터 전송에 필요한 소프트웨어와 도구가 포함되어 있음.

**데이터 준비 및 전송**  

* **데이터 준비**  
    * 데이터를 전송하기 전에 디바이스에 데이터를 암호화하여 저장할 준비를 함.
    * AWS에서 제공하는 Snow Family Client 또는 EC2 인스턴스에 설치된 Snowball Client를 사용하여 데이터를 준비함.

* **데이터 전송**  
    * 디바이스를 네트워크에 연결하고 전원 공급을 함.
    * Snow Family Client 또는 AWS CLI를 사용하여 데이터를 디바이스로 전송함.
    * 데이터 전송 중에 데이터는 자동으로 암호화됨.

**디바이스 반환 및 데이터 업로드**

* **디바이스 반환**  
    * 데이터 전송이 완료되면 디바이스를 AWS로 반환함.
    * Snowcone과 Snowball의 경우, 디바이스에는 반송 라벨이 포함되어 있음.
    * Snowmobile의 경우, AWS가 직접 디바이스를 픽업함.

* **데이터 업로드**  
    * 디바이스가 AWS에 도착하면, AWS는 디바이스의 데이터를 **S3 버킷 또는 지정된 AWS 서비스로 업로드**함.
    * 업로드된 데이터는 사용자가 지정한 S3 버킷 또는 다른 AWS 서비스에서 접근 가능함.

**데이터 처리 및 관리**

* **데이터 처리**  
    * 데이터가 AWS 클라우드에 업로드되면, 다양한 AWS 서비스 (예: S3, EC2, EMR 등)를 사용하여 데이터를 처리함.
    * **엣지 컴퓨팅 기능**을 사용하는 경우, 데이터를 처리하고 분석할 수 있음.

* **데이터 관리**  
    * AWS Management Console 또는 AWS CLI를 통해 업로드된 데이터를 관리함.
    * 데이터 보안, 접근 제어, 데이터 삭제 등 다양한 관리 기능을 사용할 수 있음.

**보안 및 컴플라이언스**

* **데이터 보안**  
    * 데이터는 전송 중 및 저장 중에 256비트 암호화로 보호됨.
    * 디바이스에 대한 물리적 보안 및 역할 기반 접근 제어가 적용됨.

* **컴플라이언스**  
    * Snow Family 디바이스는 다양한 산업 및 정부 규제 요구사항을 충족하도록 설계됨.
    * 데이터를 안전하게 처리하고 전송할 수 있도록 검증된 프로세스를 제공함.