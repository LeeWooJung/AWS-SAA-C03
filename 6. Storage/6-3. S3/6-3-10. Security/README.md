# [S3 Security](https://aws.amazon.com/ko/s3/security/)

## S3 Security

* Amazon S3는 데이터를 보호하기 위해 여러 가지 **암호화 옵션**을 제공.  

## 서버 측 암호화 (SSE)
* SSE는 Amazon S3가 데이터를 암호화하고 해독하는 작업을 대신 해주는 방식.

### SSE-S3 (S3 관리 키를 사용하는 서버 측 암호화)

* S3가 암호화 키를 관리(**Enabled by Default**)  
* 객체를 업로드할 때, Amazon S3는 객체를 고유한 키로 암호화하고, 이 키를 S3가 주기적으로 교체하는 마스터 키로 다시 암호화.  
* 객체를 가져올 때 S3가 자동으로 객체를 복호화.  
* Encyption type: **AES-256**
* Header: **"x-amz-server-side-encryption":"AES256"**
* **키 관리**  
완전히 Amazon S3가 관리.

### Architecture

![SSE-S3 Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/8d3467e6-a6b3-47db-8af6-7b8b862f6161)


### SSE-KMS (AWS 키 관리 서비스(KMS)를 사용하는 서버 측 암호화)

* **AWS KMS**를 사용해 암호화 키를 관리.
* 객체를 업로드할 때, S3는 고유한 데이터 키로 객체를 암호화.
* 데이터 키는 AWS KMS가 관리하는 마스터 키로 추가 암호화됨.
* 객체를 가져올 때, S3가 KMS를 사용해 데이터 키를 복호화하고, 이를 이용해 객체를 복호화함.
* Header: **"x-amz-server-side-encryption": "aws:kms"**
* **키 관리**  
    * AWS KMS가 관리하며, 추가적인 보안 기능을 제공.
    * CloudTrail을 사용하여 키 사용에 대한 감사 가능.
    * User control 가능.
* **제한 사항**  
    * 추가적인 AWS KMS 호출(**GenerateDataKey KMS API**)로 인해 지연 시간이 증가할 수 있음.
    * 객체를 다운로드 받을 때, **Decrypt KMS API**를 호출.
    * **KMS 사용에 대한 비용이 발생**, API 호출 및 키 저장 비용 포함.
    * 높은 부하 시 AWS KMS 요청 속도 제한이 성능에 영향을 미칠 수 있음.

### Architecture

![SSE-KMS Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/496a78dd-0174-4423-aa19-b0032587468b)


### SSE-C (고객 제공 키를 사용하는 서버 측 암호화)

* **사용자가 직접 암호화 키를 제공**.
* 사용자가 키를 관리하고, 객체를 **업로드하거나 다운로드할 때 S3에 제공**.
* S3는 Key를 저장하지 않음.
* **HTTPS가 무조건 사용되어야 함**.
* S3는 사용자가 제공한 키로 객체를 암호화하고 복호화.
* **키 관리**  
    * 사용자가 직접 관리.
    * 암호화된 key가 HTTP Header를 통해 제공되어야 함.

### Architecture

![SSE-C Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/398ee9d2-7dcd-4685-afd1-793bf348dd67)

## 클라이언트 측 암호화
* 클라이언트 측 암호화는 **데이터를 S3에 업로드하기 전에 클라이언트 측에서 암호화**하고, 다운로드한 후 복호화하는 방식.  
* **암호화와 복호화 키는 클라이언트가 관리**.

### Architecture

![Client-side Architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/9120c4fb-c2f5-4ab8-97cb-88bf4b803ab0)


### AWS KMS 관리 키를 사용하는 클라이언트 측 암호화 (CSE-KMS)

* AWS KMS를 사용해 데이터 암호화 키를 생성하고 관리.
* 클라이언트가 AWS KMS로부터 데이터 키를 요청하고, 이를 사용해 로컬에서 데이터를 암호화한 후 S3에 업로드.
* 데이터를 가져올 때 클라이언트가 S3에서 암호화된 데이터를 다운로드하고, KMS를 사용해 데이터 키를 복호화한 후 **로컬에서 데이터를 복호화**.

### 고객 제공 키를 사용하는 클라이언트 측 암호화 (CSE-C)

* 사용자가 직접 암호화 키를 관리.
* 사용자가 직접 암호화 키를 생성하고 관리.
* 클라이언트가 이 키로 데이터를 암호화한 후 S3에 업로드하고, 데이터를 가져올 때도 이 키로 데이터를 복호화.

## 전송 중 암호화 (SSL/TLS)
* 전송 중 암호화는 애플리케이션과 Amazon S3 간에 데이터를 전송할 때 보안을 유지.
* Amazon S3는 **HTTP Endpoint**, **HTTPS Enpoint**를 보유함.  
* HTTPS 를 사용하는 것이 권장되며, SSE-C를 사용할 경우 HTTPS는 의무적으로 사용되어야 함.
* **Bucket Policy**를 통해서 HTTP로 접근하는 것을 거부할 수 있음.
* **메커니즘**  
SSL(보안 소켓 계층)과 TLS(전송 계층 보안) 프로토콜을 사용해 데이터를 전송 중에 암호화.
* 클라이언트가 **S3에 요청을 할 때 SSL/TLS 연결을 설정**.
* 데이터는 전송 중에 **HTTPS 같은 프로토콜**을 사용해 암호화.
* 이는 중간자 공격과 도청을 방지.

