# [AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AMIs.html)

## Amazon Machine Image

### 설명    

**Amazon Machine Image**(AMI)

Amazon EC2 인스턴스를 시작하는 데 필요한 정보를 제공하는 이미지.  
AMI는 기본적으로 새로 시작된 인스턴스에 연결될 디스크의 복사본임. 일반적으로 부팅 디스크만 포함하지만, AMI는 실제로 여러 디스크 이미지를 포함할 수 있음.  
AMI는 새로 시작된 인스턴스의 디스크에 **복사**되며, 이를 통해 인스턴스를 시작할 때 필요한 모든 정보를 제공

---------------------------------------------
### 적용

**AMI**는 특정 AWS Region에서 생성되며, 해당 Region 내의 EC2 인스턴스에서만 직접 사용할 수 있음.  
하지만, 다른 Region에서 동일한 AMI를 사용하려는 경우, AMI를 해당 Region으로 **복사**할 수 있음.  
이를 통해 원하는 Region의 EC2 인스턴스에서 AMI를 사용하여 인스턴스를 시작할 수 있음.

---------------------------------------------

### 사용
AMI를 생성하면, 이는 **Amazon S3**에 저장되며, 이는 사용자가 직접 액세스할 수 없는 S3 버킷에 저장됨.  
Amazon EC2에서 실행되는 애플리케이션에 안정적이고 안전한 고성능 실행 환경을 제공할 수 있도록 설계되었음.

---------------------------------------------

### AMI Architecture

![AMI](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/4bca120d-cc59-4aef-bbc2-826ca06a2905)

### 카테고리

---------------------------------------------

1. **Public AMIs**  
AWS가 소유하거나 사용자가 공유한 AMI로, 누구나 사용할 수 있음.  
이들은 인기 있는 소프트웨어 패키지로 사전 구성되어 있음.
2. **Private AMIs (Own AMI)**  
사용자가 자신의 사용을 위해 생성한 AMI.  
이들은 사용자가 필요로 하는 특정 애플리케이션과 설정으로 구성될 수 있음.
3. **Marketplace AMIs**  
AWS Marketplace에서 제공하는 AMI로, 다양한 소프트웨어 벤더들이 제공하는 솔루션을 포함함. 이들은 특정 소프트웨어 또는 서비스를 실행하는 데 필요한 모든 구성을 포함하고 있음.

---------------------------------------------

1. **Amazon EBS-Backed AMIs**  
AMI는 Amazon Elastic Block Store(EBS)에 의해 지원됨.  
이들은 EBS 볼륨에서 시작되며, 인스턴스가 중지된 후에도 데이터가 유지됨.
2. **Instance Store-Backed AMIs**  
AMI는 인스턴스 스토어에 의해 지원됨.  
이들은 인스턴스 스토어 볼륨에서 시작되며, 인스턴스가 중지되면 데이터가 유실됨.

## Ready-to-use AMI

애플리케이션 및 종속성이 사전 구성된 상태로, 인스턴스가 시작되자마자 **즉시 사용 가능하도록 준비된 AMI**.

### 장점

* **빠른 시작 시간**  
인스턴스가 시작되자마자 애플리케이션이 실행될 준비가 되어 있으므로, 인스턴스 준비 시간이 크게 단축됨.
* **일관성**  
모든 인스턴스가 동일한 환경에서 시작되므로, **구성 오류가 줄어들고 일관된 성능을 유지**할 수 있음.
* **관리 용이성**  
애플리케이션 업데이트나 종속성 변경 시 새로운 AMI를 생성하여 배포하면 되므로 관리가 간편해짐.

### 설정 방법

1. AMI 생성
    * **EC2 인스턴스 설정**  
    필요한 소프트웨어, 라이브러리 및 애플리케이션을 설치한 후, 모든 설정을 완료한 EC2 인스턴스를 생성.
    * **이미지 생성**  
    설정이 완료된 인스턴스에서 AMI를 생성.

        ```bash
        aws ec2 create-image --instance-id i-1234567890abcdef0 --name "MyReadyToUseAMI" --no-reboot
        ```

2. Auto Scaling Group에 AMI 적용
    * **Launch Template 생성**  
    생성한 AMI를 사용하여 Launch Template을 생성.

        ```bash
        aws ec2 create-launch-template --launch-template-name my-launch-template --version-description "v1" --launch-template-data '{
            "ImageId": "ami-0abcdef1234567890",
            "InstanceType": "t2.micro",
            "KeyName": "my-key-pair",
            "SecurityGroupIds": ["sg-0123456789abcdef0"]
        }'
        ```

    * **Auto Scaling Group에 적용**  
    위에서 생성한 Launch Template을 사용하여 Auto Scaling Group을 생성하거나 기존 Auto Scaling Group을 업데이트.

        * Auto Scaling Group 생성
            ```bash
            aws autoscaling create-auto-scaling-group --auto-scaling-group-name my-asg --launch-configuration-name my-launch-config --min-size 1 --max-size 5 --desired-capacity 2 --vpc-zone-identifier subnet-0123456789abcdef0
            ```
        * Auto Scaling Group 업데이트
            ```bash
            aws autoscaling update-auto-scaling-group --auto-scaling-group-name my-asg --launch-configuration-name my-launch-config
            ```

### 종합

ready-to-use AMI를 사용하면 인스턴스가 시작되자마자 애플리케이션이 즉시 실행될 수 있어, **ASG의 Cooldown 기간을 줄이고 응답 시간을 최소화할 수 있음**.  
이 방법은 특히 트래픽 변화에 빠르게 대응해야 하는 경우에 유용.

### 주의 사항

* AMI를 정기적으로 업데이트하여 최신 패치 및 애플리케이션 버전을 포함하도록 해야함.
* AMI 생성 및 배포 프로세스를 자동화하면 관리 효율성이 더욱 높아짐.