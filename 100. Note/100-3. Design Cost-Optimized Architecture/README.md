# Design Cost Optimized Architectures

## EC2

* IT 인프라를 AWS로 이관할 때, License를 유지하며 **비용 효율적으로** 이동할 수 있는 방법.  
    > * [EC2 dedicated hosts](https://aws.amazon.com/ec2/dedicated-hosts/)는 인스턴스가 물리적 서버에 배치되는 방식에 대한 가시성 및 제어 기능을 제공.
    > * 따라서 기존 서버 바인딩 소프트웨어 라이선스를 사용할 수 있음.

* 온디맨드 인스턴스와 스팟 인스턴스를 혼합하여 관리하려 Auto Scaling 그룹을 생성할 때, 인스턴스 프로비저닝 옵션.
    > * [시작 템플릿](https://docs.aws.amazon.com/autoscaling/ec2/userguide/launch-templates.html)을 사용하여 온디맨드 인스턴스와 스팟 인스턴스를 모두 사용하는 등의 프로비저닝을 할 수 있음.

## Amazon DynamoDB

* Amazon DynamoDB에는 사용자 데이터, Amazon S3에는 정적 컨텐츠를 저장하는데 90% 정도의 데이터에 read requests가 발생할 때 Application의 성능을 효율적으로 증가시키는 방법.
    > * Amazon DynamoDB에는 DAX(DynamoDB Accelerator), Amazon S3에는 Amazon CloudFront를 활성화.
    > * DAX: Amazon DynamoDB를 위한 완전 관리형 고가용성 인 메모리 캐시. DynamoDB 읽기를 기본적으로 캐시하는 데 사용.
    > * Amazon CloudFront: 정적 및 동적 웹 컨텐츠, 비디오 스트림 및 API를 전 세계에 안전하고 대규모로 제공하는 CDN 서비스.

## Amazon ECS(Elastic Compute Service)

* Fargate 를 사용하는 ECS, EC2를 사용하는 ECS의 [요금 차이](https://aws.amazon.com/ko/ecs/pricing/) 설명.
    > * EC2 launch type을 사용하는 Amazon ECS는 EC2 인스턴스, EBS Volume에 기반하여 요금이 부과됨.
    > * Fargate launch type을 사용하는 Amazon ECS는 application의 vCPU, memory 사용량에 기반하여 요금이 부과됨.

## Amazon Direct Connect

* AWS Direct Connect를 이용하여 On-premise와 AWS를 연결해 놓은 상태에서 데이터 웨어하우스를 AWS로 이관 했을 때, 데이터 웨어하우스에서 반환된 쿼리(응답 크기 60MB)와 시각화 도구(600KB)를 최소 비용으로 사용하는 방법.
    > * Data warehouse가 있는 동일한 region에 시각화 도구를 배치.
    > * Direct Connect를 이용하여 시각화 도구를 이용.
    > * AWS Direct Connect는 AWS에서 On-premise로의 데이터 전송량에 따라 가격이 매겨짐.
    > * 데이터 전송 크기를 최소한으로 하기 위해 쿼리 결과를 받는 시각화 도구는 데이터 웨어하우스 근처에 두고, 시각화 도구의 결과만 On-premise로 이동.

## Amazon S3

* 네트워크 사용량 중 대부분이 애플리케이션의 정적 콘텐츠 배포로 인한 것임을 알 때, 네트워크 사용량을 개선하고 비용을 절감하기 위한 방법.
    > * Amazon S3를 사용하여 정적 웹 사이트를 호스팅 할 수 있음.
    > * Amazon S3를 통해 정적 콘텐츠를 배포하면 대부분의 네트워크 사용량을 Amazon S3에서 오프로드할 수 있음.

* 새로운 지역에서 Amazon S3 버킷에 대용량 파일을 업로드하는데 지연이 발생할 때, 해결할 수 있는 방법.
    > * [Amazon S3 Transfer Acceleration](https://docs.aws.amazon.com/AmazonS3/latest/userguide/transfer-acceleration.html)(Amazon S3TA)를 사용하여 S3 버킷에 더 빠르게 파일을 업로드 할 수 있음. 이 때, Amazon S3TA는 Amazon CloudFront의 엣지 로케이션을 활용 함.
    > * [Multipart Upload](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html)를 사용하여 Amazon S3 버킷에 더 빠르게 파일을 업로드 할 수 있음. 객체 크기가 100MB 정도가 되면 멀티 파트를 이용하는 것을 고려해야 함.

* Amazon S3에 저장된 자산을 며칠 동안은 많은 수의 사용자가 액세스 하고, 일주일이 지나면 액세스 빈도가 급격하게 떨어짐. 첫 주 이후 자산에 가끔 액세스할 수 있지만, 필요한 경우 계속해서 즉시 액세스할 수 있어야 함. 이 때, 비용을 절감하는 방법.
    > * 30일 후에 Amazon S3 One Zone-IA로 전환하도록 [수명주기 정책](https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-transition-general-considerations.html)을 구성.
    > * Amazon S3 One Zone-IA는 자주 액세스하지 않지만 필요할 때 빠른 액세스가 필요한 데이터를 위한 것.
    > * 단일 가용영역에 데이터를 저장하여 S3 Standard-IA보다 비용이 20% 저렴.
    > * Amazon S3 Standard에서 Amazon S3 One Zone-IA로 객체를 전환하기 전까지 최소 저장 기간은 **30일**.

## [AWS Snowball](https://aws.amazon.com/ko/snowball/)

* 온프레미스 데이터 센터에 있는 약 5페타바이트의 데이터를 내구성 있는 장기 스토리지에 보관하는 가장 비용 효율적인 방법.
    > * 온프레미스 데이터를 여러 개의 AWS Snowball Edge Storage Opimized Device로 전송.
    > * 전송된 데이터를 Amazon S3에 복사 후, life cycle 정책을 수립하여 Amazon S3 Glacier로 이동.
    > * AWS Snowball Edge Storage Optimized는 수십 테라바이트에서 페타바이트 규모의 데이터를 AWS로 안전하고 신속하게 전송.
    > * AWS Snowball Edge Device에서 AWS S3 Glacier로 바로 데이터를 전송할 수 없음.

## AWS Shield

* AWS 계정에서 [AWS Shield](https://aws.amazon.com/ko/shield/faqs/) Advanced를 활성화 했는데, 비용이 매우 높게 나옴. 근본적인 이유.
    > * AWS Shield Advanced에서 통합결제가 활성화되지 않았을 수 있음.
    > * 모든 AWS 계정은 월별 요금이 한 번만 청구되는 단일 통합 결제에 속해야 함.
    > * 그렇지 않은 경우, 모든 AWS 계정에서 사용하는 리소스에 대한 청구가 각각 이루어져 비용이 높게 나올 수 있음.

## AWS ElastiCache

* RDS에 대한 읽기 트래픽이 과도하게 발생하여, 대량의 읽기 트래픽을 처리하고 지연시간을 줄이며 인스턴스 크기를 줄여 비용을 절감하는 방법.
    > * Amazon ElastiCache는 Amazon RDS와 같은 데이터 스토어와 같이 요청률이 매우 높거나 지연시간 요구 사항이 짧은 애플리케이션에 적합함.
    > * 이와 같이 규모와 속토 측면에서 [캐싱](https://aws.amazon.com/ko/caching/database-caching/)은 애플리케이션 성능을 크게 향상 시킴.

## AWS Compute Optimizer

* Amazon EC2 instance, Amazon RDS instance, Amazon S3를 사용하는데 비즈니스 요구 사항에 비해 높은 비용을 지출할 때, 유요한 비용 최적화 솔루션.
    > * AWS Cost Explorer 리소스 최적화를 사용하여 유휴 상태이거나 사용률이 낮은 Amazon EC2 인스턴스에 대한 보고서를 얻음.
    > * 또한, AWS Compute Optimizer를 사용하여 인스턴스 유형 권장 사항을 확인.
    > * **AWS Cost Explorer**: 동일한 인스턴스 패밀리내에서 활용도가 낮은 EC2 인스턴스를 식별.
    > * **[AWS Compute Optimizer](https://aws.amazon.com/ko/compute-optimizer/)**: 기계학습을 사용하여 비용을 절감시키고 성능을 향상시키기 위해 워크로드에 최적의 AWS 컴퓨팅 리소스를 권장.

## AWS CloudWatch

* EC2에 배포한 애플리케이션에서 알 수 없는 버그가 발생해 EC2 인스턴스가 정기적으로 정지됨. 이 사항을 해결하기 전까지, 인스턴스 정지 시 자동으로 인스턴스를 실행시키는 비용 효율적이고, 리소스 효율적인 방법.
    > * 인스턴스 상태를 모니터링 하기 위해 CloudWatch를 설정. 
    > * [CloudWatch에서 EC2 Health Check 실패 시 EC2 재부팅 알람을 사용하여 인스턴스를 재부팅](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/UsingAlarmActions.html).
    > * CloudWatch 경보 작업을 사용하면 EC2 인스턴스를 자동으로 중지, 종료, 재부팅 또는 복구하는 **경보**를 생성할 수 있음.

## AWS DMS(Database Migration Service)

* 온프레미스의 데이터 센터에 라이선스 기반 레거시 데이터베이스 솔루션을 배포했음. 이를 AWS 클라우드로 마이그레이션 하길 원하는데, 비용 효율적이고 오픈 소스인 것으로 마이그레이션 하길 원함. 또한, 보조 인덱스, 외래 키, 저장 프로시저와 같은 구성도 처리를 원함. 이 때 해결 방안.
    > * [AWS DMS](https://aws.amazon.com/ko/dms/)는 데이터베이스를 AWS로 빠르고 안전하게 마이그레이션하는 데 도움을 줌.
    > * 기존 온프레미스에 있는 데이터베이스는 마이그레이션 중에도 완벽하게 작동하여 애플리케이션의 가동 중지 시간이 최소화 됨.
    > * AWS DMS는 동종 마이그레이션 뿐만 아니라, 이기종 마이그레이션도 지원.
    > * 이기종 마이그레이션의 경우, [AWS Schema Conversion Tool](https://aws.amazon.com/ko/dms/schema-conversion-tool/)을 사용하여 소스 스키마와 코드를 대상 데이터베이스와 일치하도록 변환해야 함.
    > * 그 후, AWS DMS를 사용하여 데이터를 마이그레이션.