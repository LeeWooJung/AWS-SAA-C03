# KMS Key Types

## Symmetric(AES-256 keys)

대칭 키는 **암호화와 복호화에 동일한 키를 사용하는 암호화 방식**임. 

**한 개의 비밀 키로 데이터를 암호화하고 복호화**함.

KMS Key와 통합된 AWS Services는 Symmetric CKMs를 사용함.

KMS Key가 unencrypted 된 상태에서 접근할 수 없음. 이 때는 **KMS API**를 사용하여야 함.

### 특징

* **단일 키 사용**

    암호화와 복호화에 **동일한 키를 사용**함.

* **성능**

    비대칭 키보다 암호화 및 복호화 속도가 빠름.

* **주로 사용**

    데이터 암호화, 저장된 데이터 보호 등에 많이 사용됨.

## Asymmetric(RSA & ECC key pairs)

비대칭 키는 두 개의 키, 즉 **공개 키(Public Key)와 개인 키(Private Key)를 사용**하는 암호화 방식임. 

**공개 키로 데이터를 암호화하고, 해당 데이터를 복호화할 때는 개인 키를 사용**함.

**KMS API**를 사용하지 못하는 User가 AWS Service 외부에서 공개키를 이용하여 Encryption을 진행해야 함.

### 특징

* **두 개의 키 사용**

    공개 키로 암호화하고, 개인 키로 복호화함. 반대로, 개인 키로 서명하고, 공개 키로 서명을 검증함.

* **보안성**

    공개 키는 공개되어도 되지만, 개인 키는 비밀로 유지되어야 함.

* **주로 사용**

    디지털 서명, 인증서 기반 보안 등에 사용됨.

-------------------------------


## AWS Owned Keys

AWS Owned Keys는 **AWS가 소유하고 관리하는 키로, AWS 서비스가 내부적으로 데이터를 암호화하기 위해 사용하는 키**임. 

사용자에게 직접적으로 노출되지 않음.

**무료**로 사용할 수 있으며, 종류에는 **SSE-S3, SSE-SQS, SSE-DDB** 등이 있음.

### 특징

* **자동 관리**

    AWS가 자동으로 생성하고 관리함.

* **투명성**

    사용자는 이 키를 직접 볼 수 없으며, AWS 서비스 내부에서 자동으로 사용됨.

* **용도**

    AWS 서비스 내부 데이터 보호에 사용됨.

## AWS Managed Key

AWS Managed Keys는 **특정 AWS 서비스에 의해 생성되고 관리되는 키로, 사용자는 키를 선택할 수 있지만, 관리 작업은 AWS가 수행**함.

자동으로 **매 1년**마다 Key Rotation을 진행함.

**무료**이며 다음과 같은 이름을 가짐.

> aws/service-name  
> [Example]  
> aws/rds  
> aws/ebs

### 특징

* **간편함**

    키 관리를 AWS가 처리하므로, 사용자가 직접 관리할 필요 없음.

* **서비스 통합**

    S3, EBS, RDS 등의 AWS 서비스와 통합되어 사용됨.

* **제한된 제어**

    사용자가 키에 대한 제한된 제어만 가짐.

## Customer managed keys created in KMS

Customer Managed Keys는 **사용자가 직접 생성하고 관리하는 키로, 사용자가 완전히 제어할 수 있는 키**임. 

사용자는 **키의 정책, 회전, 삭제 등을 관리**할 수 있음.

자동으로 **매 1년**마다 Key Rotation을 진행하도록 **설정 되어야함**.

요금은 **$1/month**임.

### 특징

* **완전한 제어**

    사용자가 키의 생성, 정책 설정, 회전 주기 등을 완전히 제어함.

* **고급 기능**

    IAM 정책, 키 정책 설정, 로깅 등의 고급 기능을 사용할 수 있음.

* **책임 증가**

    사용자가 직접 키를 관리해야 하므로, 책임이 증가함.

## Customer managed keys imported

Customer Managed Keys Imported는 **사용자가 외부에서 생성한 키를 AWS KMS로 가져와 사용하는 키**임. 

**사용자는 외부에서 생성된 키를 AWS KMS로 가져와서 사용**할 수 있음.

**무조건 Symmetric key**를 사용해야함.

사용자가 직접 **alias를 이용하여 rotation** 할 수 있음.

요금은 **$1/month**이며, KMS API call을 위해 **$0.03/10000calls**만큼의 비용을 지불해야함.

### 특징

* **외부 키 사용**

    사용자가 신뢰하는 외부 키를 AWS KMS로 가져와 사용할 수 있음.

* **완전한 제어**

    Customer Managed Keys와 마찬가지로, **사용자가 키의 정책, 회전, 삭제 등을 완전히 제어**할 수 있음.

* **키 수명**

    가져온 키의 수명을 사용자가 직접 관리해야 함.