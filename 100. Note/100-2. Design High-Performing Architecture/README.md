# Design High-Performing Architectures

## Lambda

* 서버리스 아키텍처로 마이그레이션 하는데  AWS Lambda를 아키텍처의 백본으로 사용 할 때 고려해야할 사항.  
    > * AWS Lambda는 기본적으로 AWS-owned VPC에서 작동. 따라서 public internet이나 public AWS API에 접근 가능.  
    > * Lambda가 VPC-enabled가 되면 NAT Gateway를 통해 public subnet으로 route 되어야 함.
    > * 여러 Lambda function에서 code를 재사용하기 위해서는 AWS Lambda Layer를 고려할 필요가 있음.

## AWS Global Accelerator

* UDP 프로토콜을 사용하여 지연시간이 짧은 라이브 스포츠 결과를 배포하기 위한 방법.
    > * 전 세계 사용자에게 high-performance, availability를 유지하는 애플리케이션을 배포할 수 있는 방법으로 [AWS Global Accelerator](https://aws.amazon.com/ko/global-accelerator/)가 있음.