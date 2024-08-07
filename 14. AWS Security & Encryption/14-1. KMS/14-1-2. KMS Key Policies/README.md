# [KMS Key Policies](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html)

KMS Key Policies는 **AWS KMS에서 키에 대한 접근을 제어하는 핵심 요소**임(S3 Bucket Policies와 유사). 

이는 특정 키에 대해 **어떤 주체(사용자, 역할, 서비스 등)가 어떤 작업을 수행할 수 있는지를 정의하는 정책 문서**임.

### 주요 특징

* **정책 문서 형식**

    JSON 형식으로 작성되며, IAM 정책과 유사한 구조를 가짐.

* **권한 부여**

    키에 대한 접근 권한을 부여하거나 제한할 수 있음.

* **중앙 집중 관리**

    KMS 키 정책을 통해 키에 대한 접근 제어를 중앙에서 관리할 수 있음.

* **상세한 제어**

    특정 주체가 수행할 수 있는 작업을 세밀하게 제어 가능함.

## Default KMS Key Policies

Default KMS Key Policies는 **AWS KMS에서 새 키를 생성할 때 자동으로 생성되는 기본 정책**임. 

이 정책은 **키 생성 시 사용자에게 기본적인 접근 권한을 부여**하고, **키 관리를 위한 최소한의 권한**을 포함함.

### 특징

* **자동 생성**

    키 생성 시 자동으로 생성됨.

* **기본 권한 제공**

    키 소유자에게 기본적인 관리 권한을 부여함.

* **IAM 통합**

    IAM 정책과 결합하여 사용할 수 있음.

## Customer KMS Key Policies

Custom KMS Key Policies는 **사용자가 직접 작성하고 설정하는 정책**임. 

이는 **특정 요구사항에 맞게 키에 대한 접근 권한(Users, Roles)을 세밀하게 제어**할 수 있도록 함.

Key를 누가 관리할 수 있는지 정의해야함.

KMS Key에 **Cross-account** Access을 적용하기 유용함.

### 특징

* **사용자 정의**

    사용자가 필요에 따라 정책을 작성하고 수정할 수 있음.

* **세부 제어**

    키에 대한 접근 권한을 세밀하게 설정 가능함.

* **높은 유연성**

    다양한 사용 사례에 맞게 정책을 조정할 수 있음.