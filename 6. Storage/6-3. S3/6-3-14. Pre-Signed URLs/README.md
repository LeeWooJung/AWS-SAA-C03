# [S3 Pre-Signed URLs](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/PresignedUrlUploadObject.html)

## S3 Pre-Signed URLs

* Pre-Signed URLs는 **임시적으로 S3 버킷의 객체에 접근할 수 있도록 생성된 URL**.  
* 이 URL을 통해 **제한된 시간 동안 비공개 S3 객체에 대한 접근을 허용**할 수 있음.

* **Pre-Signed URL**  
제한된 시간 동안 특정 S3 객체에 접근할 수 있는 서명된 URL.
* **생성자**  
Pre-Signed URL을 생성한 IAM 사용자 또는 역할.
* **만료 시간**  
  * URL이 유효한 시간.
  * **S3 Console**: 1분 ~ 720분
  * **AWS CLI**: default(3600s), 최대 168시간.

### 기능

* **액세스 제어**  
Pre-Signed URLs를 사용하여 **지정된 기간 동안만 객체에 대한 읽기 또는 쓰기 권한**을 부여할 수 있음.
* **임시 공유**  
Pre-Signed URL을 통해 비공개 객체를 **외부 사용자와 임시로 공유**할 수 있음.
* **API 호출**  
S3에 직접 접근하지 않고도 안전하게 객체를 업로드하거나 다운로드할 수 있음.

### 특징

* **보안**  
Pre-Signed URL은 지정된 시간 동안만 유효하므로 보안 위험을 줄일 수 있음.
* **유연성**  
읽기, 쓰기 등 다양한 액세스 권한을 설정할 수 있음.
* **쉽고 빠름**  
URL을 생성하고 배포하는 과정이 간단하며, 사용자 친화적임.

### 장점

* **보안 제어**  
접근 권한을 시간 제한과 함께 제공할 수 있음.
* **비용 절감**  
불필요한 퍼블릭 액세스를 방지하여 비용 절감 가능.
* **사용자 경험**  
사용자가 직접 S3 버킷에 접근하지 않고도 파일을 업로드하거나 다운로드할 수 있음.

### 단점

* **유효 기간**  
유효 기간이 지나면 URL이 만료되어 다시 생성해야 함.
* **보안 위험**  
URL이 유출되면 지정된 기간 동안 누구나 접근할 수 있음.

### Pre-Signed URL 생성

* **AWS SDK(Python)**  
  ```python
  import boto3
  from botocore.exceptions import NoCredentialsError

  s3_client = boto3.client('s3')

  def create_presigned_url(bucket_name, object_name, expiration=3600):
    try:
        response = s3_client.generate_presigned_url('get_object',
                                                    Params={'Bucket': bucket_name, 'Key': object_name},
                                                    ExpiresIn=expiration)
    except NoCredentialsError:
        print("Credentials not available")
        return None
    return response

  url = create_presigned_url('my-bucket', 'my-object')
  print(url)
  ```

  * **bucket_name**: 객체가 저장된 S3 버킷 이름.
  * **object_name**: 접근할 S3 객체의 키.
  * **expiration**: URL 유효 기간(초).

* **AWS CLI**  
  ```sh
  aws s3 presign s3://my-bucket/my-object --expires-in 3600
  ```
  * **my-bucket**: S3 버킷 이름.
  * **my-object**: 접근할 객체의 키.
  * **--expires-in**: URL의 유효 기간(초).

## Architecture Example

* **파일 공유 시스템**  
  * 사용자 A가 비공개 파일을 공유하려면 Pre-Signed URL을 생성.
  * URL을 사용자 B에게 제공.
  * 사용자 B는 URL을 사용하여 파일을 다운로드.

* **클라이언트 업로드 시스템**  
  * 클라이언트가 파일을 업로드하려면 서버에서 Pre-Signed URL을 생성하여 클라이언트에게 제공.
  * 클라이언트는 URL을 사용하여 S3 버킷에 파일 업로드.

## Summary

* Pre-Signed URLs는 S3 객체에 대한 임시 액세스를 안전하게 제공하는 유용한 도구임.  
* 이를 통해 보안성과 유연성을 높일 수 있으며, 다양한 사용 사례에 적용할 수 있음.  
* 하지만 URL의 유출 및 만료 시간 관리 등 보안 측면에서 주의가 필요함.
