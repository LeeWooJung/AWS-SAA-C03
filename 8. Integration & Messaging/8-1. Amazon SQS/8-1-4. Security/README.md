# Security

* Amazon Simple Queue Service (SQS)의 보안은 **데이터의 보호와 접근 제어를 포함한 여러 측면에서 제공**됨.  

## 데이터 암호화

### 데이터 전송 중 암호화 (Encryption in Transit)

* **SSL/TLS**  
    * 클라이언트와 SQS 간의 통신은 **SSL/TLS 프로토콜을 사용하여 암호화**됨.  
    * 이를 통해 전송 중인 데이터가 가로채지거나 변조되지 않도록 보호됨.

### 데이터 저장 중 암호화 (Encryption at Rest)  

* **SSE (Server-Side Encryption)**  
    * SQS는 **서버 측 암호화를 제공하여 큐에 저장된 메시지를 자동으로 암호화**함.  
    * **SSE-SQS** 
        AWS 관리형 키를 사용하여 메시지를 암호화함.  
        이 옵션을 사용하면 사용자가 별도로 키를 관리할 필요가 없음.
    * **SSE-KMS**  
        AWS Key Management Service (KMS)를 사용하여 메시지를 암호화함.  
        사용자는 KMS를 통해 키를 관리하고, 키 정책을 설정하여 액세스를 제어할 수 있음.
## 액세스 관리

### IAM (Identity and Access Management)

* **IAM 정책**  
    * **IAM 정책**을 사용하여 SQS 큐에 대한 액세스를 제어함.  
    * 사용자, 그룹, 역할에 대해 큐에 대한 허용 또는 거부 권한을 설정할 수 있음.  
    * 예를 들어, 특정 사용자가 메시지를 보내거나 받을 수 있는 권한을 부여할 수 있음.
* **조건부 액세스**  
    * **특정 조건이 충족될 때만 액세스를 허용하는 정책**을 설정할 수 있음.  
    * 예를 들어, 특정 IP 주소에서만 큐에 접근할 수 있도록 제한할 수 있음.

### SQS 정책 (Queue Policy)

* **큐 정책**  
    * 큐에 직접 적용되는 정책으로, 큐에 대한 액세스를 제어함.  
    * SQS 정책은 IAM 정책과 유사하지만, **큐 자체에 직접 적용**됨.  
    * 예를 들어, 특정 AWS 계정만 큐에 메시지를 보낼 수 있도록 제한할 수 있음.

## 네트워크 보호

### VPC 엔드포인트

* **VPC 엔드포인트**  
    * SQS 큐를 Virtual Private Cloud (VPC) 내에서 사용할 수 있도록 함.  
    * 이를 통해 VPC 내의 리소스가 SQS 큐에 안전하게 접근할 수 있음.
* **엔드포인트 정책**  
    * VPC 엔드포인트에 적용되는 정책으로, 엔드포인트를 통해 SQS 큐에 접근할 수 있는 권한을 제어함.

## 모니터링 및 감사

### AWS CloudTrail
* **CloudTrail 로그**  
    * SQS API 호출을 **로그로 기록하여 누가 언제 어떤 액션을 수행했는지 추적**할 수 있음.  
    * 이를 통해 보안 이벤트를 감시하고 감사할 수 있음.

### Amazon CloudWatch
* **CloudWatch 알람**  
    * SQS 큐와 관련된 메트릭을 모니터링하고, **특정 임계값을 초과할 때 알람을 설정**할 수 있음.  
    * 이를 통해 큐의 상태를 실시간으로 감시하고, 이상 행동을 탐지할 수 있음.

## Sumary

* **SSL/TLS**  
데이터 전송 중 암호화
* **SSE-SQS/SSE-KMS**  
데이터 저장 중 암호화
* **IAM 정책**  
사용자, 그룹, 역할에 대한 액세스 제어
* **큐 정책**  
큐에 직접 적용되는 액세스 제어
* **VPC 엔드포인트**  
안전한 VPC 내 액세스
* **CloudTrail 로그**  
API 호출 기록 및 감사
* **CloudWatch 알람**  
메트릭 모니터링 및 알람 설정