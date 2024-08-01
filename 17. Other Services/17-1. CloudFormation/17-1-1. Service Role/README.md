# Service Role

AWS CloudFormation의 Service Role은 **CloudFormation이 사용자 대신 스택을 생성, 업데이트, 삭제할 때 사용하는 IAM 역할**을 말함. 

이 역할은 CloudFormation이 **AWS 리소스에 접근하고 필요한 작업을 수행할 수 있도록 권한을 부여**함. 

이를 통해 CloudFormation이 적절한 권한을 갖고 작업을 수행하는지 확인할 수 있으며, 보안 및 권한 관리 측면에서 중요한 역할을 함.

CloudFormation을 이용하면 사용자가 **Stack**에 존재하는 Resource에 대한 **작업 권한이 없더라도, Stack Resource에 대해 생성, 업데이트, 삭제할 수 있는 권한을 줄 수 있음**.

## 특징

### 권한 위임

CloudFormation에 특정 권한을 위임하여 필요한 작업을 수행하게 함.

### 보안 강화

**최소 권한 원칙**을 적용하여 CloudFormation이 필요한 작업에만 접근하도록 함.

### 세밀한 제어

Service Role을 통해 CloudFormation이 어떤 작업을 수행할 수 있는지 세밀하게 제어할 수 있음.

### 로그 및 감사

CloudFormation의 활동을 추적하고 감사할 수 있도록 로그를 남길 수 있음.

## 구성요소

* **IAM 역할**

    CloudFormation이 사용할 IAM 역할을 정의함.

* **정책**

    IAM 역할에 부여된 권한을 정의하는 정책을 포함함.

* **신뢰 관계**

    CloudFormation 서비스가 역할을 가정할 수 있도록 신뢰 관계를 설정함.

## 역할 생성 및 설정 방법

### IAM 역할 생성

AWS Management Console, AWS CLI 또는 AWS SDK를 사용하여 IAM 역할을 생성함.

### 정책 첨부

역할에 필요한 권한을 정의하는 정책을 첨부함.

### 신뢰 관계 설정

CloudFormation 서비스가 역할을 가정할 수 있도록 신뢰 관계를 설정함.

### CloudFormation 템플릿에 역할 지정

CloudFormation 템플릿에서 RoleARN 속성을 사용하여 생성한 역할을 지정함.

## Summary

AWS CloudFormation의 Service Role은 **CloudFormation이 스택을 생성, 업데이트, 삭제할 때 사용하는 IAM 역할**임. 

이를 통해 CloudFormation이 **AWS 리소스에 접근하고 필요한 작업을 수행할 수 있도록 권한을 부여함으로써 보안과 권한 관리를 강화**함. 

Service Role을 사용하면 CloudFormation이 수행할 수 있는 작업과 리소스 접근 권한을 **세밀하게 제어**할 수 있으며, 설정과 관리가 필요함.