# Serverless

Serverless는 **개발자가 서버를 프로비저닝, 스케일링 및 관리하지 않고도 코드를 실행하고 서비스를 구축할 수 있는 컴퓨팅 모델**임.  

서버리스 아키텍처에서는 **인프라 관리를 AWS가 담당**하며, 개발자는 애플리케이션 코드와 비즈니스 로직에 집중할 수 있음.

서버리스라고 해서, 서버가 존재하지 않는 다는 것이 아니라 인프라에 대한 노력을 최소로 하고 개발에 집중할 수 있다는 것을 의미.

## AWS 내에서 Serverless로 구현된 것들

### AWS Lambda

**이벤트에 응답하여 코드를 실행하는 컴퓨팅 서비스**임.  

코드를 작성하고, 이벤트 소스와 연계하여 트리거하면 **Lambda가 자동으로 코드를 실행**함.

* **아키텍처**  
사용자는 Lambda 함수를 작성하고, 이를 트리거할 이벤트 소스를 설정함. Lambda는 이벤트가 발생하면 자동으로 함수를 실행하며, 실행 후에는 자원을 자동으로 관리함.


### Amazon API Gateway

**RESTful API**와 **WebSocket API**를 생성하고 관리할 수 있는 서비스임.  

AWS Lambda와 통합되어 서버리스 백엔드를 제공함.

* **아키텍처**  
API Gateway는 API 요청을 받아서, 해당 요청을 처리하기 위해 **Lambda 함수나 다른 백엔드 서비스로 전달**함. API Gateway는 인증, 권한 부여 및 요청/응답 변환을 처리함.

### AWS Fargate

**컨테이너를 서버리스로 실행할 수 있는 서비스**임.  

ECS나 EKS와 통합되어 컨테이너 기반 애플리케이션을 손쉽게 배포하고 관리할 수 있음.

* **아키텍처**  
사용자는 컨테이너 정의를 작성하고, **Fargate가 자동으로 인프라를 관리**하며 컨테이너를 실행함. Fargate는 컨테이너의 프로비저닝, 스케일링 및 인프라 관리를 자동화함.

### Amazon EventBridge

**서버리스 이벤트 버스 서비스**로, 다양한 소스에서 이벤트를 수집하고 이를 대상으로 라우팅하여 애플리케이션 간의 통합을 가능하게 함.

* **아키텍처**  
EventBridge는 이벤트 소스로부터 이벤트를 수집하고, 이벤트 룰에 따라 적절한 대상(Lambda 함수, SQS 큐 등)으로 이벤트를 전달함.

### AWS Step Functions

복잡한 **워크플로우를 서버리스 방식으로 구성할 수 있는 서비스**임.  
상태 기계를 사용하여 Lambda 함수, ECS 작업 등을 조정함.

* **아키텍처**  
Step Functions는 워크플로우 정의를 통해 상태 기계를 설정하고, 각 단계별로 Lambda 함수나 다른 서비스 호출을 조정함. 상태와 실행 흐름을 관리하여 복잡한 비즈니스 로직을 구현함.

### 그 외

* **DynaoDB**
* **AWS Cognito**
* **[Amazon S3](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3)**
* **[AWS SNS](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-2.%20Amazon%20SNS)**
* **[AWS SQS](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-1.%20Amazon%20SQS)**
* **[AWS Kinesis Data Firehose](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-4.%20AWS%20Kinesis/8-4-2.%20Kinesis%20Data%20Firehose)**
* **[Aurora](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-2.%20Amazon%20Aurora) Serverless**
