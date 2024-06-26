# Scalability

## 설명

**Scalability**는 시스템이 조정을 통해 더 많은 양을 처리할 수 있는 능력을 의미하며, 이는 두 가지 주요 유형으로 나뉨

### Vertical Scalability (수직 확장)

* 인스턴스의 크기를 확장하는 것을 의미하며, CPU, RAM, Storage 등의 **리소스를 추가**하는 방식.  
예를 들어, EC2 인스턴스에서 t2.micro를 사용하고 있다면, 이를 t2.large로 업그레이드하는 것이 수직 확장에 해당.  

* Database와 같은 Non distributed system에 주로 사용됨.

### Horizontal Scalability (수평 확장)

* **인스턴스의 수를 늘리는 것**을 의미하며, 동일한 시스템을 병렬의 형태로 확장하는 방식.  
예를 들어, 웹 애플리케이션에서 사용자 트래픽이 증가하면, 새로운 서버를 클러스터에 추가하여 부하를 분산시키는 것이 수평 확장에 해당.

* Distributed System에 주로 사용됨.

## 장단점

### 장점

* 시스템의 성능과 처리 능력을 유지하면서 시스템을 성장시키는 데 도움이 됨.
* 비용 효율성을 향상시킴.

### 단점

* 수직 확장은 일반적으로 확장할 수 있는 정도에 한계가 있음.
* 수평 확장은 프로그램이 수정 될 경우 수 많은 Machine에 배포되어야 하므로 관리하기 어려움.

## Use case
### EC2

**EC2 인스턴스**는 수직 확장을 통해 스케일 업(Scale up)하거나, 수직 축소를 통해 스케일 다운(Scale Down) 할 수 있음.  
또한 수평 확장을 통해 스케일 아웃(Scale out)하거나, 수평 축소를 통해 스케일 인(Scale in)할 수 있음.