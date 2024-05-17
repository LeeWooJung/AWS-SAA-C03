# [EFS](https://docs.aws.amazon.com/ko_kr/efs/latest/ug/whatisefs.html)

## <img src = "https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/f8e192fb-d31d-45de-913d-2d8f82c83d16" width = "20" height = "20"> EFS

## [EFS Performance](https://docs.aws.amazon.com/efs/latest/ug/performance.html)

1. **EFS Scale**  
EFS는 페타바이트 규모의 스토리지 볼륨으로 확장 가능하며, 세 가지 처리량 모드를 제공함.

2. **Performance Mode**  
Amazon EFS는 **General Purpose**와 **Max I/O** 두 가지 성능 모드를 제공함.  
    - **General Purpose 모드**  
작업당 지연 시간이 가장 낮으며, 파일 시스템의 기본 성능 모드임.  
    - **Max I/O 모드**  
범용 모드보다 긴 지연 시간을 견딜 수 있는 고도로 병렬화된 워크로드용으로 설계되었음.  
더 빠른 성능을 위해 항상 범용 성능 모드를 사용하는 것이 좋음.

3. **Throughput Mode**  
파일 시스템의 처리량 모드에 따라 파일 시스템에서 사용할 수 있는 처리량이 결정됨.  

    - **Bursting**  
Amazon EFS의 처리량은 파일 시스템이 성장함에 따라 확장됨.  
    - **Elastic**  
파일 시스템의 크기나 burst credit balance에 상관없이 지정된 처리량 수준에 따라 EFS 파일 시스템이 처리량을 제공함. 이 모드는 파일을 추가하고 제거함에 따라 **자동으로 확장되고 축소**되므로, 애플리케이션에서는 필요할 때 필요한 만큼 스토리지를 확보할 수 있음.  
이 모드는 자주 액세스하지 않는 데이터에 대해 최대 90,000 읽기, 자주 액세스하는 데이터에 대해 최대 250,000 읽기 IOPS를 처리할 수 있음. 이렇게 Elastic 처리량 모드는 파일 시스템의 크기와 상관없이 일관된 성능을 얻을 수 있음
    - **Provisioned**  
파일 시스템의 크기나 burst credit balance에 상관없이 지정된 처리량 수준에 따라 EFS 파일 시스템이 처리량을 제공함.  
이 모드는 처리량이 많을 경우에 권장되며, 사용자가 필요한 처리량을 미리 프로비저닝하고, 이에 따라 비용을 지불하게 됨.

이렇게 AWS EFS의 성능은 EFS Scale, Performance Mode, 그리고 Throughput Mode에 따라 달라짐.  
이 세 가지 요소를 적절히 조합하면, 워크로드의 요구 사항에 맞는 최적의 성능을 얻을 수 있음.