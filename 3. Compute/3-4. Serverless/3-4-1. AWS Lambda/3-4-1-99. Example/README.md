# Example

## with [RDS Proxy](https://github.com/LeeWooJung/AWS-SAA-C03/tree/main/7.%20Database/7-1.%20Amazon%20RDS/7-1-6.%20RDS%20Proxy)

Lambda function이 Database와 연결되면, 수 많은 Lambda Function이 생성됐을 때를 대비해야 함.

이런 high load 상황을 해결하기 위해 **RDS Proxy와 Database를 연결**하고, **Lambda function과 RDS Proxy를 연결**해야 함.

하지만, RDS Proxy는 public subnet에 존재하지 않고, **Publicly accessible 하지 않음**. 따라서, Lambda function은 VPC와 연결되어 VPC 내부에서 실행되어야 함.

### Architecture Example

![Rdx proxy architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/15f80a1f-1b90-40c8-990a-c66bafd83d84)


## Invoking Lambda from RDS & Aurora

DB 인스턴스에서 Lambda function을 호출할 수 있음. 이를 위해서는 DB에서 **data events 트리거를 설정**하여 Lambda 함수를 호출해야 함.

DB 인스턴스에서 Labmda function으로의 **Outbound traffic**을 허용해야 함.

또한, DB 인스턴스는 Lambda function을 트리거 하기 위해 **Lambda Resource-based Policy** 와 **IAM Policy**와 같은 필수 권한을 갖고 있어야 함.

### Architecture Example

![DB Instance architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/d7967746-c14b-4bb7-b4d7-c621a4d5434f)

## RDS Event Notifications

DB 인스턴스 자체에 대한 Event 알림(Created, Stopped, start, ...)을 호출할 수 있음. 데이터 자체에 대한 정보가 없어도 알림을 받을 수 있음.

이를 위해 다음과 같은 Event Category 에 대해 구독해야 함.  
* DB instance  
* DB snapshot  
* DB parameter Group  
* DB Security Group  
* RDS Proxy  
* Custom Engine Version

거의 실시간 이벤트(5분 이내)를 받을 수 있으며, SNS를 통해 알림을 보내거나 EventBridge를 구독하여 알림이나 메시지, 명령을 보낼 수 있음.

### Architecture Example

![RDS Event Notification architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/82b7cf23-8b7d-42b4-9bd0-050dae7f6f6d)
