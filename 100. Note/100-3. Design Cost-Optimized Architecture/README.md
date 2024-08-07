# Design Cost Optimized Architectures

## EC2

* IT 인프라를 AWS로 이관할 때, License를 유지하며 **비용 효율적으로** 이동할 수 있는 방법.  
    > * [EC2 dedicated hosts](https://aws.amazon.com/ec2/dedicated-hosts/)는 인스턴스가 물리적 서버에 배치되는 방식에 대한 가시성 및 제어 기능을 제공.
    > * 따라서 기존 서버 바인딩 소프트웨어 라이선스를 사용할 수 있음.

* 온디맨드 인스턴스와 스팟 인스턴스를 혼합하여 관리하려 Auto Scaling 그룹을 생성할 때, 인스턴스 프로비저닝 옵션.
    > * [시작 템플릿](https://docs.aws.amazon.com/autoscaling/ec2/userguide/launch-templates.html)을 사용하여 온디맨드 인스턴스와 스팟 인스턴스를 모두 사용하는 등의 프로비저닝을 할 수 있음.

* 프로덕션 EC2 인스턴스는 하루 24시간 실행되고, 개발 및 테스트 EC2 인스턴스는 매일 최소 8시간 동안 실행되며, 개발을 중지하고 사용하지 않을 때 EC2 인스턴스를 테스트하는 자동화를 구현하려 할 때, 비용 효율적인 방법.
    > * 프로덕션 EC2 인스턴스: **예약 인스턴스 사용**. 예약 인스턴스는 1년 또는 3년 기간으로 예약할 수 있으며, 장기적으로 사용하기 때문에 큰 비용 절감 효과가 있음.
    > * 개발 및 테스트 EC2 인스턴스: **온디맨드 인스턴스 사용**.
    > * 온디맨드 인스턴스를 사용할 경우, 필요할 때만 인스턴스를 실행하고 사용한 만큼만 비용을 지불. 자동화를 통해 인스턴스를 필요할 때만 실행하도록 설정할 수 있음.
    > * CF. **Spot Block**
    > * 스팟 블락은 AWS에서 제공하는 스팟 인스턴스의 한 종류로, 특정 기간 동안 EC2 인스턴스를 예약하고 실행할 수 있는 기능.
    > * 스팟 블락은 1시간에서 최대 6시간 동안 인스턴스의 실행을 보장. 이 시간동안 인스턴스는 중지되지 않음.
    > * 스팟 블락은 특정 시간 동안의 실행을 예약하므로, 비용 예측이 가능하고 예산 관리가 용이함.

* 애플리케이션 프런트 엔드는 **Fargate**에서 실행되고 **Lambda**는 API 계층을 제공함. 프론트엔드 활용도와 API 계층 활용도는 내년에 예측할 수 있음. EC2 인스턴스는 애플리케이션의 데이터 수집 계층을 실행함. EC2 사용은 산발적이고 예측할 수 없으며, EC2 인스턴스에서 실행되는 워크로드는 언제든지 중단될 수 있음. 이 때, 이 애플리케이션을 호스팅하는 데 가장 비용 효율적인 솔루션을 제공하는 방법.
    > * 데이터 수집 계층에 **스팟 인스턴스** 사용.
    > * 프론트 엔드 및 API 계층에 대한 1년 **Compute Savings Plan** 구매.
    > * **Spot Instance**: 동일한 EC2 인스턴스 유형에 비해 최대 90%까지 비용을 줄일 수 있음. 데이터 수집 계층은 불규칙하고 예측할 수 없는 사용 패턴을 가지고 있기 때문에, Spot Instance를 사용하여 비용을 최적화 할 수 있음.
    > * 또한, 작업이 언제든지 중단될 수 있음을 허용하는 워크로드에 이상적임. 
    > * **Compute Savings Plan**: 애플리케이션 프론트 엔드와 API 계층의 사용량이 예측 가능하기 떄문에, Compute Savings Plan을 사용하여 비용을 줄일 수 있음.
    > * Savings Plan은 EC2, Fargate, Lambda와 같은 다양한 AWS 컴퓨팅 서비스에 적용되므로, 장기적인 사용량을 예측하여 할인된 요금으로 이용할 수 있음.

## Amazon DynamoDB

* Amazon DynamoDB에는 사용자 데이터, Amazon S3에는 정적 컨텐츠를 저장하는데 90% 정도의 데이터에 read requests가 발생할 때 Application의 성능을 효율적으로 증가시키는 방법.
    > * [Amazon DynamoDB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-4.%20Amazon%20DynamoDB)에는 [DAX](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-4.%20Amazon%20DynamoDB/7-4-2.%20DynamoDB%20Accelerator)(DynamoDB Accelerator), Amazon S3에는 Amazon CloudFront를 활성화.
    > * DAX: Amazon DynamoDB를 위한 완전 관리형 고가용성 인 메모리 캐시. DynamoDB 읽기를 기본적으로 캐시하는 데 사용.
    > * Amazon CloudFront: 정적 및 동적 웹 컨텐츠, 비디오 스트림 및 API를 전 세계에 안전하고 대규모로 제공하는 CDN 서비스.

## Amazon ECS(Elastic Container Service)

* Fargate 를 사용하는 ECS, EC2를 사용하는 ECS의 [요금 차이](https://aws.amazon.com/ko/ecs/pricing/) 설명.
    > * EC2 launch type을 사용하는 Amazon ECS는 EC2 인스턴스, EBS Volume에 기반하여 요금이 부과됨.
    > * Fargate launch type을 사용하는 Amazon ECS는 application의 vCPU, memory 사용량에 기반하여 요금이 부과됨.
    > * [ECS launch type 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/9.%20Container/9-1.%20Amazon%20ECS/9-1-1.%20Launch%20Type)

## Amazon Direct Connect

* AWS Direct Connect를 이용하여 On-premise와 AWS를 연결해 놓은 상태에서 데이터 웨어하우스를 AWS로 이관 했을 때, 데이터 웨어하우스에서 반환된 쿼리(응답 크기 60MB)와 시각화 도구(600KB)를 최소 비용으로 사용하는 방법.
    > * Data warehouse가 있는 동일한 region에 시각화 도구를 배치.
    > * Direct Connect를 이용하여 시각화 도구를 이용.
    > * [AWS Direct Connect](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/15.%20VPC/15-13.%20Direct%20Connect(DX))는 AWS에서 On-premise로의 데이터 전송량에 따라 가격이 매겨짐.
    > * 데이터 전송 크기를 최소한으로 하기 위해 쿼리 결과를 받는 시각화 도구는 데이터 웨어하우스 근처에 두고, 시각화 도구의 결과만 On-premise로 이동.
    > * [AWS [ DataWarehouse Region / 시각화도구 (쿼리결과)--]--]----> [ On-Premise ]

## Amazon S3

* 네트워크 사용량 중 대부분이 애플리케이션의 정적 콘텐츠 배포로 인한 것임을 알 때, 네트워크 사용량을 개선하고 비용을 절감하기 위한 방법.
    > * [Amazon S3](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3)를 사용하여 정적 웹 사이트를 호스팅 할 수 있음.
    > * Amazon S3를 통해 정적 콘텐츠를 배포하면 대부분의 네트워크 사용량을 Amazon S3에서 오프로드할 수 있음.

* 새로운 지역에서 Amazon S3 버킷에 대용량 파일을 업로드하는데 지연이 발생할 때, 해결할 수 있는 방법.
    > * [Amazon S3 Transfer Acceleration](https://docs.aws.amazon.com/AmazonS3/latest/userguide/transfer-acceleration.html)(Amazon S3TA)를 사용하여 S3 버킷에 더 빠르게 파일을 업로드 할 수 있음. 이 때, Amazon S3TA는 Amazon CloudFront의 엣지 로케이션을 활용 함.
    > * [Multipart Upload](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html)를 사용하여 Amazon S3 버킷에 더 빠르게 파일을 업로드 할 수 있음. 객체 크기가 100MB 정도가 되면 멀티 파트를 이용하는 것을 고려해야 함.
    > * [S3 Performance 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3/6-3-6.%20Performance)

* Amazon S3에 저장된 자산을 며칠 동안은 많은 수의 사용자가 액세스 하고, 일주일이 지나면 액세스 빈도가 급격하게 떨어짐. 첫 주 이후 자산에 가끔 액세스할 수 있지만, 필요한 경우 계속해서 즉시 액세스할 수 있어야 함. 이 때, 비용을 절감하는 방법.
    > * 30일 후에 Amazon S3 One Zone-IA로 전환하도록 [수명주기 정책](https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-transition-general-considerations.html)을 구성.
    > * Amazon S3 One Zone-IA는 자주 액세스하지 않지만 필요할 때 빠른 액세스가 필요한 데이터를 위한 것.
    > * 단일 가용영역에 데이터를 저장하여 S3 Standard-IA보다 비용이 20% 저렴.
    > * Amazon S3 Standard에서 Amazon S3 One Zone-IA로 객체를 전환하기 전까지 최소 저장 기간은 **30일**.
    > * [S3 Storage class 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3/6-3-4.%20Storage%20Class)

* 1년 이내에 파일에 무작위로 액세스 하지만, 1년 이후에는 파일에 자주 액세스하지 않을 때 1년 미만의 파일을 가능한 빨리 쿼리하고 검색할 수 있는 기능을 제공하고, 오래된 파일은 검색하는데 지연이 허용되는 비용 효율적인 방법.
    > * [Amazon S3 Intelligent-Tiering](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-3.%20S3/6-3-4.%20Storage%20Class#s3-intelligent-tiering)에 개별 파일을 저장. S3 수명 주기 정책을 사용하여 1년 후 파일을 **S3 Glacier Flexible Retrieval**로 이동.
    > * Amazon Athena를 사용하여 Amazon S3에 있는 파일을 쿼리하고 검색.
    > * S3 Glacier Select를 사용하여 S3 Glacier에 있는 파일을 쿼리하고 검색.
    > * **Amazon S3 Intelligent-Tiering**
    > * 개체 크기나 보존 기간에 관계없이 알 수 없거나 변경되거나 예측할 수 없는 액세스 패턴이 있는 데이터에 이상적인 스토리지 클래스.
    > * 데이터의 액세스 패턴을 분석하여 자동으로 데이터를 스토리지 클래스(티어) 중 하나로 이동시키는 서비스.
    > * 데이터 레이크, 데이터 분석, 새로운 애플리케이션 및 사용자 생성 콘텐츠에 대한 기본 스토리지 클래스로 사용할 수 있음.
    > * 1년 이내에 액세스 되는 파일은 높은 우선순위 티어에 유지되어 빠르게 쿼리하고 검색할 수 있음.
    > * [Amazon Athena](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-10.%20Amazon%20Athena)
    > * Amazon S3에 저장된 데이터를 직접 쿼리할 수 있는 서비스로, 비정형 데이터나 대규모 데이터를 효율적으로 분석하는 데 특화됨.
    > * 쿼리할 때만 비용이 청구되어, 계속 운영되는 인프라를 두지 않아도 됨.
    > * **Amazon S3 Glacier Flexible Retrieval**
    > * 비동기로 검색되는 아카이브 데이터에 대한 저렴한 비용의 스토리지.
    > * 몇 분에서 몇 시간까지 다양한 액세스 시간에서 비용의 균형을 조정하는 대부분의 검색 속도 옵션과 무료 대량 검색 기능을 제공.

* 동일 AWS 리전에 있는 Amazon S3 버킷에서 업로드 및 다운로드가 빈번하여 데이터 전송 비용이 증가하는데, 이와 같은 비용을 줄이기 위한 방법.
    > * [S3 VPC gateway endpoint](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/15.%20VPC/15-8.%20VPC%20Endpoints#%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4-%EC%97%94%EB%93%9C%ED%8F%AC%EC%9D%B8%ED%8A%B8-gateway-endpoint)를 VPC에 배포하고, S3 버킷에 대한 액세스를 허용하는 엔드포인트 정책을 연결.
    > * S3에 직접 업로드 및 다운로드를 하면, **인터넷을 통해 전송**됨. 이 경우, 데이터 전송 비용 발생.
    > * **VPC Gateway Endpoint**를 사용하면, 데이터가 AWS 네트워크 내에서 전송되어 인터넷을 거치지 않아 비용이 발생되지 않음.

* Amazon S3에 크기가 3TB이고 증가하고 있는 데이터를 호스팅 중일 때, S3 버킷이 있는 다른 지역의 회사와 데이터를 공유하려 함. 데이터 전송 비용이 가능한 한 낮게 유지되도록 하는 방법.
    > * S3 버킷에서 **요청자 지불 기능**을 구성.
    > * 요청자 지불 기능(Requester Pays)는 데이터를 요청하는 사용자가 데이터 전송 비용을 부담하도록 하는 S3의 기능.
    > * 회사가 데이터 전송 비용을 부담하지 않기 때문에 데이터 전송 비용을 최소화할 수 있음. 이는 데이터 전송 비용을 데이터 요청자에게 전가하여 비용을 절감하는 방법.

## [AWS Snowball](https://aws.amazon.com/ko/snowball/)

* 온프레미스 데이터 센터에 있는 약 5페타바이트의 데이터를 내구성 있는 장기 스토리지에 보관하는 가장 비용 효율적인 방법.
    > * 온프레미스 데이터를 여러 개의 AWS Snowball Edge Storage Opimized Device로 전송.
    > * 전송된 데이터를 **Amazon S3에 복사 후, life cycle 정책을 수립하여 Amazon S3 Glacier로 이동**.
    > * AWS Snowball Edge Storage Optimized는 수십 테라바이트에서 페타바이트 규모의 데이터를 AWS로 안전하고 신속하게 전송.
    > * AWS Snowball Edge Device에서 AWS S3 Glacier로 바로 데이터를 전송할 수 없음.
    > * [AWS Snowball Family](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-4.%20Snow%20Family)

## AWS Shield

* AWS 계정에서 [AWS Shield](https://aws.amazon.com/ko/shield/faqs/) Advanced를 활성화 했는데, 비용이 매우 높게 나옴. 근본적인 이유.
    > * [AWS Shield Advanced](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/14.%20AWS%20Security%20%26%20Encryption/14-6.%20AWS%20Shield#aws-shield-advanced)에서 **통합결제**가 활성화되지 않았을 수 있음.
    > * 모든 AWS 계정은 월별 요금이 한 번만 청구되는 단일 통합 결제에 속해야 함.
    > * 그렇지 않은 경우, 모든 AWS 계정에서 사용하는 리소스에 대한 청구가 각각 이루어져 비용이 높게 나올 수 있음.

## AWS ElastiCache

* RDS에 대한 읽기 트래픽이 과도하게 발생하여, 대량의 읽기 트래픽을 처리하고 지연시간을 줄이며 인스턴스 크기를 줄여 비용을 절감하는 방법.
    > * [Amazon ElastiCache](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-3.%20Amazon%20ElastiCache/7-3-1.%20ElastiCache%20Architecture)는 Amazon RDS와 같은 데이터 스토어와 같이 요청률이 매우 높거나 지연시간 요구 사항이 짧은 애플리케이션에 적합함.
    > * 이와 같이 규모와 속토 측면에서 [캐싱](https://aws.amazon.com/ko/caching/database-caching/)은 애플리케이션 성능을 크게 향상 시킴.

## AWS Compute Optimizer

* Amazon EC2 instance, Amazon RDS instance, Amazon S3를 사용하는데 비즈니스 요구 사항에 비해 높은 비용을 지출할 때, 유요한 비용 최적화 솔루션.
    > * [AWS Cost Explorer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/17.%20Other%20Services/17-5.%20Cost%20Explorer) 리소스 최적화를 사용하여 유휴 상태이거나 사용률이 낮은 Amazon EC2 인스턴스에 대한 보고서를 얻음.
    > * 또한, AWS Compute Optimizer를 사용하여 인스턴스 유형 권장 사항을 확인.
    > * **AWS Cost Explorer**: 동일한 인스턴스 패밀리내에서 활용도가 낮은 EC2 인스턴스를 식별.
    > * **[AWS Compute Optimizer](https://aws.amazon.com/ko/compute-optimizer/)**: 기계학습을 사용하여 비용을 절감시키고 성능을 향상시키기 위해 워크로드에 최적의 AWS 컴퓨팅 리소스를 권장.

## AWS CloudWatch

* EC2에 배포한 애플리케이션에서 알 수 없는 버그가 발생해 EC2 인스턴스가 정기적으로 정지됨. 이 사항을 해결하기 전까지, 인스턴스 정지 시 자동으로 인스턴스를 실행시키는 비용 효율적이고, 리소스 효율적인 방법.
    > * 인스턴스 상태를 모니터링 하기 위해 CloudWatch를 설정. 
    > * [CloudWatch에서 EC2 Health Check 실패 시 EC2 재부팅 알람을 사용하여 인스턴스를 재부팅](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/UsingAlarmActions.html).
    > * CloudWatch 경보 작업을 사용하면 EC2 인스턴스를 자동으로 중지, 종료, 재부팅 또는 복구하는 **경보**를 생성할 수 있음.
    > * [CloudWatch Alarms 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/13.%20Monitoring%2C%20Audit%20%26%20Performance/13-1.%20Amazon%20CloudWatch/13-1-5.%20CloudWatch%20Alarms)

* Amazon CloudWatch Logs 로그 그룹에 애플리케이션 로그를 저장 중임. 모든 애플리케이션 로그를 Amazon OpenSearch Service(Amazon Elasticsearch Service)에 거의 실시간으로 저장하고자 할 때, **최소한의 운영 오버헤드**로 해결하는 방법.
    > * **Amazon OpenSearch Service**로 로그를 스트리밍하도록 [CloudWatch Logs 구독](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/13.%20Monitoring%2C%20Audit%20%26%20Performance/13-1.%20Amazon%20CloudWatch/13-1-2.%20CloudWatch%20Logs%20Subscriptions)을 구성. [링크](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_OpenSearch_Stream.html)
    > * [CloudWatch Logs](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/13.%20Monitoring%2C%20Audit%20%26%20Performance/13-1.%20Amazon%20CloudWatch/13-1-1.%20CloudWatch%20Logs)와 OpenSearch Service 간의 스트리밍 설정은 단순하며, 실시간으로 스트리밍할 수 있음. 따라서 운영 오버헤드가 적음.
    > * [Amazon OpenSearch Service](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-12.%20Amazon%20OpenSearch)
    > * AWS 클라우드에서 OpenSearch 클러스터를 손쉽게 배포, 운영 및 확장할 수 있도록 해주는 관리형 서비스.
    > * OpenSearch는 로그 분석, 실시간 애플리케이션 모니터링, 클릭 스트림 분석 같은 사용 사례를 위한 완전한 오픈 소스 검색 및 분석 엔진임.
    > * **Kinesis Data Firehose**를 사용하려면 Kinesis 스트림, Firehose 설정, Lambda 함수 등을 관리해야하여 운영 오버헤드가 높음.

## AWS DMS(Database Migration Service)

* 온프레미스의 데이터 센터에 라이선스 기반 레거시 데이터베이스 솔루션을 배포했음. 이를 AWS 클라우드로 마이그레이션 하길 원하는데, 비용 효율적이고 오픈 소스인 것으로 마이그레이션 하길 원함. 또한, 보조 인덱스, 외래 키, 저장 프로시저와 같은 구성도 처리를 원함. 이 때 해결 방안.
    > * [AWS DMS](https://aws.amazon.com/ko/dms/)는 데이터베이스를 AWS로 빠르고 안전하게 마이그레이션하는 데 도움을 줌.
    > * 기존 온프레미스에 있는 데이터베이스는 마이그레이션 중에도 완벽하게 작동하여 애플리케이션의 가동 중지 시간이 최소화 됨.
    > * AWS DMS는 동종 마이그레이션 뿐만 아니라, 이기종 마이그레이션도 지원.
    > * 이기종 마이그레이션의 경우, [AWS Schema Conversion Tool](https://aws.amazon.com/ko/dms/schema-conversion-tool/)을 사용하여 소스 스키마와 코드를 대상 데이터베이스와 일치하도록 변환해야 함.
    > * 그 후, AWS DMS를 사용하여 데이터를 마이그레이션.
    > * [AWS DMS 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/16.%20Disaster%20Recovery%20%26%20Migrations/16-1.%20Database%20Migration%20Service)

## Amazon Athena

* 애플리케이션의 로그가 Amazon S3 버킷에 JSON 형식으로 저장되고, 이를 분석하기 위한 쿼리는 주문형으로 실행될 때 최소한의 운영 오버헤드와 아키텍처의 최소 변경을 이룰 수 있는 방법.
    > * [Amazon Athena](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-10.%20Amazon%20Athena)를 사용하여 Amazon S3에 연결하여 쿼리 실행.  
    > * Amazon Athena는 서버리스 서비스로, 별도의 인프라를 관리할 필요 없이 S3에 저장된 데이터를 직접 쿼리 가능.
    > * Athena는 사용한 만큼 비용을 지불하는 모델로, 쿼리 실행 시간에 따라서 비용이 발생하므로 비용 절감 가능.

## Cost Explorer

* EC2 인스턴스에 대한 인스턴스 유형의 원치 않는 수직적 확장이 발생함. 지난 2개월간의 EC2 비용을 비교하는 그래프를 생성하고, 심층 분석을 통해 원인을 식별하기를 원함. 이 때, 운영 오버헤드가 가장 적은 정보를 생성하는 방법.
    > * [Cost Explorer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/17.%20Other%20Services/17-5.%20Cost%20Explorer)
    > * AWS 제공하는 관리형 서비스로, 추가적인 인프라 설정이나 관리가 필요 없어서 운영 오버헤드를 최소화 함.
    > * 필터링 기능을 사용하여 인스턴스 유형별로 비용을 상세하게 분석 가능.
    > * 자동으로 비용 데이터를 수집하고 시각화하여 손쉽게 그래프와 보고서를 생성 가능.

## Amazon Kinesis

* 경고를 생성하는 장치가 있는데, 해당 경고를 수집하고 저장하는 솔루션 구축을 원함. 비용을 최소화하면서 추가적인 인프라 구성 없이 대량의 경고를 수집하고 즉각적인 분석을 위해 14일 동안의 데이터를 유지하고 14일이 지난 데이터는 보관하기 위한 운영 효율적인 방법.
    > * [Amazon Kinesis Data Firehose](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-4.%20AWS%20Kinesis/8-4-2.%20Kinesis%20Data%20Firehose) 전송 스트림을 생성하여 경고를 수집 및 분석하고, 14일 후에 데이터를 Amazon S3 Glacier로 전환하도록 수명 주기 구성을 설정.
    > * Amazon Kinesis Data Firehose는 내결함성을 갖춘 서비스로, 데이터를 안정적으로 수집하고 전달할 수 있음.
    > * 사용한 만큼만 비용이 청구되며, 추가적인 인프라 관리나 서버 배포가 필요하지 않음. 따라서 추가적으로 인프라를 관리하지 않고도 비용 효율적으로 관리할 수 있음.
    > * [AWS Kinesis Firehose 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-4.%20AWS%20Kinesis/8-4-2.%20Kinesis%20Data%20Firehose)

## AWS Lambda

* REST API를 사용해 주문 배송 통계를 제공하는 애플리케이션을 개발중인데, 배송 통계를 추출하고 데이터를 읽기 쉬운 HTML 형식으로 구성하고 매일 아침 여러 이메일 주소로 보고서를 보내려할 때, 사용할 수 있는 방법.
    > * [AWS Lambda](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-4.%20Serverless/3-4-1.%20AWS%20Lambda)함수를 호출하여 데이터에 대한 애플리케이션의 API를 쿼리하는 Amazon Event Bridge 예약 이벤트를 생성.
    > * [Amazon SES](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/17.%20Other%20Services/17-2.%20Amazon%20SES)를 사용하여 데이터 형식을 지정하고 보고서를 이메일을 보내도록 설정.
    > * 정기적으로 주문 배송 통계를 검색하기 위해 AWS Lambda 함수를 실행하는 스케쥴된 이벤트를 설정해야함.
    > * **Amazon EventBridge**: 자체 애플리케이션, SaaS 애플리케이션, AWS 서비스의 데이터를 사용하여 애플리케이션을 쉽게 연결할 수 있게 지원하는 서버리스 이벤트 버스.

## AWS Backup

* 데이터를 Amazon DynamoDB 테이블에 보관하는데, 7년간 보관해야 할 때 운영 효율성이 높은 방법.
    > * [AWS Backup](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/16.%20Disaster%20Recovery%20%26%20Migrations/16-2.%20AWS%20Backup)을 사용하여 테이블에 대한 백업 일정 및 보존 정책을 생성.
    > * **AWS Backup**
    > * 데이터 백업, 복원, 보존을 자동화할 수 있는 서비스.
    > * 백업은 주기적으로 생성되며, 설정된 보존 기간 동안 유지됨.
    > * AWS의 여러 서비스(DynamoDB, RDS, EFS 등)에 대해 중앙에서 백업을 관리할 수 있는 기능을 제공.
    > * cf. [Amazon DynamoDB Backups](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-4.%20Amazon%20DynamoDB/7-4-6.%20Backups)

## Amazon Glue

* 매일 같은 시간에 실행되는 AWS Glue의 ETL 작업이 있고, Amazon S3 버킷에 있는 데이터를 처리함. 매일 S3 버킷에 데이터가 추가되는데, AWS Glue가 실행 중에 모든 데이터를 처리하고 있음을 알았음. AWS Glue가 오래된 데이터를 재처리하지 못하도록 하는 방법.
    > * **작업 북마크**(job bookmarks)를 사용하도록 작업을 편집함.
    > * **AWS Glue의 작업 북마크**
    > * 데이터 처리 작업의 상태를 추적하고, 이전에 처리된 데이터를 기록하여, 이후 작업에서 중복 처리를 방지하는 기능.
    > * 북마크는 자동으로 관리되며, 필요 시 수동으로 초기화하거나 수정할 수 있음.
    > * [Amazon Glue 기능 설명](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/8.%20Integration%20%26%20Messaging/8-9.%20Amazon%20Glue/8-9-1.%20things%20to%20know)