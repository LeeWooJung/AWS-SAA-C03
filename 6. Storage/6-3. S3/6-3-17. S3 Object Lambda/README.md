# [S3 Object Lambda](https://aws.amazon.com/ko/blogs/korea/introducing-amazon-s3-object-lambda-use-your-code-to-process-data-as-it-is-being-retrieved-from-s3/)

## S3 Object Lambda

* Amazon S3 Object Lambda는 S3 버킷의 객체에 액세스할 때 **AWS Lambda 함수를 호출하여 데이터의 변환이나 처리를 수행하는 기능**.  
* 이를 통해 애플리케이션을 수정하지 않고도 **객체를 동적으로 변환하거나 필터링**할 수 있음.
* S3 Access Point와 S3 Object Lambda Access Point 위에 단 하나의 S3 Bucket만 있어도 됨.

### 특징

* **실시간 데이터 처리**  
데이터를 가져오는 동안 **실시간으로 데이터를 변환하거나 처리**할 수 있음.
* **무제한 확장성**  
Lambda의 확장성을 통해 다양한 데이터 처리 요구를 충족할 수 있음.
* **유연성**  
다양한 **데이터 변환 작업**을 수행할 수 있으며, 이미지 리사이징, 데이터 마스킹, 필터링 등의 작업을 포함함.

### 작동 방식

1. **Lambda 함수 작성**  
데이터를 처리할 Lambda 함수를 작성함.

2. **Object Lambda Access Point 생성**  
S3 버킷에 Object Lambda Access Point를 생성하고, 해당 Access Point에 Lambda 함수를 연결함.

3. **데이터 요청**  
애플리케이션이 Object Lambda Access Point를 통해 데이터를 요청하면, Lambda 함수가 호출되어 데이터를 처리하고 반환함.

### 장점

* **무중단 데이터 처리**  
데이터를 변환하기 위해 애플리케이션을 변경할 필요가 없음.
* **유연한 데이터 접근**  
다양한 데이터 변환 요구를 충족할 수 있음.
* **보안 강화**  
데이터 요청 시 실시간으로 데이터를 필터링하거나 마스킹하여 보안을 강화할 수 있음.

### 단점

* **추가 비용**  
Lambda 호출에 따른 추가 비용이 발생할 수 있음.
* **복잡성 증가**  
데이터 처리를 위해 Lambda 함수를 작성하고 관리해야 하므로 복잡성이 증가할 수 있음.

### 기본 구성

* **S3 버킷**  
데이터를 저장하는 기본 스토리지.
* **Object Lambda Access Point**  
데이터를 처리하기 위한 Access Point.
* **Lambda 함수**  
데이터를 변환하거나 처리하는 코드.

### 동작 예시

1. 애플리케이션이 **S3 Object Lambda Access Point를 통해 데이터를 요청**함.  
2. Object Lambda Access Point가 **Lambda 함수를 호출하여 요청된 데이터를 처리**함.
3. Lambda 함수가 데이터를 변환하거나 필터링한 후, **결과를 반환**함.
4. 애플리케이션이 변환된 데이터를 수신함.

### Use Case

* **이미지 처리**  
이미지를 요청할 때 동적으로 리사이징하거나 필터를 적용.
* **데이터 마스킹**  
민감한 데이터를 마스킹하거나 제거하여 반환.
* **형식 변환**  
데이터를 JSON에서 XML로 변환하거나, CSV에서 JSON으로 변환.