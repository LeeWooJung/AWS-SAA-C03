# With EFS

Amazon ECS (Elastic Container Service)는 컨테이너화된 애플리케이션을 관리하고 배포하는 서비스임.  

[Amazon EFS](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/6.%20Storage/6-2.%20EFS) (Elastic File System)는 **AWS 클라우드 내에서 공유 파일 시스템을 제공하는 서비스**임.  

ECS와 EFS를 함께 사용하면 **컨테이너 간에 데이터를 공유하거나 영구 스토리지가 필요한 애플리케이션을 실행**할 수 있음.

EFS는 **여러 EC2 인스턴스에서 동시에 접근할 수 있는 네트워크 파일 시스템을 제공**하여, **ECS 태스크 및 서비스가 동일한 데이터를 공유**할 수 있게 함.  

이를 통해 **상태 유지가 필요한 애플리케이션이나 데이터 처리가 요구되는 애플리케이션에 적합**함.  

**EC2 launch type과 Fargate launch type 모두**에서 작동함.

**Fargate**와 **EFS**를 연결하면 Serverless 를 구현할 수 있음.  

**Amazon S3는 File System으로 mount될 수 없음**.

## Connect to EFS

### EFS 파일 시스템 생성

* AWS Management Console에서 EFS를 생성하고 파일 시스템 ID를 얻음.
* 필요한 경우 보안 그룹을 설정하여 접근을 제어함.

### ECS 태스크 정의에 EFS 볼륨 추가

* ECS 태스크 정의에서 **EFS 볼륨을 추가**함.
* EFS 파일 시스템 ID를 지정하고 필요한 경로와 권한을 설정함.
* **mountPoints와 volumes 섹션을 사용하여 EFS 볼륨을 컨테이너에 마운트**함.

### ECS 서비스 또는 태스크 실행

* EFS 볼륨이 포함된 태스크 정의를 사용하여 **ECS 서비스를 생성하거나 태스크를 실행**함.
* 컨테이너가 실행될 때 EFS 파일 시스템이 지정된 경로에 마운트됨.

## ECS Task 정의에서 EFS 볼륨 추가

``` json
{
    "family": "my-task",
    "containerDefinitions": [
        {
            "name": "my-container",
            "image": "my-image",
            "mountPoints": [
                {
                    "sourceVolume": "my-efs-volume",
                    "containerPath": "/mnt/efs"
                }
            ]
        }
    ],
    "volumes": [
        {
            "name": "my-efs-volume",
            "efsVolumeConfiguration": {
                "fileSystemId": "fs-12345678",
                "rootDirectory": "/",
                "transitEncryption": "ENABLED"
            }
        }
    ]
}
```

## 보안 설정

EFS와 ECS 간의 연결 시 **보안 그룹과 IAM 역할을 설정**하여 데이터 접근을 제어함.  

EFS의 보안 그룹은 ECS 인스턴스의 보안 그룹과 통신할 수 있도록 구성해야 함.  

또한, **ECS 태스크 정의에서 사용할 IAM 역할에는 EFS 파일 시스템에 접근할 수 있는 권한이 필요**함.

## EFS와 ECS의 연결 아키텍처

* **ECS 클러스터**  
여러 ECS 인스턴스 및 Fargate 태스크를 포함.

* **EFS 파일 시스템**  
여러 AZ(가용 영역)에 걸쳐 분산된 네트워크 파일 시스템.

* **ECS 태스크**  
EFS 파일 시스템을 마운트하여 데이터 공유 및 영구 저장소로 사용.

## 장점

* **데이터 공유**  
여러 컨테이너 간에 동일한 데이터를 공유할 수 있음.

* **영구 스토리지**  
컨테이너가 중단되거나 재시작되더라도 데이터가 유지됨.

* **확장성**  
EFS는 자동으로 확장되며, 고성능을 제공함.

## 단점

* **비용**  
EFS 사용량에 따라 비용이 발생함.

* **네트워크 지연**  
EFS는 네트워크를 통해 접근하므로 로컬 스토리지보다 지연이 있을 수 있음.

## Summary
Amazon ECS와 EFS를 통합하면 **컨테이너화된 애플리케이션에서 영구적이고 공유 가능한 스토리지**를 사용할 수 있음.  

이를 통해 상태 유지가 필요한 애플리케이션이나 데이터 처리 애플리케이션을 효과적으로 배포할 수 있음.  

ECS 태스크 정의에서 EFS 볼륨을 추가하고 보안 설정을 통해 안전하게 데이터에 접근할 수 있음.