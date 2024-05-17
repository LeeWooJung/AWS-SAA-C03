# [EFS](https://docs.aws.amazon.com/ko_kr/efs/latest/ug/whatisefs.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/f8e192fb-d31d-45de-913d-2d8f82c83d16" width = "20" height = "20"> EFS

### [EFS Storage Class](https://docs.aws.amazon.com/efs/latest/ug/availability-durability.html#:~:text=EFS%20storage%20classes%201%20Optimizing%20storage%20costs%20The,each%20storage%20class.%204%20Viewing%20storage%20class%20size)

AWS EFS(Elastic File System)의 Storage Class는 워크로드의 성능, 데이터 액세스, 복원력 및 비용 요구 사항에 따라 선택할 수 있는 다양한 스토리지 클래스를 제공함.

1. **Standard Class**  
자주 액세스하는 파일을 저장하는데 사용하는 클래스임. 이 클래스는 높은 내구성, 가용성 및 성능을 갖춘 객체 스토리지를 제공함.
2. **Infrequent Access (IA) Class**  
저장기간이 길지만 자주 액세스하지 않는 파일을 저장하기 위한 클래스임. 이 클래스는 비용 효율적인 스토리지를 제공하며, 감사 요구 사항을 충족시키거나 역사적 분석을 수행하거나 백업을 수행하거나 재해 복구 파일을 저장하는 데 사용될 수 있음.
3. **One Zone Class**  
이 클래스는 단일 가용 영역(AZ) 내에서 데이터를 중복 저장하며, Multi-AZ 복원력이 필요하지 않은 작업에 대해 비용을 최적화함.

이러한 스토리지 클래스들은 각각의 특정 액세스 패턴에 대해 가장 저렴한 스토리지를 제공하기 위해 특별히 구축되었음.  
이들은 까다로운 성능 요구 사항, 데이터 레이크, 레지던시 요구 사항, 알 수 없거나 변경되는 액세스 패턴 또는 자주 액세스하지 않는 파일 등을 포함하여 거의 모든 사용 사례에 적함함.