# [Connection Types](https://docs.aws.amazon.com/directconnect/latest/UserGuide/WorkingWithConnections.html)

AWS Direct Connect는 사용자의 온프레미스 네트워크와 AWS 클라우드 간에 전용 네트워크 연결을 제공하는 서비스임. 

이 서비스는 **다양한 연결 유형을 제공하여 사용자가 요구에 맞게 선택**할 수 있도록 함.

새로운 Connection을 설치하기 위해 **한 달**이상의 시간이 소요됨.

## Dedicated Connections

Dedicated Connections는 **사용자와 AWS 간에 직접 연결되는 전용 회선**임. 

이는 사용자가 **AWS Direct Connect 로케이션에서 자신의 네트워크 장비와 AWS 장비를 직접 연결**하는 형태임.

### 특징

* **대역폭 옵션**

    1Gbps, 10Gbps, 100Gbps 등 다양한 대역폭을 지원함.

* **직접 연결**

    **사용자의 네트워크 장비와 AWS 네트워크 장비가 직접 연결되어 높은 성능과 안정성을 제공**함.

* **서비스 제공자 필요**

    사용자는 AWS Direct Connect 로케이션에서 네트워크 장비를 설치하거나, 네트워크 서비스 제공자와 협력하여 연결을 설정해야 함.

### Use case

* 고대역폭 데이터 전송이 필요한 기업

* 대규모 데이터 마이그레이션 및 백업 작업

* 고성능 및 저지연 연결이 필요한 애플리케이션

## Hosted Connections

Hosted Connections는 **AWS 파트너 네트워크(APN) 제공자가 제공하는 간접 연결**임. 

이는 **사용자와 AWS 간의 연결이 네트워크 서비스 제공자를 통해 이루어지는 형태**임.

### 특징

* **대역폭 옵션**

    50Mbps에서 10Gbps까지 다양한 대역폭을 지원함.

    대역폭은 요청에 의해 추가되거나 제거될 수 있음.

* **빠른 설정**

    직접 연결보다 설정이 간편하고 빠름.

* **서비스 제공자**

    사용자는 AWS APN 제공자와 협력하여 연결을 설정함.

### Use case

* 중소기업 및 스타트업
* 빠른 설정이 필요한 경우
* 중소규모 데이터 전송 및 백업 작업