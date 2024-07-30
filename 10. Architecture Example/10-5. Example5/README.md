# Example 5

VPC 내부에서 AWS Public Service에 접근하기 위한 방법.

![Lambda in VPC accessing DynamoDB Architecture](https://github.com/user-attachments/assets/dc70a516-05e0-4e7f-98d8-ad963863b6c4)


DynamoDB는 AWS의 **Public Service**임.

VPC 내부에 존재하는 Lambda가 DynamoDB에 접근하기 위한 방법은 두 가지가 존재함.

## Access From the Public Internet

Public Internet을 이용하여 DynamoDB에 접근하기 위해서 필요한 것은 다음과 같음.

* **NAT Gateway**
* **Internet Gateway**

## Access From the Private VPC Network

Private VPC Network를 이용하려면 **VPC Gateway Endpoint**를 생성해야함.

또한, VPC Gateway Endpoint와 Lambda(Private Subnet)의 **Route Table**을 수정해주어야함.

해당 방법은 비용이 **무료**이며, 더 빠르게 Amazon DynamoDB에 접근하는 방법임.