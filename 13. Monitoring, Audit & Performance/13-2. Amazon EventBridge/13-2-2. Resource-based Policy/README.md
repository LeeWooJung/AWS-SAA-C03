# [Resource Based Policy](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-use-resource-based.html)

Amazon EventBridge의 Resource-based Policy는 **특정 리소스에 대한 액세스 권한을 제어하는 정책**임. 

이를 통해 **특정 AWS 계정, IAM 사용자 또는 역할이 EventBridge 리소스에 접근할 수 있는 권한을 명시적으로 부여**할 수 있음. 

Resource-based Policy는 **주로 여러 계정 간의 리소스 공유를 위해 사용되며, 중앙 관리 및 세밀한 권한 관리를 가능**하게 함.

Resource-based Policy는 AWS 계정 간의 안전한 리소스 공유를 가능하게 함.

## 특징

### 세밀한 액세스 제어

특정 리소스에 대한 액세스 권한을 세밀하게 제어할 수 있음.

### 계정 간 리소스 공유

여러 AWS 계정 간에 EventBridge 리소스를 공유할 수 있음.

### 정책 기반 관리

JSON 형식의 정책을 사용하여 액세스 제어를 중앙에서 관리할 수 있음.

### 권한 부여 및 제한

특정 작업에 대한 권한을 부여하거나 제한할 수 있음.

## 구성요소

* **정책 문서**(Policy Document)

    JSON 형식으로 작성된 정책 문서로, 리소스에 대한 액세스 권한을 정의함.

* **주체**(Principal)

    정책에 의해 권한이 부여되는 AWS 계정, IAM 사용자, 또는 역할임.

* **작업**(Actions)

    정책에서 허용하거나 거부하는 EventBridge 작업임. 
    
    예: PutRule, PutTargets, DeleteRule 등.

* **리소스**(Resources)

    정책이 적용되는 EventBridge 리소스임.

* **조건**(Conditions)

    정책의 적용 조건을 정의하여, 특정 조건을 만족하는 경우에만 권한을 부여함.

## 아키텍처

### 정책 생성

리소스 소유자는 JSON 형식의 정책 문서를 작성하여 특정 리소스에 대한 액세스 권한을 정의함.

### 정책 적용

작성된 정책은 EventBridge 리소스에 적용됨.

### 액세스 요청

특정 AWS 계정, IAM 사용자 또는 역할이 EventBridge 리소스에 접근을 시도함.

### 정책 평가

EventBridge는 요청을 받은 정책을 평가하여 액세스를 허용할지 결정함.

### 액세스 제어

정책에 따라 액세스를 허용하거나 거부함.

## Example

``` json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123456789012:root"
      },
      "Action": "events:PutEvents",
      "Resource": "arn:aws:events:us-west-2:098765432109:event-bus/default"
    }
  ]
}
```

* **Version**

    정책의 버전임. 
    
    2012-10-17은 가장 최근의 정책 언어 버전임.

* **Statement**

    하나 이상의 권한 부여나 거부 문장을 포함함.

    * **Effect**
    
        이 정책이 허용(Allow) 또는 거부(Deny)인지 정의함.

    * **Principal**
    
        정책의 적용 대상을 정의함. 
        
        여기서는 AWS 계정 123456789012의 루트 사용자를 지정함.

    * **Action**
    
        허용하거나 거부할 작업을 정의함. 
        
        여기서는 **events:PutEvents** 작업을 허용함.

    * **Resource**
    
        정책이 적용되는 리소스를 정의함.
        
        여기서는 **arn:aws:events:us-west-2:098765432109:event-bus/default** 리소스를 지정함. 
        
        이 ARN은 이벤트 버스를 나타내며, AWS 리전과 계정 번호를 적절히 변경해야 함.

## 장점

* **세밀한 권한 관리**

    리소스에 대한 세밀한 권한 관리를 통해 보안을 강화할 수 있음.

* **중앙 집중 관리** 

    정책을 중앙에서 관리하여 여러 계정 간의 일관된 액세스 제어를 유지할 수 있음.

* **유연성**

    다양한 조건과 주체를 설정하여 유연한 권한 관리를 구현할 수 있음.

* **보안 강화**

    특정 리소스에 대한 액세스를 제한하여 보안을 강화할 수 있음.

## 단점

* **정책 관리 복잡성**

    복잡한 정책을 작성하고 관리하는 데 어려움이 있을 수 있음.

* **오류 가능성**

    잘못된 정책 설정으로 인해 예상치 못한 액세스 제어 문제가 발생할 수 있음.

* **정책 평가 지연**

    복잡한 조건을 평가하는 과정에서 약간의 지연이 발생할 수 있음.

## Use case

* **계정 간 이벤트 공유**

    여러 AWS 계정에서 동일한 EventBridge 이벤트 버스를 사용하여 이벤트를 공유할 때.

* **협력 프로젝트**

    여러 팀 또는 계정이 협력하여 작업할 때 특정 리소스에 대한 접근 권한을 부여함.

* **멀티테넌시 환경**

    단일 EventBridge 리소스를 여러 테넌트가 사용하는 멀티테넌시 환경에서 리소스 액세스를 제어함.

* **이벤트 통합**

    Single AWS 계정 또는 AWS Region에서 AWS Organization에 속한 것들의 모든 이벤트를 통합할 때.

## Summary

Amazon EventBridge의 Resource-based Policy는 **특정 리소스에 대한 액세스 권한을 제어하는 IAM 정책**임. 

이를 통해 특정 **AWS 계정, IAM 사용자, 또는 역할에게 EventBridge 리소스에 대한 액세스 권한을 부여할 수 있으며, 세밀한 권한 관리와 여러 계정 간의 리소스 공유를 가능**하게 함. 

정책 기반의 중앙 관리, 유연한 권한 설정, 보안 강화 등의 장점을 제공하며, 계정 간 이벤트 공유, 협력 프로젝트, 멀티테넌시 환경 등 다양한 사용 사례에서 활용될 수 있음.