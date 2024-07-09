# [AWS Lambda](https://aws.amazon.com/ko/elasticbeanstalk/?gclid=CjwKCAjwvIWzBhAlEiwAHHWgvTo_7t2fB17IG7otWlErbDhhivGfiQD5K90-JuWtCxszeRmvFFOFQhoCQGoQAvD_BwE&trk=3d211853-d899-491e-bd5a-fb5f17de6f0f&sc_channel=ps&ef_id=CjwKCAjwvIWzBhAlEiwAHHWgvTo_7t2fB17IG7otWlErbDhhivGfiQD5K90-JuWtCxszeRmvFFOFQhoCQGoQAvD_BwE:G:s&s_kwcid=AL!4422!3!651510175878!e!!g!!amazon%20elastic%20beanstalk!19835789747!147297563979)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/5f32a96e-c352-48d9-9a1b-8179e3b46dd7" width = "25" height = "25"> AWS Lambda

AWS Lambda는 이벤트에 응답하여 코드를 실행하는 서버리스 컴퓨팅 서비스임.

**EC2를 사용할 때와 Lambda를 사용할 때의 차이점**

||AWS EC2|**AWS Lambda**|  
|:---|:---|:---|  
|서버 관리|Virtual Server, 인프라 직접 관리|Virtual Function, 서버관리 필요 없음|  
|비용|인스턴스 실행 시간동안 비용 지불|코드 실행 시간에 따라 비용 지불|
|Scaling|수동 또는 Auto Sclaing 필요|요청 수에 따라 자동으로 Scaling|
|자원|RAM과 CPU에 따라 제한됨|짧은 실행시간을 갖기 때문에 시간에 제한됨|
|실행|EC2를 시작하면 계속 실행됨|요청이 있을 때만 실행됨|

## AWS Lambda의 장점

* **자동 스케일링**  
트래픽에 따라 **자동으로 인스턴스를 증가/감소시켜 유연하게 대응**할 수 있음.

* **무서버 관리**  
인프라 관리를 신경 쓸 필요 없이 코드를 실행할 수 있음.

* **비용 효율성**  
코드 실행 시간에 따라 비용이 발생하므로, **사용한 만큼만 지불**함.  
1,000,000 AWS Lambda 요청과 400,000 GBs의 실행시간까지는 무료로(Free Tier) 사용할 수 있음.

* **유연성**  
다양한 이벤트 소스와 통합되어 **이벤트 기반의 애플리케이션을 쉽게 구축**할 수 있음.

* **통합성**
대부분의 AWS Service와 통합되어 사용될 수 있음.  
많은 프로그래밍 언어로 Lambda를 작성할 수 있음.

* **자원 확보**  
Function마다 10GB of RAM 만큼의 자원을 쉽게 얻을 수 있음.

* **보안**  
AWS Identity and Access Management (IAM)와 통합되어, 세밀한 권한 관리를 제공함.  
AWS CloudWatch를 통해서 쉽게 모니터링할 수 있음.

## 지원 언어

* **Node.js**(JavaScript)
* **Python**
* **Java**(Java 8 compatible)
* **C#**(.NET Core)
* **Golang**
* **C#**/**Powershell**
* **Ruby**
* **Custom RuntimeAPI**
* **Container**  
    AWS Lambda는 컨테이너 이미지를 사용하여 배포할 수 있음. Docker 이미지를 Lambda에 배포하여, 맞춤형 런타임과 라이브러리를 사용할 수 있음.  
    ECS/Fargate가 임의의 도커 이미지를 실행시키는데 선호됨.

## Integrate with AWS Service

* **Amazon S3**: 객체가 생성/수정될 때 트리거로 사용 가능.  
* **Amazon DynamoDB**: 테이블 변경 스트림을 트리거로 사용 가능.
* **Amazon SNS**: 주제에 메시지가 게시될 때 트리거로 사용 가능.  
* **Amazon SQS**: 메시지가 큐에 도착할 때 트리거로 사용 가능.  
* **Amazon CloudWatch**: 이벤트, 로그 및 경보를 트리거로 사용 가능(CloudWatch Events EventBridge, CloudWath Logs).  
* **Amazon API Gateway**: HTTP 요청을 트리거로 사용 가능.  
* **AWS Step Functions**: 워크플로우 단계로 사용 가능.  
* **API Gateway**
* **Kinesis**
* **CloudFront**
* **Cognito**

## [비용](https://aws.amazon.com/lambda/pricing/)

* **Pay per calls**  
    첫 1,000,000 call은 무료임.  
    그 후, $0.20 per 1 million request 만큼의 비용을 청구함.
* **Pay per duration**  
    400,000 GB-sec of compute time per month 만큼 무료임.  
    그 후, $1.00 for 600,000 GB-sec 만큼의 비용을 청구함.

## 한계 (per Region)

### Execution

