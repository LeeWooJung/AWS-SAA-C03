# Disaster Recovery & Migrations

Disaster Recovery & Migrations와 관련된 AWS Services에 대해 설명합니다.


## Pilot Light

Cloud에서 small version의 Application이 항상 돌아가는 상태.

Pilot Light는 Critical Core에 유용함.

Backup & Restore와 매우 유사하지만, 이보다 빠르게 Disaster Recover가 가능함.

## Warm Standby

최소한의 크기로 전체 system이 돌아가는 상태.

Disaster가 발생하자마자 Production load를 시작함.

## Multi Site

RTO 시간이 매우 짧고 비용이 많이 듦.

전체 Production Scale이 AWS와 On-Premise에서 작동하고 있음.

## Disaster Recovery

### Backup

* EBS Snapshot, RDS automated backups, Snapshot 등을 활용.
* 평상시에 S3, S3 IA, S3 Glacier로 Lifecycle policy를 이용하여 데이터를 전송하고, Cross Region Replication을 이용하여 다른 Region에 데이터를 복사해놓음.
* On-Premise에서는 Snowball 또는 Storage Gateway를 이용하여 AWS로 데이터를 백업.

### High Availability

* Route53을 이용하여 DNS Fail에 대한 대첵을 마련해둠.
* RDS Multi-AZ, ElastiCache Multi-AZ, EFS, S3를 활용.
* Direct Connect의 Failure를 대비하여 Site-to-Site VPN을 연결해 놓음.

### Replication

* Cross Region이 가능한 RDS Replication을 진행함. 또한, AWS Aurora와 Global Databases를 이용하여 데이터를 미리 복제해놓음.
* On-premise에 있는 데이터를 RDS로 미리 복제해놓음.
* Storage Gateway를 활용.

### Automation

* CloudFormation, Elastic Beanstalk를 이용하여 새로운 환경을 즉시 재생성.
* CloudWatch에서 Fail Alarm이 생겼을 경우, EC2 Instance를 자동으로 Recover 또는 Reboot
* AWS Lambda function을 이용하여 미리 자동화 해놓음.
