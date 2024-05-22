# [Hibernate](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/hibernating-instances.html#:~:text=To%20hibernate%20an%20instance%20Open%20the%20Amazon%20EC2,hibernated%20or%20stopped%2C%20or%20it%20can%27t%20be%20hibernated.)

## Hibernate

Hibernate는 [EC2 인스턴스](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/3.%20EC2)의 현재 상태를 일시 중지하고 나중에 다시 시작할 수 있는 기능.  
Hibernate를 사용하면 인스턴스의 메모리(RAM) 내용이 Amazon Elastic Block Store(**EBS**) 루트 볼륨에 저장됨.  
이는 인스턴스를 중지하고 나중에 정확히 **같은** 상태에서 다시 시작할 수 있음을 의미.

## Process

1) Hibernate를 사용하면 인스턴스가 중지 상태로 이동하고, Amazon EC2는 운영 체제에게 Hibernate(디스크로의 일시 중지)를 수행하도록 신호를 보냄.  
2) Hibernate는 모든 프로세스를 동결하고, RAM의 내용을 EBS 루트 볼륨에 저장한 후 일반적인 종료를 수행.
3) 종료가 완료되면 인스턴스는 중지 상태로 변함. EBS 볼륨은 인스턴스에 연결된 상태로 유지되며, 그들의 데이터는 유지됨.
4) 인스턴스가 시작되면, 인스턴스는 부팅되고 운영 체제는 EBS 루트 볼륨에서 RAM의 내용을 읽은 후 프로세스를 해제하여 상태를 재개.  
인스턴스는 개인 IPv4 주소와 IPv6 주소를 유지함. 인스턴스가 시작되면, Amazon EC2는 인스턴스에 새로운 공용 IPv4 주소를 할당함.

## Architecture
![Hibernate](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/1785bb34-bcfe-4188-a365-093fdc3977c3)


## Stop vs. Hibernate

* **Stop**  
인스턴스를 중지하면 메모리(RAM)에 저장된 데이터가 손실됨.  
중지 상태에서는 인스턴스가 실행되지 않으므로, 인스턴스 사용료나 데이터 전송료는 청구되지 않지만, Amazon EBS 볼륨에 대한 저장 공간은 계속 청구됨.

* **Hibernate**  
인스턴스를 Hibernate 상태로 전환하면, AWS는 운영 체제에게 Hibernate(디스크로의 일시 중지)를 수행하도록 신호를 보냄.  
이는 인스턴스 메모리(RAM)의 내용을 Amazon EBS 루트 볼륨에 저장함.  
따라서, Hibernate 상태에서 인스턴스를 다시 시작하면, 이전에 실행 중이던 프로세스 정보를 빠르게 다시 불러올 수 있음.  
Hibernate 상태에서는 인스턴스가 중지되어 있지만, 메모리 상태가 유지되므로, 인스턴스 사용료나 데이터 전송료는 청구되지 않지만, EBS 루트 볼륨에 대한 저장 공간은 계속 청구됨.

* **주요 차이점**  
Stop과 Hibernate의 주요 차이점은 메모리(RAM)에 저장된 데이터의 처리 방식임.  
Stop 상태에서는 메모리 데이터가 손실되지만, Hibernate 상태에서는 메모리 데이터가 보존되어 인스턴스를 빠르게 재개할 수 있음.