# [EFS](https://docs.aws.amazon.com/ko_kr/efs/latest/ug/whatisefs.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/f8e192fb-d31d-45de-913d-2d8f82c83d16" width = "20" height = "20"> EFS

### 설명    

**AWS EFS**(Elastic File System)는 AWS에서 제공하는 클라우드 기반 파일 스토리지 서비스임.  
이 서비스는 확장성이 높고, 공유성이 높은 **파일 스토리지**를 제공하며, EC2 Linux 인스턴스에 마운트된 **Network File System** (NFS)을 통해 VPC에서 필요한 파일에 접근하거나 AWS Direct Connect로 연결된 온프레미스 서버의 파일에 접근할 수 있음.

### 장점

1. EFS는 사용이 간편하며, 파일 시스템을 쉽고 빠르게 생성 및 구성할 수 있는 간단한 인터페이스를 제공하며, 애플리케이션에서는 필요할 때 필요한 만큼 스토리지를 확보할 수 있음.  
또한 리전별 서비스인 EFS는 여러 가용 영역에 걸쳐 데이터를 중복으로 저장하여 **높은 가용성과 내구성**을 제공하도록 설계되어 있음.

2. EFS는 다수의 인스턴스에서 파일에 접근 할 수 있는 **전송 지연 문제가 적으며 안전하며 내구성이 높은 네트워크 파일 스토리지 서비스**라고 할 수 있음. 이런 특징들로 인해 EFS는 웹 서비스 환경, 콘텐츠 관리 시스템, 홈 디렉터리, 일반 파일 서비스와 같이 지연 시간에 민감한 애플리케이션에 적합함.

### 단점

EFS는 리눅스용 파일 서비스로, 따라서 **윈도우는 지원되지 않으며**, 아마존 리눅스 AMI에 최적화 되어 있음.  
우분투 역시 연결이 가능하지만 설정이 약간 복잡하다는 흠이 있음.

## EFS with Security Group

**AWS EFS**(Elastic File System)는 AWS에서 제공하는 확장 가능한 파일 스토리지 서비스임.  
이 서비스는 EC2 인스턴스와 같은 AWS 리소스에서 사용할 수 있으며, 이러한 리소스들은 [**AWS Security Group**](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/4.%20Security%20Group)과 연결되어 있음.

**AWS Security Group**은 가상 프라이빗 클라우드(**VPC**) 내에서 동작하는 가상 방화벽으로, 인스턴스에 대한 **인바운드** 및 **아웃바운드** 트래픽을 제어함. Security Group은 인스턴스의 **ENI**(Elastic Network Interface)에 적용되며, 인스턴스에 대한 특정 유형의 트래픽을 허용하거나 거부할 수 있음.

* **EFS와 Security Group의 연결**  
EFS와 Security Group을 연결하면, **EFS 파일 시스템에 대한 접근을 보안 그룹의 규칙에 따라 제어**할 수 있음.  
예를 들어, 특정 Security Group의 인스턴스만 EFS에 접근하도록 설정할 수 있음.  
이렇게 하면 EFS 파일 시스템에 대한 접근을 보다 세밀하게 제어하고, 필요한 경우 보안을 강화할 수 있음.

## EFS with EC2 Instance
EFS 파일 시스템을 생성하고 인스턴스에 탑재할 때, **Amazon EFS Quick Create** 기능을 사용하여 인스턴스를 시작할 때 EFS 파일 시스템을 생성하고 인스턴스에 탑재할 수 있음.  
이 과정에서 필요한 **보안 그룹이 자동으로 생성**되어 파일 시스템의 인스턴스 및 탑재 대상에 연결됨.

이렇게 AWS EFS와 AWS Security Group을 연결하여 사용하면, 클라우드 환경에서의 파일 스토리지 관리를 보다 안전하고 효율적으로 수행할 수 있음.

## EFS Use Case

**AWS EFS**(Elastic File System)는 다양한 사용 사례에 적합한 확장 가능한 파일 스토리지 서비스임.

1. **DevOps 간소화**  
EFS는 안전하고 체계적인 방식으로 코드 및 기타 파일을 공유하여 DevOps 민첩성을 높이고 고객 피드백에 더 빠르게 응답하는데 사용될 수 있음.
2. **애플리케이션 개발에 집중**  
AWS 컨테이너 및 서버리스 애플리케이션의 데이터를 유지 및 공유하면서 관리는 전혀 필요하지 않음.
3. **데이터 분석 가속화**  
사용 및 크기 조정이 쉬운 Amazon EFS는 기계 학습 (ML) 및 빅 데이터 분석 워크로드에 필요한 성능 및 일관성을 제공함.
4. **콘텐츠 관리 시스템 개선**  
콘텐츠 관리 시스템 (CMS) 워크로드를 위한 영구 스토리지를 간소화함.  
제품 및 서비스 출시를 앞당기고 저렴한 비용으로 더 안정적이고 안전하게 출시할 수 있음.

이 외에도 EFS는 수천대의 EC2 인스턴스간 파일 시스템 공유가 필요할 때, **병렬 접근이 가능하도록 설계**되어 있어, 두 개 이상의 EC2로부터 하나의 공유된 스토리지 공간이 필요할 때 EFS를 채택하면 됨. 이런 특징들로 인해 EFS는 웹 서비스 환경, 콘텐츠 관리 시스템, 홈 디렉터리, 일반 파일 서비스와 같이 지연 시간에 민감한 애플리케이션에 적합함.

## EFS Architecture

![EFS architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/1c48489f-6239-41f7-973d-05e01117ff18)