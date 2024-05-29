# [Aurora Machine Learning](https://aws.amazon.com/ko/rds/aurora/machine-learning/)

## Aurora Machine Learning

* **Amazon Aurora Machine Learning**(Aurora ML)은 데이터베이스 관리 시스템인 Amazon Aurora에 기계 학습 기능을 통합하여 **사용자가 SQL 쿼리로 직접 기계 학습 모델을 호출하고 사용할 수 있게 하는 기능**.  
* Aurora ML을 통해 데이터베이스에 저장된 데이터를 기반으로 예측 분석 및 기계 학습 작업을 수행할 수 있음.

## 특징

1. **직접적인 SQL 통합**

    * 사용자는 SQL 쿼리를 통해 Amazon SageMaker와 AWS Comprehend의 기계 학습 모델을 호출할 수 있음.
    * 복잡한 데이터 이동 과정 없이 데이터베이스 내에서 바로 예측 분석을 수행할 수 있음.

2. **간편한 설정**

    * 기계 학습 모델을 설정하고 배포하는 과정을 Aurora 내에서 직접 처리할 수 있어, 기존의 데이터베이스 관리 방식에 쉽게 통합됨.
    * AWS Management Console이나 CLI를 통해 간단히 설정할 수 있음.

3. **실시간 예측 분석**

    * 실시간으로 데이터베이스 트랜잭션과 연동하여 예측 분석을 수행할 수 있음.
    * 예를 들어, 사용자가 온라인 쇼핑몰에서 상품을 조회할 때 실시간으로 추천 상품을 보여주는 기능 등을 구현할 수 있음.

## 작동 원리

* **Amazon SageMaker**  
    * 기계 학습 모델을 구축, 훈련 및 배포하는데 사용됨.
    * Aurora는 **SageMaker**에서 배포된 모델을 호출하여 예측 결과를 가져옴.

* **AWS Comprehend**  
    * 텍스트 분석 서비스로, 텍스트에서 감정, 엔터티, 키워드 등을 추출할 수 있음.
    * Aurora는 Comprehend를 호출하여 텍스트 데이터를 분석할 수 있음.

## Use Case

* **제품 추천 시스템**  
    * 사용자 행동 데이터를 기반으로 제품을 추천하는 기계 학습 모델을 SageMaker에서 훈련하고 Aurora에 통합.
    * 사용자가 특정 제품을 조회할 때, SQL 쿼리를 통해 해당 사용자에게 추천할 제품을 실시간으로 분석하여 제공.

* **사기 탐지 시스템**  
    * 거래 데이터에서 이상 징후를 탐지하는 모델을 SageMaker에서 훈련.
    * Aurora를 통해 실시간 거래 데이터에 대해 모델을 호출하여 사기 가능성을 평가.

* **고객 감정 분석**  
    * 고객 피드백 텍스트를 AWS Comprehend로 분석하여 감정을 추출.
    * SQL 쿼리를 통해 피드백 텍스트를 분석하고, 감정 점수를 데이터베이스에 저장하여 고객 만족도를 모니터링함.

## Conclusion

* **Amazon Aurora Machine Learning**은 데이터베이스와 기계 학습을 통합하여 실시간 예측 분석을 가능하게 함.  
* SageMaker와 Comprehend를 통해 강력한 기계 학습 기능을 데이터베이스 내에서 직접 사용할 수 있으며, 이를 통해 더욱 효율적이고 실시간적인 분석 및 예측 작업을 수행할 수 있음.  
* Aurora ML의 사용은 데이터 이동을 줄이고, 데이터 기반 의사결정을 더욱 빠르고 정확하게 할 수 있게 해줌.

## Architecture

![machine learning architecture](https://github.com/LeeWooJung/AWS-SAA-C03/assets/31682438/313c9f9d-547d-478d-8c54-ecdca35180c3)
