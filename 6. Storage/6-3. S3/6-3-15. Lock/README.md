# [S3 Lock](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/object-lock.html)

## S3 Object Lock

* S3 Object Lock은 S3 객체를 삭제 또는 변경되지 않도록 보호하는 기능임.
* S3의 Versioning이 가능해야만 적용할 수 있음.  
* 이를 통해 데이터의 **무결성을 보장하고 규제 준수를 지원**할 수 있음.

### 개념

* **WORM** (Write Once, Read Many)  
  * 데이터를 **한 번만 작성할 수 있고 이후에는 읽기만 가능하게 하는 모델**임.
* **Retention Period**  
  * 객체가 변경되거나 삭제되지 않도록 잠금 상태로 유지되는 기간.
* **Legal Hold**  
  * 객체가 일정 기간 동안 삭제되지 않도록 하는 기능으로, 특정 법적 요구사항을 충족하기 위해 사용됨.
  * 해당 기간동안은 retention period와 관계없이 작동함.

### Retention Mode

* **Compliance Mode**  
객체는 잠금 기간 동안 **어떠한 사용자**(Root User 포함)도 삭제하거나 변경할 수 없음.
* **Governance Mode**  
객체를 소유한 AWS 계정의 사용자는 권한을 부여받은 경우 객체를 삭제할 수 있음.

### 장점

* **데이터 무결성**  
규정된 기간 동안 데이터가 변경되지 않도록 보장함.
* **규제 준수**  
금융, 건강 등 규제가 요구하는 데이터 보존 요구사항을 충족함.
* **유연성**  
Legal Hold 및 Retention Period를 통해 다양한 보존 요구사항을 충족할 수 있음.

### Use Case

* **금융 기록 보관**  
법적 요구사항을 충족하기 위해 금융 기록을 보호함.
* **로그 데이터 보존**  
감사 목적으로 로그 데이터를 일정 기간 동안 보호함.

## Amazon S3 Glacier Vault Lock

* Amazon S3 Glacier 볼트에 저장된 데이터에 대해 WORM (Write Once, Read Many) 정책을 적용하여 데이터를 일정 기간 동안 변경하거나 삭제할 수 없도록 보호하는 기능임.

### 개념

* **Vault**  
데이터 아카이빙을 위해 사용되는 컨테이너로, 여러 아카이브를 저장할 수 있음.
* **Vault Lock Policy**  
특정 Vault에 대한 보존 정책을 정의하고 적용하는 규칙임.
* **Retention Period**  
Vault에 저장된 데이터가 보호되는 기간.

### 특징

* **Compliance Enforcement**  
Vault Lock 정책이 적용된 후에는 **어떠한 사용자도 정책을 변경할 수 없음**.
* **Auditing**  
Vault Lock은 감사 및 규제 준수를 위해 설계됨.

### 장점

* **강력한 보존 정책**  
데이터가 규정된 기간 동안 변경되지 않도록 보장함.
* **규제 준수**  
법적 및 규제 요구사항을 충족하기 위해 데이터를 보호함.
* **정책 고정**  
정책이 한 번 적용되면 변경할 수 없어 데이터 무결성을 보장함.

### Use Case

* **장기 아카이빙**  
법적 요구사항을 충족하기 위해 장기 데이터 보존.
* **감사 및 규제 준수**  
감사 및 규제 요구사항을 충족하기 위해 데이터 보호.