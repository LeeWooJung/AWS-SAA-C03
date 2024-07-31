# [AWS Application Discovery Service](https://docs.aws.amazon.com/ko_kr/application-discovery/latest/userguide/what-is-appdiscovery.html)

## <img src = "https://github.com/user-attachments/assets/5d34a0f0-899b-42e7-ac3a-819f1d14d860" width = "25" height = "25"> AWS Application Discovery Service

AWS Application Discovery Service는 **온프레미스 데이터 센터의 애플리케이션, 서버, 데이터베이스, 네트워크 구성 요소, Dependency Mapping 등을 자동으로 탐색하고 수집하는 데 도움을 주는 서비스**임. 

이는 **AWS로 마이그레이션을 계획할 때 필요한 데이터를 제공하여, 마이그레이션 프로세스를 더욱 원활하고 효율적으로 진행**할 수 있도록 지원함.

수집된 데이터는 AWS Migration Hub에서 분석되고 시각화되어, 마이그레이션 작업의 준비 상태를 평가하고 마이그레이션 전략을 수립하는 데 도움을 줌.

## 특징

### 자동 자산 탐색

온프레미스 환경의 서버, 애플리케이션, 네트워크 구성 요소 등을 자동으로 탐색함.

### 종합적인 데이터 수집

**서버 구성, 성능 데이터, 실행 중인 애플리케이션, 네트워크 연결 등 다양한 데이터를 수집**함.

### AWS Migration Hub 통합

수집된 데이터를 **AWS Migration Hub에서 분석하고 시각화하여 마이그레이션 작업을 계획**할 수 있음.

### 에이전트 기반 및 에이전트리스 모드

**에이전트를 설치(AWS Application Discovery Agent)하여 심층 데이터를 수집하거나, 네트워크 트래픽을 통해 데이터를 수집하는 에이전트리스 모드(AWS Agentless Discovery Connector)를 제공**함.

### 데이터 보안

수집된 데이터는 AWS의 보안 프로토콜을 통해 안전하게 전송되고 저장됨.

## 구성요소

* **Discovery Agent**

    각 온프레미스 서버에 설치되어 심층 데이터를 수집하는 소프트웨어 에이전트임.

* **Discovery Connector**

    **에이전트리스 모드**에서 VMware 환경의 데이터를 수집하기 위한 가상 어플라이언스임.

* **Application Discovery Service Console**

    데이터를 관리하고 마이그레이션 준비 상태를 평가할 수 있는 AWS 콘솔임.

* **AWS Migration Hub**

    수집된 데이터를 분석하고 시각화하여 마이그레이션 전략을 수립하는 데 도움을 줌.

## Use case

* **온프레미스에서 AWS로 마이그레이션**

    온프레미스 데이터 센터의 자산을 AWS로 마이그레이션할 때 필요한 데이터를 수집하고 분석함.

* **데이터 센터 평가**

    데이터 센터의 자산과 구성 요소를 평가하여 최적화 방안을 모색함.

* **IT 자산 관리**

    IT 자산의 구성, 성능, 네트워크 연결 등을 중앙에서 관리하고 모니터링함.

* **비용 절감**

    마이그레이션 계획 수립을 통해 불필요한 비용을 절감하고, 효율적인 클라우드 자원 활용을 도모함.

## Sumamry

AWS Application Discovery Service는 온프레미스 데이터 센터의 IT 자산을 자동으로 탐색하고, 데이터를 수집하여 AWS로의 마이그레이션을 지원하는 **완전 관리형 서비스**임. 

이를 통해 서버 구성, 성능 데이터, 네트워크 연결 등을 수집하고 분석하여, 마이그레이션 계획을 수립하고 실행할 수 있음. 

**AWS Migration Hub와 통합**되어 데이터 분석과 시각화를 지원하며, 자동화된 탐색과 데이터 수집을 통해 마이그레이션 과정의 효율성을 높임. 

그러나 에이전트 설치와 관리의 복잡성, 추가 비용 등의 단점도 고려해야 함.