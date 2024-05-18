# [General Purpose SSD](https://aws.amazon.com/ko/about-aws/whats-new/2014/06/16/introducing-the-amazon-ebs-general-purpose-ssd-volume-type/#:~:text=General%20Purpose%20%28SSD%29%20volumes%20are%20our%20new%20default,databases%2C%20development%20and%20test%20environments%2C%20and%20boot%20volumes.)

## General Purpose SSD

### 설명

General Purpose SSD 볼륨은 **Amazon EBS gp3 볼륨**으로, 저장 용량에 관계없이 성능을 독립적으로 프로비저닝할 수 있게 해주며, 기존 gp2 볼륨보다 GB당 **최대 20% 낮은 가격**으로 제공되었음.  
이 볼륨은 MySQL, Cassandra, 가상 데스크톱, Hadoop 분석 클러스터와 같이 비용 대비 높은 성능이 필요한 다양한 애플리케이션에 이상적임.

사용자는 추가적인 블록 스토리지 용량을 프로비저닝하지 않고도 **IOPS(초당 입출력 작업 수)와 처리량을 확장**할 수 있으며, 이는 사용자가 필요한 저장소만큼만 비용을 지불한다는 것을 의미함.  
gp3 볼륨은 모든 볼륨 크기에 상관없이 3,000 IOPS의 예측 가능한 기본 성능을 제공함.

또한, Microsoft SQL Server 및 Oracle과 같은 중간 크기의 단일 인스턴스 데이터베이스, Kafka와 Spark와 같은 프레임워크를 기반으로 한 **지연 시간에 민감한 대화형 애플리케이션, 개발/테스트 환경 등 대부분의 애플리케이션에 대한 IOPS 및 처리량 요구 사항을 충족시키기 위해 비용 효율적**임.

더 높은 성능이 필요한 경우, 사용자는 추가 용량을 추가하지 않고도 필요한 IOPS나 처리량을 프로비저닝할 수 있음.  
이러한 특성으로 인해 General Purpose SSD 볼륨은 **부팅 볼륨, 중형 데이터베이스, 개발 환경, 가상 데스크톱 등 대부분의 워크로드에 적합**함

### 특성
* **내구성**  
99.8% - 99.9%의 내구성(연간 실패율 0.1% - 0.2%).
* **볼륨당 최대 IOPS**  
최대 16,000 IOPS(64 KiB I/O).
* **볼륨당 최대 처리량**  
최대 1,000 MiB/s.
* **볼륨 크기**  
1 GiB에서 16 TiB까지.
* **NVMe 예약**  
지원되지 않음.
* **부팅 볼륨 지원**  
지원됨.
* **멀티 어태치**  
지원되지 않음.
* **처리량 제한**  
볼륨 크기에 따라 128 MiB/s에서 250 MiB/s 사이.

### gp2 vs. gp3

* **gp2**  
저장 용량에 따라 성능이 선형적으로 증가하며, 볼륨 크기가 커질수록 IOPS와 처리량이 증가.  
gp2 볼륨은 최대 16,000 IOPS와 볼륨 크기에 따라 128 MiB/s에서 250 MiB/s 사이의 처리량을 제공.
* **gp3**  
볼륨 크기에 관계없이 예측 가능한 3,000 IOPS의 기본 성능과 125 MiB/s의 처리량을 제공.  
gp3 볼륨은 저장 용량을 늘리지 않고도 IOPS와 처리량을 독립적으로 프로비저닝할 수 있으며, gp2 볼륨에 비해 GB당 최대 20% 낮은 비용으로 제공.

* **정리**  
따라서, gp3 볼륨은 **성능을 유지하면서 비용을 절감하고자 하는 경우에 적합**하며, 필요에 따라 성능을 더 높일 수 있는 유연성을 제공.  
반면에 gp2 볼륨은 **큰 볼륨에서 더 높은 성능을 제공하지만, 성능 향상을 위해 더 큰 저장 용량을 프로비저닝**해야 할 수도 있음.