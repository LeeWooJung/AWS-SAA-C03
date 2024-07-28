# IAM Permission Boundaries

IAM Permission Boundaries는 AWS에서 **사용자 또는 역할(Not Group)에게 할당된 권한의 최대 범위를 설정하는 방법**임. 

이는 사용자가 **더 높은 수준의 권한을 부여받는 것을 방지하고, 보안 정책을 더욱 세밀하게 관리할 수 있도록 도움**을 줌.

## 특징

### 최대 권한 한정

Permission Boundaries는 사용자나 역할이 가질 수 있는 **최대 권한을 정의**함.

### 정책 조합

사용자의 실제 권한은 **Permission Boundaries와 사용자에게 부여된 IAM 정책의 교집합으로 결정**됨.

즉, 사용자가 부여받은 권한이 Permission Boundaries 내에 있어야 실제로 권한을 사용할 수 있음.

또한, **AWS Organizations SCP**와도 결합될 수 있음.

### 정책 유형

JSON 형식으로 작성된 관리형 정책임.

### 적용 대상

주로 사용자 또는 역할에 적용됨.

## Use case

Permission Boundary 내에 있는 비관리자의 권한을 제거(IAM User를 새로 생성하는 등).

개발자가 정책을 자체 할당하도록 허용하고, 자신의 권한을 관리하는 **동시에** 자신의 권한을 상승시킬 수 없도록 관리.

SCP 와 AWS Organizations를 사용하는 대신 **한 명의 User**의 권한만을 제한하는 데 사용.