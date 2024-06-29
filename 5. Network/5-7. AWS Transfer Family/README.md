# [AWS Transfer Family](https://aws.amazon.com/ko/aws-transfer-family/)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/39b5aef7-80b5-4738-9d2c-0bb290513d89" width = "30" height = "30"> AWS Transfer Family

* Secure File Transfer Protocol (**SFTP**), File Transfer Protocol over SSL (**FTPS**), 및 File Transfer Protocol (**FTP**)을 지원하여 데이터를 **안전하게 전송하고 관리**할 수 있는 서비스임.  
* 이를 통해 기업은 기존 파일 전송 워크플로를 **AWS 스토리지 서비스(S3, EFS)와 통합**할 수 있음.

## 특징

* **프로토콜 지원**  
SFTP, FTPS, FTP 프로토콜을 지원하여 다양한 파일 전송 요구를 충족할 수 있음.
* **통합 및 호환성**  
Amazon S3 및 Amazon EFS를 FTP protocol을 사용하여 통합되어 데이터를 안전하게 저장하고 관리할 수 있음.
* **보안**  
전송 중 데이터 암호화(TLS/SSL), 사용자 인증 및 액세스 제어를 통해 높은 수준의 보안을 제공함.
* **자동화 및 관리**  
AWS Management Console, AWS CLI, AWS SDK를 통해 손쉽게 관리 및 자동화할 수 있음.
* **확장성**  
AWS 인프라의 확장성을 활용하여 필요에 따라 서비스를 확장할 수 있음.
* **가용성**  
Mult-AZ 에 설치할 수 있어 가용성을 늘릴 수 있음.

## 장점
* **손쉬운 마이그레이션**  
    * 기존 SFTP, FTPS, FTP 서버를 **AWS로 쉽게 마이그레이션**할 수 있음.
    * 기존에 사용중인 authentication systems(Microsoft Active Directory, LDAP, Okta, Amazon Cognito custom)과 통합할 수 있음.
* **높은 보안**  
전송 중 데이터 암호화 및 **IAM**을 통한 세밀한 액세스 제어를 제공함.
* **운영 효율성**  
**관리형 서비스로**서 인프라 관리 부담을 줄여주고, AWS의 다양한 서비스와 통합하여 효율성을 높일 수 있음.
* **확장성**  
AWS의 글로벌 인프라를 활용하여 필요에 따라 서비스를 쉽게 확장할 수 있음.

## 단점
* **초기 설정 필요**  
프로토콜 및 사용자 설정을 처음에 구성해야 하는 초기 작업이 필요함.
* **네트워크 의존성**  
네트워크 대역폭에 따라 전송 속도가 영향을 받을 수 있음.

## Architecture
AWS Transfer Family는 클라이언트가 SFTP, FTPS, 또는 FTP를 통해 데이터를 전송할 때, 이를 **Amazon S3 또는 Amazon EFS와 연결하여 저장**함.  
전송된 데이터는 AWS의 보안 및 컴플라이언스 기능을 통해 안전하게 관리됨.

* **클라이언트**  
파일을 전송하려는 사용자는 SFTP, FTPS, FTP 클라이언트를 사용함.
* **AWS Transfer Family 서버**  
AWS에서 제공하는 관리형 서버가 프로토콜을 처리함.
* **Amazon S3 / Amazon EFS**  
최종적으로 파일이 저장되는 위치임.  
S3는 객체 스토리지, EFS는 파일 스토리지로 사용됨.
* **IAM**  
사용자 인증 및 액세스 제어를 관리함.

## Use Case
* **데이터 마이그레이션**  
기존 온프레미스 SFTP 서버의 데이터를 클라우드로 마이그레이션할 때 유용함.
* **데이터 공유**  
파트너와 **안전하게 파일을 공유**해야 하는 경우 사용함.
* **백업 및 아카이빙**  
중요한 파일을 안전하게 전송하여 S3나 EFS에 백업 및 아카이빙할 때 유용함.

## Architecture Example

![Aws transfer family architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/5b431d2c-b6fb-43de-b43e-276b93fdacc9)
