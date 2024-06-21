# [S3 Storage Lens](https://aws.amazon.com/ko/blogs/korea/s3-storage-lens/)

## S3 Storage Lens

* Amazon S3 Storage Lens는 **S3 사용량과 활동에 대한 통합 뷰를 제공하는 분석 도구**.  
* 이를 통해 데이터 저장소를 더 효율적으로 관리하고 비용을 최적화할 수 있음.  
* S3 Storage Lens는 대시보드, 프리미엄 지표, 권장 사항을 통해 사용자에게 인사이트를 제공함.

### 주요 기능 및 특징

* **통합 뷰**  
    * 모든 S3 버킷 및 계정의 사용량과 활동을 통합하여 보여줌.
    * 여러 계정 및 리전에 걸쳐 데이터를 분석할 수 있음.

* **대시보드**  
    * **웹 기반**의 대시보드를 통해 다양한 차원에서 데이터를 시각화.
    * 기본 제공되는 대시보드를 통해 저장소 사용량, 비용, 성능, 보안 상태 등을 모니터링할 수 있음.
    * 사용자 정의 가능한 위젯을 통해 필요한 정보를 한눈에 볼 수 있음.

* **프리미엄 지표**  
    * 스토리지 트렌드, 비율, 연령 분석, 빈도 분석 등 29개 이상의 고급 지표를 제공.
    * 객체 크기 분포, 객체 수, 요청 유형, 전송된 데이터 양 등 상세한 데이터를 제공.

* **권장 사항**  
    * 비용 최적화 및 데이터 관리 개선을 위한 자동화된 권장 사항을 제공.
    * 잘못된 구성이나 비효율적인 사용 패턴을 식별하여 개선 방안을 제시.

* **데이터 수집 및 보고**  
    * S3 Storage Lens는 **24시간마다** 데이터를 수집하여 보고서를 생성.
    * CSV 형식으로 데이터를 내보내거나 AWS Management Console을 통해 시각화할 수 있음.

### 주요 구성 요소

* **대시보드**  
    * 대시보드는 사용자가 스토리지 활동을 모니터링할 수 있는 **인터페이스**를 제공.
    * 여러 레벨에서 데이터를 분석할 수 있는 다양한 **위젯과 필터**를 포함.
    * 사용자 정의 가능한 설정을 통해 특정 요구에 맞는 대시보드를 구성할 수 있음.

* **지표 (Metrics)**  
    * **기본 지표**  
    저장된 데이터 양, 객체 수, 스토리지 클래스 별 사용량 등의 기본적인 정보를 제공.
    * **프리미엄 지표**  
    데이터 연령, 비율 분석, 요청 유형 등 고급 분석 기능을 포함.

* **권장 사항 (Recommendations)**:
    * 데이터 삭제 정책, 저장소 클래스 전환, 액세스 권한 관리 등 구체적인 개선 방안을 제안.

* **보고서 (Reports)**  
    * 자동으로 생성되는 보고서를 통해 주기적인 데이터 분석 결과를 제공.
    * 보고서를 **CSV 형식**으로 내보내어 외부 분석 도구와 통합할 수 있음.

### 장점
* **통합 관리**  
여러 계정과 리전에서 S3 사용량을 통합적으로 관리할 수 있음.
* **비용 절감**  
불필요한 데이터와 비효율적인 저장소 사용 패턴을 식별하여 비용을 절감할 수 있음.
* **보안 개선**  
보안 설정을 모니터링하고 취약점을 파악하여 개선할 수 있음.
* **운영 효율성**  
저장소 관리를 자동화하여 운영 효율성을 높일 수 있음.

### 단점
* **비용**  
프리미엄 지표와 권장 사항을 사용하려면 추가 비용이 발생할 수 있음.
* **복잡성**  
대규모 환경에서는 설정과 관리가 복잡할 수 있음.

### 아키텍처
* **데이터 수집기**  
S3 Storage Lens는 정기적으로 S3 API를 호출하여 사용량 및 활동 데이터를 수집.
* **분석 엔진**  
수집된 데이터를 분석하고, 지표와 권장 사항을 생성.
* **대시보드 및 보고서**  
분석 결과를 시각화하여 대시보드와 보고서 형태로 제공.

### Use Case

