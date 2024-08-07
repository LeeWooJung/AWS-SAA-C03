# Multi Region Secrets

AWS Secrets Manager의 Multi-Region Secrets 기능은 **비밀 정보를 여러 AWS 리전에 걸쳐 자동으로 복제하여 고가용성과 재해 복구 기능을 제공하는 기능**임. 

이를 통해 **애플리케이션이 여러 리전에 분산되어 있을 때 동일한 비밀 정보를 공유할 수 있으며, 한 리전에 장애가 발생하더라도 다른 리전에서 계속해서 비밀 정보를 사용**할 수 있음.

## 특징

### 자동 복제

비밀 정보가 생성되면 선택한 리전에 자동으로 복제됨.

### 동기화

원본 비밀 정보가 업데이트되면, 모든 복제된 리전에서도 자동으로 동기화됨.

### 고가용성

여러 리전에 비밀 정보를 복제하여 높은 가용성을 제공함.

### 재해 복구

한 리전에서 비밀 정보에 접근할 수 없는 경우 다른 리전에서 접근할 수 있음.

### 간편한 관리

콘솔, CLI, SDK를 통해 손쉽게 Multi-Region Secrets을 관리할 수 있음.

## 구성요소

* **원본 비밀 정보**(Primary Secret)

    기본 리전에 저장된 비밀 정보임.

* **복제된 비밀 정보**(Replica Secret)

    원본 비밀 정보가 복제된 리전에 저장된 비밀 정보임.

* **비밀 정보 ARN**(Secret ARN)

    각 리전에서 비밀 정보를 고유하게 식별할 수 있는 ARN임.

## 장점

* **고가용성**

    여러 리전에 비밀 정보를 저장하여 높은 가용성을 제공함.

* **재해 복구**

    한 리전에 장애가 발생하더라도 다른 리전에서 비밀 정보를 사용할 수 있음.

* **자동 동기화**

    비밀 정보가 변경될 때 모든 복제된 리전에서 자동으로 동기화됨.

* **간편한 관리**

    콘솔, CLI, SDK를 통해 손쉽게 관리할 수 있음.

## 단점

* **추가 비용**

    여러 리전에 비밀 정보를 복제하여 저장하므로 추가 비용이 발생할 수 있음.

* **복잡성 증가**

    여러 리전에 걸쳐 비밀 정보를 관리해야 하므로 관리 복잡성이 증가할 수 있음.

## Use case

* **글로벌 애플리케이션**

    여러 리전에 분산된 애플리케이션이 동일한 비밀 정보를 필요로 할 때.

* **재해 복구 계획**

    재해 복구 시나리오에서 중요한 비밀 정보를 여러 리전에 저장하여 가용성을 높이고 복구 시간을 단축할 때.

* **고가용성 요구 사항**

    비즈니스 연속성을 위해 고가용성을 유지해야 하는 경우.

## Summary

AWS Secrets Manager의 Multi-Region Secrets 기능은 **비밀 정보를 여러 리전에 자동으로 복제하여 고가용성과 재해 복구 기능을 제공**함. 

이를 통해 글로벌 애플리케이션이 동일한 비밀 정보를 공유할 수 있으며, **한 리전에 장애가 발생하더라도 다른 리전에서 계속해서 비밀 정보를 사용**할 수 있음. 

추가 비용이 발생할 수 있으며, 관리 복잡성이 증가할 수 있으나, 높은 가용성과 재해 복구 기능을 제공하는 큰 장점이 있음.