# Performance Improvement

## Columnar Data 사용

Columnar data 형식은 **데이터를 컬럼별로 저장하는 방식**임. 

대용량 데이터를 분석하거나 특정 컬럼에 대해 반복적으로 쿼리하는 경우에 적합함.

대표적인 예로 **Parquet와 ORC 포맷**이 있음. **Glue**를 사용하여 데이터를 Parquet 혹은 ORC 포맷으로 변경 가능.

이는 로우 기반 저장 방식과 달리 쿼리할 때 **필요한 컬럼만 읽어들여 성능을 높이는 방식**임.

### 장점

* **쿼리 성능 향상**  
    
    필요한 컬럼만 읽어들여 I/O와 처리 시간을 줄일 수 있음.

* **데이터 압축 효율성**

    비슷한 데이터 유형끼리 저장되어 압축 효율이 높음.

### 단점

* **데이터 변환 필요**  
    
    기존 데이터를 컬럼형식으로 변환하는 추가 작업이 필요함.

* **호환성 문제**  
    
    일부 시스템이나 도구는 컬럼형식 데이터를 지원하지 않을 수 있음.

### Example

데이터를 CSV에서 Parquet로 변환하는 예시

``` sql
CREATE TABLE dataset_parquet
WITH (
  format = 'PARQUET'
) AS
SELECT * FROM dataset_csv;
```

## 데이터 압축 사용

데이터를 압축하여 저장하면 **저장 공간을 절약하고, Athena가 데이터를 읽을 때 더 적은 데이터를 스캔**하므로 성능이 향상됨. 

Bzip2, Lz4, Zlip, Zstd, Gzip, Snappy, LZO 등 다양한 압축 포맷을 사용할 수 있음.

### 장점

* **저장 비용 절감**

    압축된 데이터는 저장 공간을 줄여 비용을 절감함.

* **쿼리 성능 향상**

    적은 데이터를 스캔하므로 쿼리 시간이 단축됨.

### 단점

* **추가 CPU 사용**  
    
    데이터 압축 및 해제 과정에서 CPU 자원이 추가로 사용됨.

* **복잡성 증가**

    압축 및 해제 과정을 관리해야 함.

### Example
데이터를 Gzip으로 압축하여 저장하는 예시

``` sql
CREATE TABLE dataset_gzip
WITH (
  format = 'TEXTFILE',
  compression = 'GZIP'
) AS
SELECT * FROM dataset;
```

## S3에 존재하는 데이터셋을 파티셔닝

파티셔닝은 데이터를 **특정 컬럼의 값에 따라 분할하여 저장하는 방법**임.  

예를 들어, 날짜별로 파티셔닝하면 쿼리 시 특정 날짜의 데이터만 스캔하여 성능을 향상시킬 수 있음.

쿼리가 특정 키(예: 날짜, 지역, 카테고리 등)에 따라 자주 필터링되는 경우에 적합함.

### 장점

* **쿼리 성능 향상**  

    필요한 파티션만 스캔하므로 I/O와 처리 시간이 줄어듦.

* **효율적인 데이터 관리**

    데이터 접근 패턴에 따라 데이터를 조직화할 수 있음.

### 단점

* **복잡한 설정**

    파티셔닝을 설계하고 관리하는 데 추가 노력이 필요함.

* **작은 파티션 문제**

    지나치게 작은 파티션이 많으면 오버헤드가 발생할 수 있음.

## 큰 파일 사용하여 오버헤드 감소

작은 파일이 많으면 **각 파일을 읽을 때마다 오버헤드가 발생**하므로, 큰 파일을 사용하면 이러한 오버헤드를 줄일 수 있음.  

일반적으로 **128 MB 이상의 파일을 사용**하는 것이 좋음.


### 장점

* **쿼리 성능 향상**

    작은 파일을 처리하는 오버헤드가 줄어들어 성능이 향상됨.

* **관리 용이성**

    큰 파일은 관리하기가 더 쉬움.

### 단점

* **데이터 갱신 어려움**

    큰 파일을 갱신하거나 삭제하는 작업이 어려울 수 있음.

* **메모리 사용 증가**

    큰 파일을 처리할 때 메모리 사용량이 증가할 수 있음.