## SSE 방법과 클라이언트 측 암호화 비교
* **SSE-S3**  
    * **키 관리**  
    Amazon S3가 키를 관리.
    * **사용 편의성**  
    사용자가 키를 관리할 필요 없어서, 가장 사용하기 쉬움.
    * **보안**  
    대부분의 애플리케이션에 적합, S3가 키를 주기적으로 교체함.

* **SSE-KMS**  
    * **키 관리**  
    AWS KMS가 키를 관리, 추가적인 보안 기능 제공.
    * **사용 편의성**  
    AWS KMS와의 통합 필요, **추가 비용 발생**.
    * **보안**  
    세부적인 접근 제어와 감사 기능으로 향상된 보안 제공.
    * **제한 사항**  
    지연 시간 증가와 속도 제한이 문제될 수 있음.

* **SSE-C**
    * **키 관리**  
    사용자가 직접 키를 관리.
    * **사용 편의성**  
    사용자가 키 관리와 보안을 책임져야 함.
    * **보안**  
    키 관리에 대해 가장 높은 수준의 제어 제공.

* **클라이언트 측 암호화**  
    * **키 관리**  
    클라이언트가 직접 키를 관리.
    * **보안**  
    데이터는 클라이언트가 업로드하기 전에 암호화, S3에 암호화된 상태로 저장.
    * Amazon S3의 다양한 암호화 옵션을 통해 데이터의 보안을 강화할 수 있고, 각 방법은 서로 다른 수준의 키 관리와 보안을 제공.  
    
## Default Encryption vs. Bucket Policy

* Amazon S3는 데이터를 안전하게 보호하기 위한 다양한 보안 기능을 제공함.  
* 그 중에서도 Default Encryption과 Bucket Policy는 주요한 역할을 함.

### Default Encryption
* Default Encryption은 S3 버킷에 업로드되는 모든 객체를 자동으로 암호화하는 기능.

#### 특징

* **자동화**  
사용자가 개별 객체에 암호화 설정을 지정하지 않아도 버킷에 업로드되는 모든 객체가 자동으로 암호화됨.
* 지원되는 암호화 방식: SSE-S3, SSE-KMS, SSE-C 방식이 있음.
    * **SSE-S3**  
    S3 관리 키를 사용하여 암호화됨.
    * **SSE-KMS**  
    AWS KMS 키를 사용하여 암호화됨.
    * **SSE-C**  
    고객 제공 키를 사용하여 암호화됨.
* **편리성**  
버킷 수준에서 설정하기 때문에 개별 객체 관리가 필요 없음.
* **설정 방법**  
    * AWS Management Console, AWS CLI, 또는 AWS SDK를 통해 설정할 수 있음.
    * 버킷의 속성에서 "Default Encryption" 옵션을 선택하여 활성화함.

#### 장점  
* 데이터 보호를 위한 자동화된 암호화.
* 일관된 보안 정책 적용.

### Bucket Policy (버킷 정책)
* Bucket Policy는 S3 버킷에 대한 접근 제어를 **JSON 형식**으로 정의하는 정책임.

#### 특징
* **정밀한 접근 제어**  
**특정 사용자, 역할, 또는 AWS 서비스에 대한 접근 권한**을 세부적으로 설정할 수 있음.
* **조건부 제어**  
IP 주소, VPC, MFA 사용 여부 등 다양한 조건에 기반한 접근 제어를 설정할 수 있음.
* **정책 구조**  
    * **Effect**: Allow 또는 Deny.
    * **Principal**: 정책이 적용되는 사용자 또는 역할.
    * **Action**: 허용 또는 거부할 S3 API 작업.
    * **Resource**: 정책이 적용되는 S3 리소스 (예: 버킷 또는 객체).
    * **Condition**: 조건부 제어를 위한 추가 매개변수.

#### 예시
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::example-bucket/*",
      "Condition": {
        "IpAddress": {
          "aws:SourceIp": "192.0.2.0/24"
        }
      }
    }
  ]
}
```

### 비교
|**항목**|**Default Encryption**|**Bucket Policy**|
|:---|:---|:---|
|**주요 기능**|버킷에 업로드되는 모든 객체 자동 암호화|버킷 및 객체에 대한 접근 제어|
|**설정 방법**|버킷 수준에서 암호화 방식 설정|JSON 형식의 정책 파일 설정|
|**암호화 지원**|SSE-S3, SSE-KMS, SSE-C|해당 없음|
|**조건부 제어**|조건부 제어 기능 없음|다양한 조건(IP주소, VPC등) 기반 접근 제어|
|**보안 적용 범위**|데이터 암호화(기본 암호화)|접근 권한 관리(정밀한 접근 제어)|
|**유연성**|암호화 방식에 대해 일관된 설정 적용 가능|특정 사용자, 역할, 조건에 따른 유연한 정책 설정|

**Bucket Policy는 Default Encrpytion 적용 전에 먼저 확인 됨**.