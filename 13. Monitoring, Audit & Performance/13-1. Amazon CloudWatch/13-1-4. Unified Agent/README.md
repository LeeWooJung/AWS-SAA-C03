# [CloudWatch Unified Agent](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Install-CloudWatch-Agent.html)

Amazon CloudWatch Unified Agent는 AWS에서 제공하는 **통합 모니터링 에이전트**임. 

**시스템 메트릭과 로그 데이터를 수집하여 Amazon CloudWatch에 전송**함. 

이 에이전트는 **CPU, 메모리, RAM, Processes, 디스크 I/O 등의 시스템 메트릭을 모니터링**하고, 다양한 로그 파일에서 데이터를 수집하여 중앙에서 관리할 수 있도록 함. 

이를 통해 인프라의 성능을 모니터링하고, 로그 분석을 수행할 수 있음.

이를 통해 **단일 에이전트로 인스턴스의 성능 및 로그 데이터를 모니터링**할 수 있음. 

**System Manager Parameter Store**를 사용하여 중앙화된 구성이 가능함.

**CloudWatch Unified Agent는 CloudWatch Logs Agent와 CloudWatch Monitoring Scripts의 기능을 결합한 더 발전된 형태**임.

## 특징

### 통합 데이터 수집

**시스템 메트릭과 로그 데이터를 동시에 수집**하여 단일 에이전트로 관리할 수 있음.

### 다양한 메트릭 지원

**CPU 사용량, 메모리 사용량, 디스크 I/O, 네트워크 트래픽 등 다양한 시스템 메트릭을 수집**함.

### 로그 파일 수집

다양한 형식의 로그 파일을 수집하여 CloudWatch Logs로 전송할 수 있음.

### 확장 가능

**사용자 정의 메트릭을 추가로 수집하고, 플러그인을 통해 기능을 확장**할 수 있음.

### 자동화된 배포

**AWS Systems Manager와 통합하여 에이전트 설치 및 구성을 자동화**할 수 있음.

### 실시간 모니터링

수집된 데이터를 실시간으로 CloudWatch 대시보드에서 모니터링할 수 있음.


## 구성요소

* **CloudWatch Metrics**

    서버의 성능 지표를 수집하고 모니터링함.

* **CloudWatch Logs**

    서버의 로그 데이터를 수집하여 중앙에서 관리함.

* **Unified Agent Configuration**

    **에이전트의 설정 파일로, 수집할 메트릭과 로그 파일 경로 등을 지정**함.

* **플러그인 시스템**

    다양한 플러그인을 통해 에이전트의 기능을 확장할 수 있음.

## Metrics

Linux 서버 혹은 EC2 instacne에서 직접적으로 수집됨.

* **CPU**: Active, Guest, Idle, System, User, Steal

* **Disk Metrics**: Free, Used, Total, Disk I/O(Writes, Reads, Bytes, Iops)

* **RAM**: Free, Inactive, Used, Total, Cached

* **Netstat**: Number of TCP & UDP connections, Net packets, Bytes

* **Processes**: Total, Dead, Bloqued, Idle, Running, Sleep

* **Swap Space**: Free, Used, Used Percentage

## 아키텍처

### 데이터 수집

Unified Agent는 **서버에서 메트릭과 로그 데이터를 수집**함. 

메트릭 수집은 다양한 시스템 자원(CPU, 메모리, 디스크 등)을 모니터링함.

### 데이터 전송

수집된 메트릭과 로그 데이터는 Amazon CloudWatch로 전송됨. 

데이터는 CloudWatch에 저장되고, 대시보드에서 실시간으로 확인할 수 있음.

### 데이터 저장 및 분석

CloudWatch는 수집된 데이터를 저장하고, 이를 기반으로 알림 설정, 시각화, 분석을 수행함.

### 결과 시각화 및 알림

CloudWatch **대시보드를 사용하여 데이터 시각화와 알림을 설정**할 수 있음.

이를 통해 시스템 상태를 실시간으로 모니터링하고, 이상 징후를 빠르게 감지할 수 있음.

## 장점

* **단일 에이전트 관리**

    메트릭과 로그 데이터를 **단일 에이전트로 관리할 수 있어 운영 효율성**을 높임.

* **확장성**

    다양한 메트릭과 로그 파일을 지원하고, 플러그인을 통해 기능을 확장할 수 있음.

* **실시간 모니터링**

    실시간 데이터 수집과 모니터링을 통해 시스템 상태를 신속하게 파악할 수 있음.

* **자동화된 배포**

    **AWS Systems Manager와의 통합**으로 에이전트 설치 및 구성을 자동화할 수 있음.

## 단점

* **설정 복잡성**

    다양한 기능을 제공하기 때문에 설정이 복잡할 수 있음. 
    
    초기 설정 시 주의가 필요함.

* **비용**

    대규모 데이터 수집과 저장에 따른 비용이 발생할 수 있음. 
    
    특히 많은 양의 로그 데이터를 수집할 경우 비용이 증가할 수 있음.

* **리소스 사용**

    **에이전트가 서버 자원을 사용하기 때문에, 리소스가 제한된 환경에서는 성능에 영향**을 줄 수 있음.

## Use case

* **서버 성능 모니터링**

    CPU, 메모리, 디스크 사용량 등을 모니터링하여 서버 성능을 실시간으로 확인하고 관리할 수 있음.

* **로그 분석 및 관리**

    애플리케이션 로그, 시스템 로그 등을 수집하여 중앙에서 분석하고 관리할 수 있음.

* **알림 설정**

    특정 메트릭 임계값을 설정하여 이상 징후가 발생하면 즉시 알림을 받을 수 있음.

* **운영 문제 해결**

    실시간 모니터링 데이터를 활용하여 운영 중 발생하는 문제를 신속하게 해결할 수 있음.

## Summary

Amazon CloudWatch Unified Agent는 **메트릭과 로그 데이터를 통합적으로 수집하여 Amazon CloudWatch로 전송하는 에이전트**임. 

다양한 시스템 메트릭과 로그 파일을 지원하며, **단일 에이전트로 관리**할 수 있음. 

실시간 모니터링, 자동화된 배포, 확장성 등의 장점을 제공함. 

설정이 다소 복잡할 수 있지만, 서버 성능 모니터링, 로그 관리, 알림 설정 등 다양한 사용 사례에서 유용하게 활용될 수 있음.