* **실행 시간 제한**

    Lambda 함수는 **최대 15분 동안만 실행**될 수 있음. 이는 짧은 시간 내에 작업을 완료해야 하는 **단기 작업에 적합하지만, 장기 실행 작업에는 적합하지 않음**.  
    대용량 데이터 처리나 복잡한 연산 작업을 수행할 때 제약이 됨.

* **메모리 제한**

    Lambda 함수의 메모리 크기는 **128MB에서 10GB**까지 설정할 수 있음. 이는 많은 메모리를 요구하는 작업에는 한계가 될 수 있음.  
    메모리 사용량이 많은 애플리케이션이나 대규모 데이터 처리에는 적합하지 않음.

* **디스크 공간 제한**

    Lambda 함수의 임시 저장소(/tmp)는 최대 **512MB ~ 10GB**로 제한됨. 이는 대용량 파일 처리나 많은 데이터를 임시 저장소에 저장해야 하는 작업에 제약이 됨.  
    데이터를 임시로 저장하고 처리해야 하는 애플리케이션에는 적합하지 않음.

* **동시 실행 제한**

    계정당 **동시 실행 가능한 Lambda 함수의 수에 제한**이 있음. 기본 동시 실행 한도는 1000개이며, 이는 AWS에 요청하여 늘릴 수 있지만 무제한은 아님.  
    고빈도 트래픽을 처리해야 하는 애플리케이션에서는 병목 현상이 발생할 수 있음.

* **Cold Start 지연**

    Lambda 함수가 오랫동안 호출되지 않으면 "Cold Start" 지연이 발생하여 **첫 번째 호출 시 지연**이 생김.  
    짧은 응답 시간이 중요한 애플리케이션에서는 Cold Start가 성능에 영향을 줄 수 있음.

### Deployment

* **패키지 크기 제한**

    Lambda 함수 코드 패키지의 크기는 **50MB**(압축 파일)로 제한되며, 함수와 함께 제공되는 종속성 라이브러리의 총 크기는 최대 **250MB**(압축 해제 파일)로 제한됨.  
    대형 애플리케이션이나 많은 종속성을 포함하는 애플리케이션에는 제약이 됨.

* **환경 변수 관리**

    Lambda 함수는 환경 변수를 통해 설정을 전달받을 수 있음. 하지만 **환경 변수의 크기와 개수에도 제한**이 있어, 많은 설정을 필요로 하는 애플리케이션에는 적합하지 않을 수 있음.  
    복잡한 설정 관리를 요구하는 애플리케이션에서 어려움이 있을 수 있음.

* **버전 관리 및 배포**

    Lambda는 함수 버전 관리를 지원하지만, 이를 **효과적으로 관리하고 배포하기 위한 도구나 프로세스가 필요**함.  
    많은 함수 버전과 환경을 관리해야 하는 애플리케이션에서 복잡성이 증가할 수 있음.

* **VPC 연결 제한**

    Lambda 함수가 VPC에 연결될 때 초기 연결 설정에 시간이 소요될 수 있음. 이는 **VPC 내의 리소스와 통합할 때 성능에 영향**을 줄 수 있음.  
    VPC 내에서 실행해야 하는 애플리케이션의 경우 네트워크 설정과 성능에 주의가 필요함.

## [Lambda SnapStart](https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/snapstart.html)

AWS Lambda SnapStart는 **Lambda 함수의 초기화 시간을 줄여서 응답 성능을 향상**시키기 위한 기능임.  

이는 특히 함수의 **콜드 스타트(cold start) 지연 시간을 감소시키는 데 중점**을 둔 기술임.  

SnapStart는 **Java 함수의 초기화를 가속화하는 데 사용**되며, 초기화 단계를 미리 실행하여 이를 캐싱하고 재사용함으로써 다음 호출 시 빠르게 처리할 수 있음.

### 주요 개념

**콜드 스타트 문제**  

Lambda 함수는 콜드 스타트 시 **코드 초기화, 라이브러리 로드, 그리고 모든 초기화 로직을 수행**해야 함.  
이는 특히 Java 함수의 경우 시간이 오래 걸릴 수 있으며, 사용자가 느끼는 지연 시간이 길어짐.

**SnapStart 동작 방식**  

SnapStart는 함수의 **초기화 단계를 미리 실행하고 그 상태를 스냅샷으로 저장**함.  

다음 호출 시에는 이 스냅샷을 재사용하여 초기화 단계를 건너뛸 수 있음.  

1. **초기화 단계**  
    함수가 처음 배포되거나 업데이트될 때 초기화가 한 번 실행되고, 그 상태가 저장됨.
2. **스냅샷 생성**  
    초기화 후 메모리와 디스크 상태를 스냅샷으로 캡처함.
3. **스냅샷 재사용**  
    이후 호출 시 스냅샷을 로드하여 초기화 단계를 생략하고 빠르게 실행됨.