* **엔터프라이즈 데이터 관리**  
대규모 엔터프라이즈 환경에서 여러 계정과 리전의 S3 사용량을 통합적으로 관리할 수 있음.
* **애플리케이션 성능 최적화**    
애플리케이션의 데이터 접근 패턴을 분석하여 성능 최적화를 진행할 수 있음.
* **보안 감사 및 개선**  
정기적인 보안 감사를 통해 S3 버킷과 객체의 보안 설정을 개선할 수 있음.

## Metrics

Amazon S3 Storage Lens는 다양한 메트릭을 통해 사용자가 S3 버킷 및 객체 스토리지 사용을 분석하고 최적화할 수 있도록 도와줌.

1. **Summary Metrics** (요약 메트릭)  
Summary Metrics는 S3 **사용량과 활동의 요약 정보**를 제공. 
    * **Total Storage** (총 저장 용량)  
    모든 S3 버킷에 저장된 데이터의 총량.
    * **Total Object Count** (총 객체 수)  
    모든 S3 버킷에 저장된 객체의 총 수.
    * **Total Request Count** (총 요청 수)  
    모든 S3 버킷에서 수행된 총 요청 수.

2. **Cost-Optimization Metrics** (비용 최적화 메트릭)
Cost-Optimization Metrics는 S3 비용을 최적화하는 데 도움이 되는 정보를 제공.
    * **Storage Class Analysis** (저장 클래스 분석)  
    서로 다른 S3 저장 클래스(예: Standard, Intelligent-Tiering, Glacier 등) 간의 데이터 분포.
    * **Unaccessed Data** (비액세스 데이터)  
    지정된 기간 동안 접근되지 않은 데이터의 양.

3. **Data Protection Metrics** (데이터 보호 메트릭)  
Data Protection Metrics는 데이터 보호 및 백업 상태를 모니터링. 

    * **Replication Status** (복제 상태)  
    복제가 설정된 객체의 상태.
    * **Encryption Status** (암호화 상태)  
    암호화된 데이터의 비율.
    * **Lifecycle Transition Count** (수명 주기 전환 수)  
    수명 주기 정책에 따라 전환된 객체의 수.

4. **Access Management Metrics** (액세스 관리 메트릭)  
Access Management Metrics는 S3 버킷과 객체에 대한 액세스 제어 상태를 보여줌.

    * **Public Access** (공용 액세스)  
    공용으로 액세스 가능한 버킷과 객체의 수.
    * **Bucket Policies** (버킷 정책)  
    버킷 정책이 적용된 버킷의 수.
    * **Access Control Lists** (ACLs)  
    ACL이 설정된 객체의 수.

5. **Event Metrics** (이벤트 메트릭)  
Event Metrics는 S3 이벤트 관련 정보를 제공.

    * **Event Notifications** (이벤트 알림)  
    S3 이벤트 알림이 설정된 버킷의 수.
    * **Triggered Events** (트리거된 이벤트)  
    지정된 기간 동안 트리거된 S3 이벤트의 수.

6. **Performance Metrics** (성능 메트릭)  
Performance Metrics는 S3 버킷과 객체의 성능 관련 정보를 제공.

    * **Request Latency** (요청 지연 시간)  
    S3 요청의 평균 지연 시간.
    * **Throughput** (처리량)  
    시간당 처리된 데이터의 양.

7. **Activity Metrics** (활동 메트릭)  
Activity Metrics는 S3 버킷과 객체의 활동 관련 정보를 제공.

    * **Read Requests** (읽기 요청)  
    S3에서 수행된 읽기 요청의 수.
    * **Write Requests** (쓰기 요청)  
    S3에서 수행된 쓰기 요청의 수.
    * **Delete Requests** (삭제 요청)  
    S3에서 수행된 삭제 요청의 수.

8. **Detailed Status Code Metrics** (상세 상태 코드 메트릭)  
Detailed Status Code Metrics는 S3 요청의 성공 및 실패 상태 코드에 대한 상세 정보를 제공.

    * **Success Codes** (성공 코드)  
    성공적으로 완료된 요청의 상태 코드.
    * **Error Codes** (오류 코드)  
    실패한 요청의 상태 코드 (예: 4xx, 5xx 에러 코드).

이러한 다양한 메트릭을 통해 Amazon S3 Storage Lens는 사용자가 S3 스토리지 사용을 효과적으로 모니터링하고 최적화할 수 있도록 도와줌. 각 메트릭 범주는 특정한 관리 및 최적화 영역에 집중하여 데이터 관리에 필요한 인사이트를 제공함.

## Architecture Example

![Storage Lens Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/eeb18c53-782b-4ea5-8cb3-ed956c688192)