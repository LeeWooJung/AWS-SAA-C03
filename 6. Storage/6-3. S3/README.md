# [Amazon S3](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/Welcome.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/aca4d49f-b547-4ed7-a356-441c7cec2d4a" width = "25" height = "25"> S3

* **Amazon S3** (Simple Storage Service)는 Amazon Web Services (AWS)에서 제공하는 객체 스토리지 서비스로, 데이터 저장, 검색, 관리에 최적화된 서비스.  
* S3는 인터넷 규모의 스토리지를 제공하며, 데이터의 가용성, 보안, 성능, **확장성**을 보장.
* **Amazon S3**는 사용자가 데이터를 **버킷**이라는 논리적 컨테이너에 저장할 수 있도록 함.  
* 각 버킷에는 **객체**가 저장되며, 객체는 **키와 데이터**로 구성됨.  
* 키는 객체의 고유 식별자이고, 데이터는 실제 저장된 콘텐츠임.

### 주요 특징 및 기능

* **내구성과 가용성**  
    * **내구성**  
        * S3는 **99.999999999**% (11 9's) 내구성을 제공.  
        * 데이터는 여러 장치와 가용 영역(AZ)에 중복 저장됨.
    * **가용성**  
        * S3는 **99.99**% 가용성을 제공하며, 다양한 리전에서 데이터를 접근할 수 있도록 함.

* **확장성**  
    * S3는 거의 **무한히 확장 가능**하여 사용자는 필요에 따라 스토리지를 동적으로 확장할 수 있음.

* **보안**  
    * **액세스 제어**  
    [**IAM**](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/2.%20Identity%20and%20Access(IAM))을 통한 세밀한 접근 제어, 버킷 정책, ACL 등을 통해 데이터 접근을 제어.
    * **데이터 암호화**  
        * 서버 측 암호화(SSE)와 클라이언트 측 암호화 지원.  
        * 암호화 키는 **AWS Key Management Service** (KMS)를 통해 관리할 수 있음.

* **데이터 관리 기능**  
    * **버전 관리**  
    객체의 **여러 버전**을 저장하여 데이터의 이전 버전을 복구할 수 있음.
    * **수명 주기 관리**  
    객체의 수명 주기를 정의하여 **데이터의 이동과 삭제를 자동화**할 수 있음.
    * **복제**  
    Cross-Region Replication (CRR)과 Same-Region Replication (SRR)을 통해 데이터를 다른 리전에 복제할 수 있음.

* **통합 및 호환성**  
    * **API 및 SDK**  
    다양한 프로그래밍 언어 및 도구를 지원하는 API 및 SDK 제공.
    * **S3 이벤트 알림**  
    객체 생성, 삭제 등의 이벤트 발생 시 Lambda 함수, SNS, SQS 등과 통합하여 알림을 보낼 수 있음.

### 장점

* **비용 효율성**  
사용자는 저장한 데이터 양과 데이터 접근량에 따라 비용을 지불하므로, 비용 효율적으로 스토리지를 사용할 수 있음.
* **안정성**  
여러 AZ에 데이터를 분산 저장하여 데이터 손실 위험을 최소화함.
* **유연성**  
다양한 저장 클래스(Standard, Intelligent-Tiering, Glacier 등)를 제공하여 사용자의 요구에 맞게 비용과 성능을 최적화할 수 있음.

### 단점

* **데이터 전송 비용**  
데이터 전송 시 비용이 발생할 수 있으며, 대규모 데이터 이동 시 **비용이 증가**할 수 있음.
* **지연 시간**  
S3는 인터넷을 통해 액세스되므로, 네트워크 지연이 발생할 수 있음.

### 아키텍처

* **버킷**  
    * 데이터가 저장되는 **논리적 컨테이너**.  
    * 각 버킷은 **전역적으로 고유한 이름**을 가져야 함.
* **객체**  
    * 버킷 내에 저장되는 데이터.  
    * 각 객체는 **고유한 키**를 가짐.
* **리전**  
    * 버킷은 **특정 리전에 생성**되며, 데이터는 해당 리전 내의 여러 AZ에 중복 저장됨.

### Use Case

* **백업 및 복구**  
데이터를 안전하게 저장하고, 필요 시 빠르게 복구할 수 있음.
* **빅 데이터 분석**  
대규모 데이터 세트를 저장하고 분석 도구와 통합하여 분석할 수 있음.
* **미디어 저장소**  
이미지, 동영상 등의 대용량 미디어 파일을 저장하고 스트리밍할 수 있음.
* **정적 웹 사이트 호스팅**  
**정적** 콘텐츠를 저장하고 HTTP를 통해 제공할 수 있음.
* **분산 애플리케이션**  
여러 지역에 걸친 데이터 저장 및 동기화를 통해 글로벌 분산 애플리케이션을 지원함.

## S3 스토리지 클래스

* **S3 Standard**  
    * **자주 액세스되는 데이터를 위한 기본 스토리지 클래스**.  
    * 높은 가용성과 성능을 제공.
* **S3 Intelligent-Tiering**  
    * 액세스 패턴이 변하는 데이터에 대해 비용 효율적인 스토리지 제공.
* **S3 Standard-IA** (Infrequent Access)  
    * **자주 액세스되지 않는 데이터를 위한 스토리지 클래스**.  
    * 낮은 비용과 높은 내구성을 제공.
* **S3 One Zone-IA**  
    * **단일 AZ에 저장**되며, 낮은 비용을 제공.
* **S3 Glacier**  
    * **장기 보관**을 위한 저비용 아카이브 스토리지.
* **S3 Glacier Deep Archive**  
    * 매우 저렴한 비용의 장기 보관 스토리지.

## Summary

* Amazon S3는 다양한 데이터 저장 요구를 충족시키기 위한 강력하고 유연한 스토리지 솔루션을 제공.  
* 높은 내구성, 확장성, 보안을 통해 다양한 사용 사례에 적용할 수 있으며, 다양한 AWS 서비스와 통합하여 효율적인 데이터 관리와 분석을 지원함.

* 객체를 위한 Key/Value 저장소

* 큰 객체에 적합, 작은 객체에는 좋지 않음.

* Serverless, Scales Infinitely, 객체의 최대 사이즈는 5TB, **Versioning** 가능.

* **Tiers**: S3 Standard, S3 Infrequent Access, S3 Intelligent, S3 Glacier / Life cycle policy 적용하여 변환 가능.

* **Features**: Versioning, Encryption, Replication, MFA-Delete, Acess Logs 등.

* **Security**: IAM, Bucket Policies, ACL, Access Points, Object Lambda, CORS, Object/Value Lock.

* **Encryption**: SS3-S3, SSE-KMS, SSE-C, client-side, TLS in transit, default encryption.

* S3 Batch를 사용한 객체에 대한 **Batch Operations**, S3 Inventory를 사용하여 file listing 가능.

* **Performance**: Multi-part upload, S3 Transfer Acceleration, S3 Select.

* **Automation**: S3 Event Notification(SNS, SQS, Lambda, EventBridge)