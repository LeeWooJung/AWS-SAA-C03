# [S3 MFA Delete](https://docs.aws.amazon.com/AmazonS3/latest/userguide/MultiFactorAuthenticationDelete.html)

## S3 MFA Delete

* **MFA Delete**는 Amazon S3에서 다단계 인증(Multi-Factor Authentication, MFA)을 사용하여 객체 삭제 작업을 보호하는 기능임.  
* 이를 통해 추가적인 보안 레이어를 제공하여, 실수나 악의적인 삭제를 방지할 수 있음.

* **다단계 인증**(MFA)  
사용자가 일반적으로 알고 있는 정보(비밀번호) 외에도 사용자가 **소유한 물리적 장치**(예: MFA 기기 또는 모바일 앱)를 사용하여 인증을 수행하는 보안 프로세스.  
* **버킷 버전 관리**(Versioning)  
S3 버킷에서 객체의 여러 버전을 유지할 수 있는 기능.  
**MFA Delete는 버전 관리가 활성화된 버킷에서만 사용 가능**함.

### 특징

* MFA Delete는 **버전 관리가 활성화된 버킷에서만 설정 가능**함.  
* **버킷 소유자만**이 MFA Delete를 활성화하거나 비활성화할 수 있음.  
* 객체 삭제 시, 추가적인 MFA 인증을 요구함.

### MFA Delete 설정

MFA Delete를 활성화하기 위해서는 **AWS CLI**를 사용하여 설정해야 함.  
**콘솔에서는 직접 설정할 수 없음**.

* **MFA Delete 활성화**  
  ```sh
  aws s3api put-bucket-versioning --bucket <bucket-name> --versioning-configuration Status=Enabled,MFADelete=Enabled --mfa "arn:aws:iam::<account-id>:mfa/<mfa-device> <mfa-code>"
  ```
  * bucket-name: 버킷 이름.
  * account-id: AWS 계정 ID.
  * mfa-device: MFA 장치의 ARN.
  * mfa-code: MFA 장치에서 생성된 6자리 코드.

* **MFA Delete 비활성화**  
  ```sh
  aws s3api put-bucket-versioning --bucket <bucket-name> --versioning-configuration Status=Enabled,MFADelete=Disabled --mfa "arn:aws:iam::<account-id>:mfa/<mfa-device> <mfa-code>"
  ```

### 작동 방식

* **MFA Delete 활성화 후 작업**  
  * 버킷에 대해 MFA Delete가 활성화되면, 특정 작업(객체 삭제 및 버전 삭제)을 수행하기 위해 추가적인 MFA 인증이 필요함.
  * 이를 통해 **중요한 데이터가 실수로 삭제되는 것을 방지**할 수 있음.

* **객체 삭제 시도**  
  * MFA Delete가 활성화된 버킷에서 객체를 삭제하려면, MFA 인증이 요구됨.
  * 예를 들어, AWS CLI를 통해 객체를 삭제할 때 MFA 코드를 제공해야 함.

    ```sh
    aws s3api delete-object --bucket <bucket-name> --key <object-key> --mfa "arn:aws:iam::<account-id>:mfa/<mfa-device> <mfa-code>"
    ```
    * object-key: 삭제할 객체의 키

### 장점

* **보안 강화**  
다단계 인증을 통해 중요한 데이터의 삭제를 보호할 수 있음.
* **사고 방지**  
실수나 내부자 공격으로 인해 발생할 수 있는 데이터 손실을 방지할 수 있음.

### 단점

* **사용자 편의성 저하**  
추가적인 인증 단계가 필요하므로, 삭제 작업이 번거로울 수 있음.
* **복잡성 증가**  
MFA Delete 설정 및 관리가 복잡할 수 있음.

## Summary

* Amazon S3의 MFA Delete는 중요한 데이터를 보호하는 강력한 보안 기능임.  
* 이를 통해 실수나 악의적인 삭제로부터 데이터를 보호할 수 있음.  
* **버전 관리가 활성화된 버킷에서만 사용 가능**하며, 설정 및 관리는 **AWS CLI**를 통해 수행해야 함.  
* 추가적인 보안 레이어를 제공하므로, 중요한 데이터를 다루는 모든 S3 버킷에 대해 고려해볼 만한 기능임.