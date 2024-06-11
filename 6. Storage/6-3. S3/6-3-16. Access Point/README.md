# [S3 Access Point](https://aws.amazon.com/ko/s3/features/access-points/)

## S3 Access Point

* Amazon S3 Access Points는 단일 S3 버킷에 대한 데이터 액세스를 관리하고 구성하기 위한 **분리된 네트워크 엔드포인트**를 제공함. 
* 이를 통해 **애플리케이션의 데이터 접근을 쉽게 관리하고, 특정 요구 사항에 맞게 세분화된 제어를 가능**하게 함.

### 특징

* **개별 엔드포인트**  
각 Access Point는 **고유한 엔드포인트 URL**을 가지며, 특정 버킷에 대한 접근을 제공함.

* **정책 설정**  
Access Point 별로 개별 정책을 설정([Bucket Policy](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3/6-3-3.%20Security#%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%95%A1%EC%84%B8%EC%8A%A4-%EC%A0%9C%EC%96%B4)와 유사)하여 **세밀한 권한 제어**가 가능함.

* **VPC 통합**  
Virtual Private Cloud (VPC)와 통합하여 **프라이빗 네트워크 내에서 안전하게 데이터 접근이 가능**함.

* **네임스페이스 관리**  
각 Access Point는 고유한 네임스페이스(Own DNS Name)를 가지므로, 여러 애플리케이션이 같은 버킷을 동시에 사용하더라도 충돌 없이 데이터 접근이 가능함.

### 장점

* **보안 강화**  
특정 VPC에서만 접근 가능하도록 설정하여 네트워크 레벨의 보안을 강화할 수 있음.
* **유연한 접근 제어**  
각 **Access Point 별로 다른 정책을 적용**하여 다양한 애플리케이션 요구를 만족시킬 수 있음.
* **간편한 관리**  
Access Point를 통해 복잡한 버킷 정책을 간소화하고 관리하기 쉽게 함.

## VPC Origin

* VPC (Virtual Private Cloud)와 통합된 S3 Access Points는 **프라이빗 네트워크 내에서 S3 데이터에 접근**할 수 있도록 하여, 외부 인터넷을 통하지 않고 안전하게 데이터를 주고 받을 수 있게 함.

### 작동 방식

* **Access Point 생성**  
S3 버킷에 대한 Access Point를 생성하고, 해당 Access Point가 VPC와 통합되도록 설정함.
* **VPC 엔드포인트 설정**  
AWS PrivateLink를 사용하여 VPC 내에서 S3 Access Point에 접근할 수 있도록 VPC 엔드포인트를 설정함.
* **정책 적용**  
Access Point와 VPC 엔드포인트에 적절한 정책을 설정하여 필요한 권한을 부여함.

### 아키텍처

* **VPC 엔드포인트**  
S3 Access Point에 대한 네트워크 엔드포인트를 **VPC 내에 생성하여 프라이빗 네트워크 경로를 통해 S3 버킷에 접근**함.

* **Access Point 정책**  
각 Access Point 별로 정책을 설정하여 VPC 내부의 리소스가 특정 S3 버킷의 데이터에 접근할 수 있도록 허용함.

* **프라이빗 DNS**  
프라이빗 DNS를 설정하여 VPC 내에서 S3 Access Point에 대해 간편하게 접근할 수 있도록 함.

### 장점

* **보안 강화**  
인터넷을 통하지 않고, 프라이빗 네트워크 내에서 안전하게 S3 데이터에 접근 가능.
* **네트워크 성능**  
VPC 내에서 직접 데이터 접근이 가능하여 지연 시간이 감소하고 성능이 향상됨.
* **정책 관리**  
Access Point를 통해 세분화된 정책을 설정하여 더욱 세밀한 접근 제어가 가능.

### Use Case

* **내부 애플리케이션**  
기업 내부 애플리케이션이 S3 버킷의 데이터를 사용할 때 VPC 내에서만 접근 가능하도록 설정하여 **데이터 유출을 방지**.
* **데이터 분석**  
VPC 내에서 데이터 분석 작업을 수행하는 경우, 분석 애플리케이션이 S3 데이터에 안전하게 접근 가능하도록 설정.