# Auto Scaling

AWS ECS 서비스 **Auto Scaling**은 애플리케이션의 트래픽 변화에 따라 ECS 서비스가 **자동으로 확장되거나 축소되도록 설정할 수 있는 기능**임.  

이를 통해 애플리케이션의 성능을 최적화하고 비용 효율성을 높일 수 있음.  

Fargate는 Serveless이기 때문에 **Auto Scaling을 Setup하기 더 쉬움**.

## 구성 요소

### [Auto Scaling 그룹](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20Compute/3-2.%20Auto%20Scaling%20Group)

EC2 인스턴스를 **자동으로 추가하거나 제거하는 데 사용**됨.

정의된 **최소, 최대, 원하는 수의 인스턴스를 유지하도록 설정**할 수 있음.

### ECS 서비스 Auto Scaling

ECS 서비스 내의 **태스크 수를 자동으로 조절**함.

원하는 태스크 수를 유지하면서 트래픽 변화에 대응할 수 있음.

* **주의**  
    EC2 Level에서 진행되는 EC2 Auto Scaling Group(EC2 instance level)과 ECS Service Auto Scaling(task level)은 다름.

### CloudWatch 알람

**특정 조건이 충족되었을 때 트리거되는 알람**임.

CPU 사용률, 메모리 사용률, 요청 수, Target 별 ALB 요청 수 등의 지표를 기반으로 설정할 수 있음.

## 설정 방법

1. **ECS 클러스터 및 서비스 생성**

    먼저 ECS 클러스터와 서비스를 생성함.  
    서비스에 대한 기본 설정을 완료함.

2. **Auto Scaling 정책 생성**

    AWS Management Console에서 ECS 서비스의 **Auto Scaling 정책**을 생성함.  
    **스케일 인 및 스케일 아웃 정책**을 설정함.  
    각 정책에 대한 트리거 조건을 정의함 (예: CPU 사용률 > 75%일 때 스케일 아웃).

3. **CloudWatch 알람 설정**

    **CloudWatch에서 ECS 서비스와 관련된 지표에 대해 알람**을 설정함.  
    알람이 트리거될 때 Auto Scaling 정책이 실행됨.

## Auto Scaling 정책

* **Target Tracking**  
    특정 CloudWatch Metric에 대한 target value에 기초하여 Scaling을 진행함.

* **Step Scaling**  
    지정된 CloudWatch Alarm에 기초하여 Scaling을 진행함.

* **Scheduled Scaling**  
    예측할 수 있는 변화에 적용하며, 지정된 날짜/시간에 기초하여 Scaling을 진행함.