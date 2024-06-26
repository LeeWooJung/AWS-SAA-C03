# [S3 Storage Class](https://aws.amazon.com/ko/s3/storage-classes/)

## S3 Storage Class

* **Amazon S3의 스토리지 클래스**는 사용자가 데이터를 저장할 때 각 데이터의 접근 빈도와 내구성 요구 사항에 맞게 최적화된 비용과 성능을 제공하기 위해 다양한 옵션을 제공.  
* 각 스토리지 클래스는 고유한 특성과 요금 구조를 가지고 있음.

## S3 Standard
* **자주 접근**하는 데이터를 위한 기본 스토리지 클래스.
* **특징**  
    * 높은 내구성(99.999999999%)과 가용성(99.99%)을 제공.
    * 멀티 AZ(가용 영역)에 데이터를 복제하여 높은 내구성을 보장.
    * **지연 시간과 처리량**이 중요한 워크로드에 적합.
    * **사용 사례**  
    웹사이트, 모바일 앱, 데이터 분석, 배포 콘텐츠.

## S3 Intelligent-Tiering
* 액세스 패턴이 알 수 없는 데이터 또는 **변동이 심한** 데이터를 위한 스토리지 클래스.
* **특징**  
    * 두 가지 접근 계층(자주 접근과 드물게 접근) 간에 자동으로 데이터를 이동시켜 비용을 최적화.
    * 객체 접근 패턴을 모니터링하여 30일 동안 접근하지 않은 데이터를 드물게 접근 계층으로 이동.
    * 관리 오버헤드가 없음.
    * **사용 사례**  
    액세스 패턴이 예측할 수 없는 데이터, 새로운 애플리케이션.

## S3 Standard-IA (Infrequent Access)
* **드물게 접근**하는 데이터를 위한 스토리지 클래스.
* **특징**  
    * S3 Standard와 동일한 높은 내구성(99.999999999%)을 제공하지만, **낮은 스토리지 비용과 높은 액세스 비용**을 제공.
    * **멀티 AZ**에 데이터를 저장하여 높은 내구성을 보장합니다.
    * **사용 사례**  
    장기 보관 데이터, 백업 및 재해 복구 데이터.

## S3 One Zone-IA
* 드물게 접근하는 데이터를 위한 스토리지 클래스이지만, **단일 AZ**에 데이터를 저장.
* **특징**  
    * S3 Standard-IA보다 저렴한 비용으로 데이터를 저장.
    * **단일 AZ**에만 데이터를 저장하므로 내구성이 낮음.
    * **사용 사례**  
    재생 가능한 데이터, 백업, 잘못된 데이터 또는 드물게 접근하는 데이터.

## S3 Glacier
* **장기 보관 및 데이터 아카이빙**을 위한 스토리지 클래스.
* **특징**
    * **매우 저렴한 비용으로 데이터를 장기 보관**할 수 있음.
    * 데이터 복구 시간은 몇 분에서 몇 시간까지 소요될 수 있음.
    * 데이터 내구성은 S3 Standard와 동일.
    * **사용 사례**  
    장기 데이터 보관, 법적 또는 규제 요구 사항 데이터, 대용량 데이터 아카이빙.

## S3 Glacier Deep Archive
* 가장 저렴한 장기 데이터 아카이빙 스토리지 클래스.
* **특징**  
    * S3 Glacier보다 저렴한 비용으로 데이터를 저장.
    * 데이터 복구 시간은 12시간에서 48시간까지 소요될 수 있음.
    * 데이터 내구성은 S3 Standard와 동일.
    * **사용 사례**  
    거의 접근하지 않는 데이터, 데이터 보존 및 규제 아카이빙.

## S3 Outposts
* AWS Outposts 인프라 내에서 **데이터를 로컬에 저장하는 스토리지 클래스**.
* **특징**  
    * AWS Outposts에서 S3 API와 완전히 호환.
    * **로컬 데이터 처리, 로컬 규제 및 데이터 주권 요구 사항**을 충족할 수 있음.
    * **사용 사례**  
    온프레미스 데이터 처리, 데이터 주권 요구 사항이 있는 워크로드.
    
## S3 Standard-Reduced Redundancy (RRS)
* 덜 중요한 데이터를 위한 스토리지 클래스 (신규 사용 권장되지 않음)
* **특징**  
    * 내구성이 낮아져 비용을 절감.
    * 멀티 AZ에 데이터를 저장하지 않음.
    * **사용 사례**  
    재생 가능한 데이터, 임시 데이터, 쉽게 재생할 수 있는 데이터를 위한 저장소.