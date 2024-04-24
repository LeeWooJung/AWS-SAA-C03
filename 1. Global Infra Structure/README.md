# [Global Infrastructure](https://aws.amazon.com/ko/about-aws/global-infrastructure/)

* **[Regions](https://aws.amazon.com/ko/about-aws/global-infrastructure/regions_az/?p=ngi&loc=2&refid=sl_card)**: AWS는 전 세계에 걸쳐 데이터 센터를 클러스터링하는 물리적 위치인 Region을 갖고 있음.  
각 Region은 최소 세 개의 독립적이고 물리적으로 분리된 Availability Zones(AZ)로 구성.  
 Region은 독립된 전력, 냉각, 물리적 보안을 갖추고 있으며, 초저지연 네트워크를 통해 연결.
* **Availabilty Zones**: AZ는 AWS Region 내의 하나 이상의 독립된 데이터 센터로, 서로 독립적으로 운영되어 고장 내성과 높은 가용성을 제공.  
각 AZ는 독립된 전력, 네트워킹 및 연결성을 가지고 있음.
* **Data Centers**: AWS의 각 AZ는 여러 개의 데이터 센터로 구성되어 있으며, 각 데이터 센터는 고유의 전력, 냉각 시스템을 갖추고 있음.  
이는 AWS가 단일 데이터 센터로 Region을 정의하는 다른 클라우드 제공업체와는 다른 점임.

## Global Infrastructure의 중요 요소

* **리전 및 가용 영역**: AWS는 전 세계에 33개의 지리적 리전 내에 105개의 가용 영역을 운영하고 있으며, 추가 리전 및 가용 영역을 계획 중.
* **보안**: AWS 인프라는 클라우드용으로 구축되었으며, 데이터의 기밀성, 무결성 및 가용성을 보장하기 위해 24시간 모니터링됨.
* **성능**: AWS는 짧은 지연 시간, 낮은 패킷 손실 및 향상된 전체 네트워크 품질을 제공.
* **확장성 및 유연성**: AWS는 비즈니스 요구 사항에 따라 즉시 확장하거나 축소할 수 있는 무한한 확장성을 제공.

## Region 선택 시 고려할 점

* **고객 근접성**: 사용자와 서비스 대상이 되는 고객의 위치에 가까운 리전을 선택하여 네트워크 지연 시간을 최소화.
* **[서비스 가용성](https://aws.amazon.com/ko/about-aws/global-infrastructure/regional-product-services/?p=ngi&loc=4&refid=sl_card)**: 특정 리전에서 원하는 AWS 서비스가 제공되는지 확인. 일부 서비스는 특정 리전에서만 사용할 수 있음.
* **데이터 거버넌스 및 법적 요구 사항**: 서비스 대상 국가의 데이터 보호 법규와 규제를 준수하는 리전을 선택.  
Ex) GDPR이나 CCPA와 같은 법적 요구사항을 고려.
* **비용**: 리전별로 서비스 비용이 다를 수 있으므로, 비용 효율성을 고려하여 선택.
* **내결함성**, **안정성**, **다중 가용 영역(Availibility Zone)**, **고가용성(High Availability)**

## Diagram

![Region](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/4e2f5f74-9fe6-42fa-b2dd-a97ad99986a9)