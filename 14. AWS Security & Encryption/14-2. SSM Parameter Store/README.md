# [SSM Parameter Store](https://docs.aws.amazon.com/ko_kr/systems-manager/latest/userguide/systems-manager-parameter-store.html)

## <img src = "https://github.com/user-attachments/assets/1e903f46-4aff-451e-9f84-5c87ebdb1c0c" width = "25" height = "25"> SSM Parameter Store

AWS Systems Manager Parameter Store는 **애플리케이션의 구성 데이터를 안전하게 저장하고 관리하는 AWS 서비스**임. 

이를 통해 **비밀번호, 데이터베이스 연결 문자열, AMI ID, 라이선스 키 등의 중요한 데이터를 중앙에서 관리하고, 필요한 경우 애플리케이션에 안전하게 제공**할 수 있음.

**서버리스** 서비스이며, 확장 가능하고 내결함성이 있는 SDK임.

**IAM**을 통해서 보안 설정할 수 있음.

**Amazon EventBridge**를 사용하여 파라미터의 변경 등을 알릴 수 있음.

**CloudFormation**과 통합될 수 있음.

## 특징

### 안전한 저장소

암호화된 데이터와 일반 텍스트 데이터를 안전하게 저장 가능함.

### 버전 관리

**파라미터 값에 대한 버전 관리 기능을 제공하여 변경 내역을 추적**할 수 있음.

### 정책 및 권한

**AWS IAM을 통해 파라미터에 대한 세부 권한 설정이 가능**함.

### 알림 및 감사

**AWS CloudTrail을 사용하여 파라미터 변경을 모니터링하고 감사**할 수 있음.

### 다양한 형식 지원

문자열, 문자열 목록, 안전 문자열(SecureString) 등 다양한 형식의 파라미터를 지원함.

### 호환성

AWS Lambda, Amazon EC2, AWS CloudFormation 등 여러 AWS 서비스와 통합하여 사용할 수 있음.

## 구성요소

* **파라미터**

    저장할 데이터 단위로, 이름과 값을 가짐.

* **파라미터 유형**

    **String**: 일반 텍스트 데이터.

    **StringList**: 쉼표로 구분된 문자열 목록.

    **SecureString**: AWS KMS(Key Management Service)를 사용하여 암호화된 문자열.

* **파라미터 버전**

    각 파라미터는 변경될 때마다 버전이 매겨짐.

* **파라미터 정책**

    파라미터의 생명주기와 접근 제어를 정의하는 정책.

## SSM Parameter Store Hierarchy

SSM Parameter Store Hierarchy는 파라미터를 **계층적(혹은 트리 구조)으로 구성하여 관리하는 방식**임. 

이를 통해 파라미터를 **논리적으로 그룹화하고, 쉽게 관리하고 검색**할 수 있음. 

파라미터 이름에 슬래시(/)를 사용하여 계층 구조를 정의함.

### Example

> /MyApp/Database/Hostname  
> /MyApp/Database/Port  
> /MyApp/Secrets/DBPassword  
> /MyApp/Config/MaxConnections  

위 예시에서 /MyApp이 루트 파라미터이고, 그 하위에 여러 파라미터가 계층적으로 구성되어 있음.


## 아키텍처

### 파라미터 생성 및 저장

사용자 또는 애플리케이션이 AWS Management Console, AWS CLI, AWS SDK를 통해 파라미터를 생성하고 값을 저장함.

### 암호화 및 저장

SecureString 파라미터는 AWS KMS로 암호화하여 저장됨.

### 파라미터 접근

애플리케이션이 파라미터 값을 요청하면, IAM 정책에 따라 접근 권한이 확인된 후 값을 반환함.

## 장점

* **중앙 집중 관리**

    애플리케이션 구성 데이터를 중앙에서 관리하여 일관성을 유지할 수 있음.

* **보안 강화**

    중요한 데이터를 암호화하여 저장하고, 세부 권한 설정을 통해 접근을 제어할 수 있음.

* **유연한 통합**

    다양한 AWS 서비스와 쉽게 통합할 수 있음.

* **자동화 지원**

    **AWS Lambda, AWS Step Functions 등과 통합**하여 자동화된 워크플로우를 구현할 수 있음.

## 단점

* **비용**

    대규모 데이터를 관리할 경우, 특히 암호화된 파라미터를 많이 사용할 경우 비용이 증가할 수 있음.

* **복잡성**

    IAM 정책을 통해 세부 권한을 설정하고 관리하는 데 추가적인 노력이 필요할 수 있음.

## Use case

* **애플리케이션 구성 관리**

    애플리케이션의 **구성 데이터를 중앙에서 관리하고, 변경 사항을 쉽게 적용**할 수 있음.

* **비밀 관리**

    비밀번호, API 키 등의 중요한 데이터를 안전하게 저장하고, 필요한 경우 안전하게 제공할 수 있음.

* **자동화된 워크플로우**

    **AWS Lambda와 통합하여, 파라미터 변경 시 자동으로 특정 작업을 수행하도록 설정**할 수 있음.

## Summary

AWS Systems Manager Parameter Store는 **애플리케이션 구성 데이터를 중앙에서 안전하게 관리할 수 있는 서비스**임. 

**다양한 파라미터 유형을 지원하고, IAM을 통해 세부 권한을 설정하여 보안을 강화**할 수 있음. 

여러 AWS 서비스와 통합하여 유연하게 사용할 수 있으며, 특히 중요한 데이터의 관리에 유용함.

다만, 대규모 데이터 관리 시 비용과 관리 복잡성이 증가할 수 있으므로 적절한 계획과 관리가 필요함.