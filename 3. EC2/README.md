# [EC2](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/concepts.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/5bae276b-8ec8-4c28-af9f-e2f88c717580" width = "20" height = "20"> EC2

* **EC2**: Amazon EC2(Elastic Compute Cloud)는 AWS(Amazon Web Services)에서 제공하는 클라우드 기반의 가상 컴퓨팅 서비스.  
사용자는 EC2를 통해 가상 서버 인스턴스를 생성하고, 필요에 따라 컴퓨팅 파워를 조정할 수 있음.  
EC2는 다양한 컴퓨팅 요구사항에 맞춰 유연하게 확장하거나 축소할 수 있는 서비스로, 웹 애플리케이션 호스팅, 데이터 처리, 백엔드 서버 등 다양한 용도로 사용됨.

## EC2 Configuration

* **[AMI](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/AMIs.html)(Amazon Machine Image)**: 운영 체제, 애플리케이션 서버 및 애플리케이션과 같은 소프트웨어 구성을 포함하는 템플릿으로 사용자는 AMI를 선택하여 인스턴스를 시작할 수 있음.
* **[Instance type](https://aws.amazon.com/ko/ec2/instance-types/)**: 다양한 CPU, 메모리, 스토리지 및 네트워킹 용량을 제공하는 인스턴스 유형을 선택할 수 있음.  
각 인스턴스 유형은 특정 워크로드에 최적화되어 있음.
* **[Security Group](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-security-groups.html)**: 인스턴스로의 트래픽을 제어하는 가상 방화벽.  
사용자는 특정 포트와 프로토콜에 대한 액세스를 허용하거나 거부할 수 있음.
* **[Key Pairs](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/ec2-key-pairs.html)**: SSH를 통한 안전한 인스턴스 로그인을 위한 공개 키 암호화를 사용함.  
사용자는 키 쌍을 생성하고, 인스턴스에 할당하여 보안을 유지할 수 있음.

## Instacne Type

* **범용(General Purpose)**: 균형 잡힌 CPU와 메모리를 제공. 웹 서버 및 코드 저장소와 같은 애플리케이션에 적합.
* **컴퓨팅 최적화(Compute Optimized)**: 고성능 컴퓨팅 작업에 적합.
* **메모리 최적화(Memory Optimized)**: 메모리 집약적인 애플리케이션에 적합.
* **스토리지 최적화(Storage Optimized)**: I/O 집약적인 작업에 적합.
* **가속화된 컴퓨팅(Accelerated Computing)**: GPU를 사용하는 애플리케이션에 적합.
-------------------------
* 유형 구분:  
{인스턴스패밀리}{인스턴스 세대}**.**{인스턴스 크기}
    * 예시:  
    t2.micro: {t}{2}.{micro}  
    t2.xlarge: {t}{2}.{xlarge}  
    r5.16xlarge : {r}{5}.{16xlarge}

## EC2 Cost Optimization

* **온디맨드 인스턴스(On-Demand Instance)**: 장기 약정 없이 초 단위로 컴퓨팅 용량에 대해 비용을 지불.  
인스턴스의 수명 주기를 완전하게 제어할 수 있으며, 중단할 수 없는 불규칙한 단기 워크로드가 있는 애플리케이션의 경우에 적합.
* **예약 인스턴스(Reserved Instance)**: 1년 또는 3년과 같은 장기 약정을 통해 상당한 할인 혜택을 받을 수 있음.  
특정 가용 영역에서 사용하는 경우에는 용량 예약을 제공함.
* **스팟 인스턴스(Spot Instance)**: 사전 약정 없이 On-demand 요금보다 70~90% 절감된 비용으로 사용할 수 있으며, 사용자 제시 가격(입찰가격)을 정해놓고 저렴할 때 이용가능.  
시장 가격이 사용자의 제시 가격보다 높아지면 인스턴스가 종료됨.
