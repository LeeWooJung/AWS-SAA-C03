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