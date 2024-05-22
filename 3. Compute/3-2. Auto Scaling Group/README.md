# [Auto Scaling Group](https://docs.aws.amazon.com/ko_kr/autoscaling/ec2/userguide/auto-scaling-groups.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/3006fba4-dabf-4717-b4eb-5088a0bd542e" width = "20" height = "20"> Auto Scaling Group

### 설명

* **AWS Auto Scaling Group** (ASG)는 애플리케이션의 수요에 따라 자동으로 EC2 인스턴스의 수를 조정하여 가용성과 비용 효율성을 보장하는 서비스.  
이를 통해 사용자는 트래픽 변화에 대응할 수 있고, 자원을 적절하게 배치하여 성능을 유지할 수 있음.

### 목표

* 증가된 부하에 대해 서버의 부하를 줄이고자 배정된 EC2 인스턴스를 증가시킨다(Scale out).
* 감소된 부하에 대해 유휴 자원을 줄이고자 배정된 EC2 인스턴스를 감소시킨다(Scale in).
* 설정한 최소/최대 EC2 인스턴스의 개수를 유지한다.
* 자동으로 새로운 인스턴스를 [Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer)에 할당한다.
* 오작동(unhealthy)으로 인해 종료된 EC2 인스턴스가 있을 경우 해당 EC2 인스턴스를 대신하는 새로운 인스턴스를 생성하여 할당한다.

### 구성 요소

1. **Auto Scaling Group**  

    * **Launch Configuration / Launch Template**  
    ASG에서 [EC2 인스턴스](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-1.%20EC2)를 생성할 때 사용하는 설정.  
    
    * Launch Template 구성 요소
        - AMI, EC2 인스턴스 유형
        - EC2 User Data
        - [EBS 볼륨](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-1.%20EBS)
        - [Security Groups](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/4.%20Security%20Group)
        - SSH Key Pair
        - [IAM Role](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/2.%20Identity%20and%20Access(IAM)) for EC2 인스턴스
        - VPC + Subent
        - [Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer)

    * **Desired Capacity**  
    ASG가 유지하려고 하는 인스턴스의 목표 개수. 필요에 따라 인스턴스 수가 이 값에 맞게 조정됨.

    * **Minimum Size**  
    ASG가 유지해야 하는 인스턴스의 **최소 개수**.

    * **Maximum Size**  
    ASG가 유지할 수 있는 인스턴스의 **최대 개수**.

    * **Scaling Policies**  
    트리거 조건을 정의하여 인스턴스 수를 자동으로 조정하는 정책.

2. **Scaling Policies**

    * **Dynamic Scaling**
        * **Target Tracking Scaling**  
        특정 지표(예: CPU 사용률)가 **목표 값에 맞춰지도록 인스턴스 수를 조정**.  
        ex) 목표 값: Average CPU Usage 30%

        * **Step Scaling**  
        지정된 지표가 임계 값을 초과할 때마다 **단계별로 조정**.

        * **Simple Scaling**  
        지정된 조건을 충족할 때마다 일정한 수의 **인스턴스를 추가하거나 제거**.

    * **Scheduled Scaling**
        * 기존 Pattern을 사용하여 지표를 예측하고 scheduling  
        ex) 오후 10시에 접속자 수 폭증이 예측 되므로 min capacity를 늘려 놓음.

3. **Health Checks**

    * **EC2 Health Check**  
    [EC2](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-1.%20EC2) 인스턴스의 상태를 모니터링하고, 비정상 인스턴스를 자동으로 교체.

    * **ELB Health Check**  
    [ELB](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer)와 연계하여 인스턴스의 상태를 확인하고, 비정상 인스턴스를 교체.

4. **Lifecycle Hooks**

    * 인스턴스가 **시작**되거나 **종료**될 때 **사용자 정의 작업을 수행**할 수 있음.  
    예를 들어, 인스턴스가 시작되기 전에 초기 설정 작업을 수행하거나, 종료되기 전에 데이터를 백업할 수 있음.

5. **Cooldown Period**

    * 확장 또는 축소 작업 후 일정 기간 동안 **추가 작업을 지연**시켜 시스템이 안정될 시간을 제공. 이는 불필요한 조정 작업을 방지하고 시스템의 안정성을 유지함.
    * **Cooldown 기간 동안 ASG는 EC2 인스턴스를 시작하거나 종료하지 않음**.
    * Default: 300 secs
    * [Ready-to-use AMI](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-1.%20EC2/3-1-3.%20AMI)를 사용하여 cool down 기간을 낮추는 것이 좋음.

### ASG 동작

1. **인스턴스 시작**

    * ASG는 지정된 Launch Configuration 또는 Launch Template을 사용하여 EC2 인스턴스를 시작함.
    * 인스턴스가 시작되면 ASG는 이를 모니터링하여 상태를 확인함.

2. **수요 변화 대응**

    * **트래픽 증가 시**: Scaling Policies에 따라 인스턴스를 추가로 시작함.
    * **트래픽 감소 시**: 필요에 따라 인스턴스를 종료하여 비용을 절감함.

3. **인스턴스 종료**

    * **비정상 인스턴스 발견 시**: ASG는 비정상 인스턴스를 종료하고 새로운 인스턴스를 시작함.
    * **수요 감소 시**: ASG는 인스턴스 수를 줄여 최적화된 자원 활용을 유지함.

### Use Case

1. **웹 애플리케이션 스케일링**
    * 웹 서버 트래픽이 증가할 때 인스턴스를 자동으로 추가하여 처리 능력을 확장.
    * 트래픽이 감소하면 인스턴스를 자동으로 종료하여 비용을 절감.

2. **비즈니스 로직 처리**
    * 데이터 처리 작업이 증가할 때 백그라운드 작업 서버의 인스턴스 수를 증가시킴.
    * 작업이 완료되면 인스턴스를 줄여 비용을 최적화함.

### 비용

* ASG를 사용하는 것은 Free.
* ASG로 인해 생성된 EC2 instance에 대해서만 비용을 지불 함.

## ASG Code Example

1. **Launch Template 생성**
    ```bash
    aws ec2 create-launch-template --launch-template-name my-template --version-description my-version --launch-template-data '{"ImageId":"ami-0abcdef1234567890","InstanceType":"t2.micro","KeyName":"my-key"}'
    ```

2. **Auto Scaling Group 생성**

    ```bash
    aws autoscaling create-auto-scaling-group --auto-scaling-group-name my-asg --launch-template "LaunchTemplateName=my-template,Version=1" --min-size 1 --max-size 5 --desired-capacity 2 --vpc-zone-identifier "subnet-12345678"
    ```

3. **Scaling Policy 설정**

    ```bash
    aws autoscaling put-scaling-policy --auto-scaling-group-name my-asg --policy-name scale-out --scaling-adjustment 1 --adjustment-type ChangeInCapacity
    ```

## ASG with Cloud Watch

* Cloud Watch의 alarm을 trigger 삼아 ASG Scale 조정 가능.
    - **Average CPU Usage** 등의 Metric을 지표로 하여 ASG Scale 조정 가능.
        - **Scale out**
        - **Scale in**

## ASG Architecture

### Auto Scaling Group with Load Balancer

![ASG architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/f5f3d433-ef15-406a-add7-2a379fe6edda)
