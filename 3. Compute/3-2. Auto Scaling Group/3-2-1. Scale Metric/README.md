# ASG Scale Metric

**AWS Auto Scaling Group** (ASG)에서 사용하기 좋은 스케일 메트릭은 애플리케이션의 성능과 가용성을 유지하기 위해 중요함.

## CPU Utilization

* ASG는 CPU 사용률을 모니터링하여 인스턴스의 부하를 확인함.  
CPU 사용률이 높으면 추가 인스턴스를 시작하고, 사용률이 낮으면 인스턴스를 종료.
* EX)  CPUUtilization 메트릭이 70%를 초과하면 인스턴스를 추가하고, 30% 미만이면 인스턴스를 줄이는 정책을 설정할 수 있음.

```json
{
    "MetricName": "CPUUtilization",
    "Namespace": "AWS/EC2",
    "Statistic": "Average",
    "ComparisonOperator": "GreaterThanThreshold",
    "Threshold": 70,
    "Period": 60,
    "EvaluationPeriods": 2,
    "ScalingAdjustment": 1,
    "AdjustmentType": "ChangeInCapacity"
}
```

## Network In/Out

* 네트워크 트래픽을 기반으로 스케일링 결정을 내림.  
대규모 데이터 전송 작업이 있을 경우 네트워크 입출력 메트릭을 사용하면 유용.

* EX) NetworkIn 메트릭이 일정 수준 이상이면 인스턴스를 추가하여 트래픽을 분산.

```json
{
    "MetricName": "NetworkIn",
    "Namespace": "AWS/EC2",
    "Statistic": "Average",
    "ComparisonOperator": "GreaterThanThreshold",
    "Threshold": 50000000,
    "Period": 60,
    "EvaluationPeriods": 2,
    "ScalingAdjustment": 1,
    "AdjustmentType": "ChangeInCapacity"
}
```

## Request Count Per Target

* **Application Load Balancer**(ALB)를 사용할 때, 각 대상에 대한 요청 수를 기준으로 스케일링 결정을 내림.  
웹 애플리케이션에서 유용.
* EX) 대상 그룹의 요청 수가 증가하면 인스턴스를 추가하여 처리 능력을 확장.

```json
{
    "MetricName": "RequestCountPerTarget",
    "Namespace": "AWS/ApplicationELB",
    "Statistic": "Sum",
    "ComparisonOperator": "GreaterThanThreshold",
    "Threshold": 1000,
    "Period": 60,
    "EvaluationPeriods": 2,
    "ScalingAdjustment": 1,
    "AdjustmentType": "ChangeInCapacity"
}
```

## Memory Utilization (Custom Metric)
* 기본적으로 제공되지 않지만, **CloudWatch**를 사용하여 메모리 사용률을 모니터링하고 스케일링에 사용할 수 있음.
* EX) 메모리 사용률이 80%를 초과하면 인스턴스를 추가하고, 40% 미만이면 인스턴스를 줄이는 정책을 설정할 수 있음.

```json
{
    "MetricName": "MemoryUtilization",
    "Namespace": "CustomNamespace",
    "Statistic": "Average",
    "ComparisonOperator": "GreaterThanThreshold",
    "Threshold": 80,
    "Period": 60,
    "EvaluationPeriods": 2,
    "ScalingAdjustment": 1,
    "AdjustmentType": "ChangeInCapacity"
}
```