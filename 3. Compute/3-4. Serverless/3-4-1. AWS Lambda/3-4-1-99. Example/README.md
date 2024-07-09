# Example

## with [RDS Proxy](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-1.%20Amazon%20RDS/7-1-6.%20RDS%20Proxy)

Lambda function이 Database와 연결되면, 수 많은 Lambda Function이 생성됐을 때를 대비해야 함.

이런 high load 상황을 해결하기 위해 **RDS Proxy와 Database를 연결**하고, **Lambda function과 RDS Proxy를 연결**해야 함.

하지만, RDS Proxy는 public subnet에 존재하지 않고, **Publicly accessible 하지 않음**. 따라서, Lambda function은 VPC와 연결되어 VPC 내부에서 실행되어야 함.

## Invoking Lambda from RDS & Aurora