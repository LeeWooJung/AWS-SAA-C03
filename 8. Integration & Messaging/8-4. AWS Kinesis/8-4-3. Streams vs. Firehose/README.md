# Kinesis Data Streams vs. Firehose

## 공통점

### 실시간 데이터 스트리밍  
두 서비스 모두 **실시간으로 데이터를 스트리밍** 처리할 수 있음.

### 확장성  
데이터 처리량 증가에 따라 자동으로 확장할 수 있음.

### 다양한 데이터 소스  
**다양한 소스**(웹 애플리케이션, IoT 디바이스 등)에서 데이터를 수집할 수 있음.

### 보안  
AWS IAM을 통해 세밀한 액세스 제어를 제공함.

## 차이점

### 관리형 서비스

* **Kinesis Data Streams**  
    * Producer와 Customer에 대한 소스코드를 작성해야 함.

* **Kinesis Data Firehose**
    * 완전 관리형 서비스로 사용자가 소스코드를 작성할 필요가 없음.

### Scaling

* **Kinesis Data Streams**  
    * Shard Splitting 혹은 Merging에 대해서 사용자가 관리해야 함.

* **Kinesis Data Firehose**
    * 자동적으로 스케일링이 진행됨(Auto Scaling).

### 처리 속도

* **Kinesis Data Streams**  
    * Real Time (~ 200ms)

* **Kinesis Data Firehose**
    * Near Real Time

### 데이터 처리 방식

* **Kinesis Data Streams**  
    * 데이터를 **샤드**라는 단위로 나눠서 처리하며, 각 샤드는 **초당 1MB의 데이터 입력과 2MB의 데이터 출력**을 처리할 수 있음.  
    * 데이터를 실시간으로 읽고 처리할 수 있으며, **데이터를 보관하여 재처리**할 수 있음.

* **Kinesis Data Firehose**  
    * 데이터의 **배치 전송**을 자동으로 관리함.  
    * 데이터는 지정된 간격이나 데이터 크기에 도달했을 때 대상에 전송됨.  
    * **실시간 변환 기능**을 제공하며, 데이터를 변환한 후 **저장 가능**함.
    * 데이터를 재처리할 수 없음.

### 데이터 저장 및 전송

* **Kinesis Data Streams**  
    * 사용자가 데이터를 직접 처리하거나, Lambda, Kinesis Analytics 등을 사용하여 처리할 수 있음. 
    * **데이터를 S3, Redshift, Elasticsearch 등으로 전송하려면 추가적인 설정**이 필요함.

* **Kinesis Data Firehose**  
    * 데이터를 S3, Redshift, Elasticsearch, Splunk 등으로 **자동으로 전송**함.  
    * 사용자가 데이터의 전송 방식을 별도로 관리할 필요가 없음.

### 데이터 보존 기간

* **Kinesis Data Streams**  
    * 기본적으로 데이터를 **24시간 동안 보존**하며, 최대 365일 동안 데이터를 보존할 수 있음.

* **Kinesis Data Firehose**   
    * 데이터를 **즉시 전송**하며, 보존 기간을 설정할 수 없음.  
    * 전송된 데이터는 **최종 목적지에 따라 보존**됨.

### 데이터 변환

* **Kinesis Data Streams**  
    * 자체적으로 **데이터 변환 기능을 제공하지 않음**. 
    * 데이터를 처리하기 위해 Lambda 함수 등을 사용해야 함.

* **Kinesis Data Firehose**  
    * **Lambda 함수를 사용하여 데이터를 실시간으로 변환**할 수 있음.  
    * 데이터 전송 전에 변환 작업을 수행할 수 있음.

## Use Case

* **Kinesis Data Streams**  
    * 실시간 데이터 분석, 로그 및 이벤트 데이터 처리, 실시간 대시보드, 실시간 모니터링 및 경고 등에 적합함.

* **Kinesis Data Firehose**  
    * 데이터 웨어하우징, 로그 및 이벤트 데이터 수집 및 저장, 데이터 아카이빙, 스트리밍 데이터의 배치 분석 등에 적합함.

## Summary

* Kinesis Data Streams와 Kinesis Data Firehose는 **실시간 데이터 스트리밍 서비스**를 제공하는 공통점을 가짐. 
* 그러나 Kinesis Data Streams는 **데이터를 샤드 단위로 처리하고 데이터를 보존**할 수 있는 반면, Kinesis Data Firehose는 **데이터를 배치로 전송하며 실시간 데이터 변환 기능을 제공**함.  
* Streams는 실시간 데이터 처리와 분석에, Firehose는 데이터 웨어하우징과 배치 전송에 적합함.