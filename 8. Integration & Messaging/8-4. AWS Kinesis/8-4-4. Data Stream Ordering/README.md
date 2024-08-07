# Data Stream Ordering

* Kinesis Data Streams에서 **데이터를 순서대로 처리하는 것은 특정 애플리케이션의 중요한 요구사항**일 수 있음.  
* 이를 위해 Kinesis는 **샤드**와 **파티션 키**를 사용하여 데이터 순서를 보장함.

## 샤드(Shard)

* 샤드는 Kinesis Data Streams의 기본 단위임.  
* 각 샤드는 **고유한 순서대로 데이터를 저장**하며, 데이터 레코드의 순서는 각 샤드 내에서 보장됨.  
* 즉, 특정 **샤드에 할당된 모든 레코드는 해당 샤드 내에서 순서대로 처리**됨.

## 파티션 키(Partition Key)

* **파티션 키는 데이터 레코드가 특정 샤드로 라우팅되는 방식을 결정하는 키**임.  
* 데이터 레코드를 스트림에 넣을 때, 각 레코드는 **파티션 키와 함께 전송**됨.  
* Kinesis는 이 **파티션 키를 해싱**하여 특정 샤드로 매핑함.  
* 따라서 **동일한 파티션 키를 가진 모든 데이터 레코드는 동일한 샤드에 할당**됨.

## 순서 보장 메커니즘

* **같은 파티션 키 사용**  
    * 동일한 파티션 키를 사용하면 모든 관련 데이터 레코드는 같은 샤드에 저장되고, 그 순서는 보장됨.  
    * 예를 들어, 특정 사용자 ID를 파티션 키로 사용하면 해당 사용자의 모든 이벤트는 순서대로 처리됨.

* **샤드 내 순서**  
    * 각 샤드 내에서 레코드는 순서대로 저장됨.  
    * 따라서 동일한 파티션 키를 가진 레코드는 그 샤드 내에서 순서가 보장됨.

## 샤드의 분할과 병합

### 샤드 분할  
* 데이터 **처리량이 증가하면, 기존 샤드를 두 개의 새로운 샤드로 분할**하여 처리량을 늘릴 수 있음.  
* 이 과정에서 데이터의 순서는 각 새로운 샤드 내에서 유지됨.

### 샤드 병합  
* 처리량이 감소하면, 두 개의 샤드를 하나로 병합하여 **비용을 절감**할 수 있음.  
* 병합된 샤드는 병합된 두 샤드의 모든 레코드를 포함하며, **각각의 순서는 유지**됨.

## 아키텍처 예시

### 데이터 프로듀서  
* 데이터를 생성하고, 각 데이터 레코드에 파티션 키를 지정하여 Kinesis Data Streams로 전송함.

### Kinesis Data Streams  
* 각 레코드를 **파티션 키에 따라 해싱**하여 특정 샤드로 라우팅함.  
* 샤드 내에서 데이터는 순서대로 저장됨.

### 데이터 컨슈머  
* 각 샤드에서 데이터를 순차적으로 읽어 처리함.  
* 이는 동일한 파티션 키를 가진 데이터가 순서대로 처리되도록 보장함.

## 장점

### 데이터 순서 보장  
동일한 파티션 키를 사용하는 데이터는 순서가 보장됨.

### 확장성  
샤드를 분할하여 더 많은 데이터 처리량을 지원할 수 있음.

### 유연성  
필요에 따라 샤드를 분할하거나 병합할 수 있음.

## 단점

### 복잡성 증가  
파티션 키를 적절히 설계하지 않으면 **데이터가 불균형하게 분포**될 수 있음.

### 비용  
샤드의 수에 따라 비용이 증가할 수 있음.

## Summary
Kinesis Data Streams에서 데이터를 순서대로 처리하기 위해서는 **파티션 키를 적절히 사용하여 동일한 파티션 키를 가진 데이터가 동일한 샤드에 할당되도록 하는 것이 중요**함.  
이를 통해 특정 애플리케이션의 순서 요구사항을 충족시킬 수 있음.
