# Backups for Disaster Recovery

Amazon DynamoDB에서 백업 및 복구는 **데이터 손실을 방지하고, 장애 발생 시 데이터를 복구하기 위한 중요한 기능**임.   

DynamoDB는 **지속적인 백업과 수동 백업** 기능을 제공하여 데이터를 안전하게 보호하고 관리할 수 있음.

## 주요 백업 기능

### Point-in-Time Recovery (PITR)

PITR은 DynamoDB 테이블의 **지속적인 백업**을 자동으로 수행하는 기능임.  

**데이터 손실이 발생한 시점 이전의 특정 시간으로 데이터를 복구**할 수 있음.  

**최대 35일 전**까지의 데이터를 복구할 수 있음.

### 수동 백업(On-demand Backups)

필요에 따라 **사용자가 수동으로 테이블의 전체 백업을 생성**할 수 있음.  

수동 백업은 **특정 이벤트나 스케줄에 따라 생성**할 수 있으며, **보관 기간에 제한이 없음**.

DynamoDB의 Latency와 Performance에 영향을 주지 않음.

**AWS Backup**에서 관리되고 구성될 수 있음(Cross Region 복사가 가능함).

## 백업 및 복구 설정 방법

### PITR 활성화

DynamoDB 콘솔에서 테이블을 선택하고, **백업 및 복구** 섹션에서 **PITR을 활성화**함.

활성화 후 DynamoDB는 테이블의 데이터를 지속적으로 백업함.

### 수동 백업 생성

DynamoDB 콘솔에서 테이블을 선택하고 **백업 만들기**를 클릭하여 백업을 생성함.  

**백업 이름을 지정하고, 백업 프로세스를 시작**함.

백업이 완료되면 해당 백업은 **백업 리스트에 표시**됨.

### 데이터 복구

PITR 또는 수동 백업을 사용하여 데이터를 복구할 수 있음.

Recovery를 진행할 때 **새로운 테이블을 생성**함.

**복구할 테이블을 선택하고, 복구할 시간 또는 백업을 선택**함.

복구 프로세스를 시작하면 DynamoDB는 데이터를 지정된 시간 또는 백업 시점으로 복구함.

## Example

**PITR 활성화**

``` python
import boto3

dynamodb = boto3.client('dynamodb')

response = dynamodb.update_continuous_backups(
    TableName='YourTableName',
    PointInTimeRecoverySpecification={
        'PointInTimeRecoveryEnabled': True
    }
)
print(response)
```

**On-demand 백업 활성화**

``` python
import boto3

dynamodb = boto3.client('dynamodb')

response = dynamodb.create_backup(
    TableName='YourTableName',
    BackupName='YourBackupName'
)
print(response)
```

## 장점

### 데이터 보호
PITR과 수동 백업을 통해 데이터 손실을 방지하고, 중요한 데이터를 안전하게 보호할 수 있음.

### 자동화
PITR은 자동으로 지속적인 백업을 수행하므로, 백업 관리에 대한 부담을 줄일 수 있음.

### 유연한 복구 옵션
**특정 시점으로의 복구와 수동 백업을 통한 복구 모두 가능하여 유연한 데이터 복구**가 가능함.

## 단점

### 비용

PITR과 수동 백업 **모두 추가 비용이 발생**함. 

특히 대규모 테이블의 경우 비용이 많이 들 수 있음.

### 복구 시간

대규모 데이터의 경우 복구 시간이 오래 걸릴 수 있음.

### 관리 복잡성

여러 백업을 관리하고, 적절한 복구 시점을 선택하는 과정이 복잡할 수 있음.


## Summary
Amazon DynamoDB의 백업 및 복구 기능은 데이터 손실 방지와 장애 복구를 위해 중요한 역할을 함.  

PITR과 수동 백업을 통해 데이터를 안전하게 보호하고, 필요 시 신속하게 복구할 수 있음.