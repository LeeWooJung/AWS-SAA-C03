# [Amazon EKS](https://docs.aws.amazon.com/ko_kr/eks/latest/userguide/what-is-eks.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/c586e608-585c-492a-9a0c-b7b17f3901f3" width = "30" height = "30"> AWS EKS

Amazon EKS (Elastic Kubernetes Service)는 **완전관리형 Kubernetes 서비스**로, AWS에서 Kubernetes 애플리케이션을 쉽게 배포, 관리, 확장할 수 있도록 지원함.  

**Kubernetes**는 컨테이너화된 애플리케이션을 자동으로 배포하고 관리, Scaling 하는 오픈 소스 시스템임.  

ECS의 대체제로 유사한 목적을 갖고 있지만, 다른 API를 사용함.

EKS는 이 **Kubernetes 클러스터를 AWS에서 안정적이고 보안적으로 관리할 수 있도록 해줌**.

On-Premise의 Kubernetes 혹은 다은 클라우드의 Kubernetes를 AWS로 이전하고 싶을 때 사용할 수 있음.

여러 Region에 적용하고 싶을 때, 각 Region 당 하나의 EKS Cluster가 필요함.

## 특징

### 완전관리형

AWS에서 **Kubernetes 클러스터의 관리 및 운영을 자동화**하여 사용자 부담을 줄임. 

제어 플레인 (Control Plane)과 워커 노드 (Worker Node)의 운영을 자동화함.

### 통합성

AWS의 다양한 서비스 (VPC, IAM, ELB 등)와 **원활하게 통합**됨.  

**AWS Fargate와 통합되어 서버리스 Kubernetes 배포가 가능**함.

### 보안

**IAM을 사용한 역할 기반 접근 제어** (RBAC) 제공.  

Kubernetes 클러스터와 관련된 모든 데이터는 **자동으로 암호화**됨.

### 확장성

**워커 노드의 자동 확장 기능을 제공**하여, 트래픽 증가 시에도 애플리케이션이 원활하게 동작할 수 있음.  

EKS 클러스터는 필요에 따라 **확장 및 축소 가능**함.

## 기능

### 제어 플레인 관리

EKS는 Kubernetes **제어 플레인의 고가용성 및 자동 패치 기능을 제공**함.  

다중 가용 영역 (Multi-AZ)에 걸쳐 제어 플레인을 **자동으로 분산시켜 가용성을 높임**.

### 네트워킹

AWS **VPC 네트워크 정책을 사용하여 클러스터 내의 통신을 제어**함.  

**[Elastic Load Balancer](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/5.%20Network/5-2.%20Load%20Balancer)** (ELB)을 통해 클러스터 외부로의 접근을 관리함.

### 자동화

**AWS Fargate와 통합하여 서버리스**로 Kubernetes 애플리케이션을 실행할 수 있음.  

**AWS CloudFormation**을 사용하여 Kubernetes 클러스터와 관련 리소스를 **자동으로 배포하고 관리**할 수 있음.

### 모니터링 및 로깅

**Amazon CloudWatch와 통합**되어 클러스터 및 애플리케이션의 모니터링 및 로깅 기능을 제공함.

**Kubernetes에서 기본 제공하는 모니터링 도구와의 통합을 지원**함.

## 아키텍처

### 제어 플레인  
EKS는 관리형 Kubernetes API 서버 및 etcd를 포함하는 **제어 플레인을 운영**함.

### 워커 노드  
EC2 인스턴스 또는 AWS Fargate를 사용하여 **워커 노드를 실행**함.

### 네트워킹  
VPC, 서브넷, 보안 그룹을 통해 네트워크를 구성하고, ELB를 통해 외부 트래픽을 관리함.

### IAM 역할  
**Kubernetes의 RBAC와 AWS IAM을 통합**하여 보안성을 높임.

## 장점

### 보안 및 컴플라이언스  
AWS의 보안 기능과 통합되어 높은 수준의 보안을 제공함.

### 유연성  
**다양한 AWS 서비스와의 통합**을 통해 유연한 애플리케이션 배포 및 관리를 지원함.

### 고가용성  
**다중 가용 영역에 걸쳐 제어 플레인을 분산**하여 고가용성을 제공함.

### 자동화  
자동 확장 및 패치 기능을 통해 운영 부담을 줄임.

## 단점

### 비용  
완전관리형 서비스로 인해 자체 관리 Kubernetes 클러스터보다 비용이 높을 수 있음.

### 학습 곡선  
Kubernetes의 복잡한 구조로 인해 초기 설정 및 운영에 대한 학습이 필요함.

## Summary
Amazon EKS는 Kubernetes 클러스터를 AWS에서 쉽고 안정적으로 운영할 수 있도록 지원하는 **완전관리형 서비스**임.  

**AWS의 다양한 서비스와 통합**되어 유연한 애플리케이션 배포 및 관리를 가능하게 하며, 높은 보안성과 고가용성을 제공함.  

그러나 비용 및 학습 곡선 등의 단점도 존재함.