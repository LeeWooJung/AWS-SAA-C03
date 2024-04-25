# [Security Group](https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-security-groups.html)

## Security Group

* **보안 그룹(Security Group)**: 가상의 방화벽으로, AWS에서 인스턴스에 대한 인바운드(Inbound)와 아웃바운드(Outbound) 네트워크 트래픽을 제어하는 역할을 함.  
각 인스턴스에는 최대 5개의 보안 그룹을 할당할 수 있으며, 이를 통해 특정 포트와 프로토콜에 대한 액세스를 허용하거나 거부 가능.

## 보안 그룹 특징

* **인바운드 규칙(Inbound Rule)**: 외부에서 인스턴스로 들어오는 트래픽을 제어. 기본적으로 모든 인바운드 트래픽은 **차단**되어 있음.
* **아웃바운드 규칙(Outbound Rule)**: 인스턴스에서 외부로 나가는 트래픽을 제어. 기본적으로 모든 아웃바운드 트래픽은 **허용**되어 있음.
* **상태 저장(Stateful)**: 인바운드 규칙을 통과한 트래픽은 아웃바운드 규칙의 영향을 받지 않고, 반대로 아웃바운드 규칙을 통과한 트래픽도 인바운드 규칙의 영향을 받지 않음.
* **적용**: EC2 인스턴스뿐만 아니라 RDS, ELB, VPC Interface Endpoint 등 VPC 내에서 Elastic Network Interface (ENI)를 갖는 모든 서비스에 적용될 수 있음.

## 보안 그룹 설정

* **Type**: 서비스 타입(HTTP, SSH 등)을 지정.
* **Protocol**: 사용할 프로토콜(TCP, UDP 등)을 지정.
* **Port Range**: 허용할 포트 범위를 지정.
* **Source**: 허용할 IP 주소 또는 다른 보안 그룹을 지정.

## Diagram

![diagram](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/71c154b1-819a-42b8-ad5b-2218de43d327)

* Inbound Rule: HTTP, TCP, 80, 0.0.0.0/0(Any)
* Outbound Rule: Any(Default)

1) Users가 SSH를 사용하여 EC2 Instances에 접근하려 하더라도 보안 그룹에서 Inbound를 허용하지 않기 때문에 접근할 수 없음.
2) Desktop에서 HTTP/TCP를 통해 EC2 Instances에 접근하려 하면 해당 보안 그룹의 Inbound에 속하므로 접근할 수 있음.
3) Outbound는 모든 트래픽을 허용하는 것이 Default이므로 Desktop으로 Outbound 허용됨.
4) 혹은, **Stateful** 특성 덕분에 Inbound가 허용된 Desktop에 Outbound도 허용.