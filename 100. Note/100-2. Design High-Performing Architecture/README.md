# Design High-Performing Architectures

## Lambda

* 서버리스 아키텍처로 마이그레이션 하는데  AWS Lambda를 아키텍처의 백본으로 사용 할 때 고려해야할 사항.  
    > * AWS Lambda는 기본적으로 AWS-owned VPC에서 작동. 따라서 public internet이나 public AWS API에 접근 가능.  
    > * Lambda가 VPC-enabled가 되면 NAT Gateway를 통해 public subnet으로 route 되어야 함.
    > * 여러 Lambda function에서 code를 재사용하기 위해서는 AWS Lambda Layer를 고려할 필요가 있음.

## AWS Global Accelerator

* UDP 프로토콜을 사용하여 지연시간이 짧은 라이브 스포츠 결과를 배포하기 위한 방법.
    > * 전 세계 사용자에게 high-performance, availability를 유지하는 애플리케이션을 배포할 수 있는 방법으로 [AWS Global Accelerator](https://aws.amazon.com/ko/global-accelerator/)가 있음.
    
## Amazon RedShift

* Amazon Redshift를 사용하여 데이터 웨어하우징 솔루션을 구축하고, 1년 이후의 데이터를 Amazon S3로 옮기더라도 해당 데이터와 일일 데이터를 비교할 수 있는 기능을 유지하는 방법.
    > * [Amazon Redshift](https://aws.amazon.com/ko/blogs/big-data/amazon-redshift-spectrum-extends-data-warehousing-out-to-exabytes-no-loading-required/)는 대규모 데이터 세트 저장 및 분석을 위해 설계된 완전 관리형 페타바이트 규모의 클라우드 기반 데이터 웨어하우스 제품.
    > * Amazon Redshift Spectrum에서 Amazon Redshift Cluster 테이블을 이용하여 S3의 historical data를 pointing하여 query를 쉽게 할 수 있음.

## Network Load Balancer

* 퍼블릭 서브넷에 여러 인스턴스를 프로비저닝하고 이러한 인스턴스 ID를 [NLB](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html) 대상으로 지정하여 올바르게 라우팅하는 방법.
    > * 인스턴스 ID를 사용하여 대상을 지정하는 경우 트래픽은 인스턴스의 기본 네트워크 인터페이스에 지정된 Primary Private IP 주소를 사용하여 인스턴스로 라우팅 됨.

## EC2

* EC2 User Data의 특징.
    * > User data는 EC2 인스턴스를 처음 실행했을 때만 실행 됨.
    * > User data는 root user 권한으로만 실행됨.