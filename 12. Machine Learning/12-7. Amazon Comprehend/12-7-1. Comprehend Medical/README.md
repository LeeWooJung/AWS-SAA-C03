# [Comprehend Medical](https://docs.aws.amazon.com/ko_kr/comprehend-medical/latest/dev/comprehendmedical-welcome.html)

## <img src = "https://github.com/user-attachments/assets/12c32a51-fee6-4d98-860f-7131941eaac9" width = "25" height = "25"> Amazon Comprehend Medical

Amazon Comprehend Medical은 **Unstructured한 의료 데이터를 분석하고 자연어 처리(NLP)를 통해 중요한 정보를 추출하는 머신 러닝 서비스**임. 

Unstructured Clinical data는 Physician's notes, Discharge summaries, Test results, Case notes 등이 될 수 있음.

이를 통해 **의료 텍스트에서 임상적 개념, 약물, 질병 및 증상, 치료법, 검사 결과 등을 자동으로 식별하고 구조화**할 수 있음.

NLP를 사용하여 **Protected Health Information**(PHI)를 식별함.

Amazon S3에 저장된 Document, Kinesis Data Firehose를 이용한 real-time data, Amazon Transcribe를 사용하여 환자의 말을 텍스트로 변환한 데이터 등이 **Amazon Comprehend Medical**에 의해 분석될 수 있음.

## 특징

### 엔티티 인식

의료 텍스트에서 **질병, 증상, 약물, 치료법, 검사 결과 등의 임상적 엔티티를 식별**할 수 있음.

### 관계 추출

텍스트 내에서 **엔티티 간의 관계를 추출**할 수 있음. 

예를 들어, 특정 약물과 관련된 부작용 등을 식별할 수 있음.

### 필드 추출

의료 문서에서 **특정 필드를 추출하고 구조화**할 수 있음.

### PHI(Protected Health Information) 추출

텍스트에서 **보호되는 건강 정보를 식별하고 관리**할 수 있음.

### ICD-10-CM 코딩

질병 및 건강 상태를 ICD-10-CM 코드로 매핑할 수 있음.

## 구성 요소

* **API**

    텍스트 분석을 위한 **RESTful API**를 제공함.

* **콘솔**

    Amazon Comprehend Medical의 기능을 테스트하고 설정할 수 있는 관리 콘솔을 제공함.

* **SDK**

    다양한 프로그래밍 언어에서 사용할 수 있는 SDK를 제공함.

## 아키텍처

### 입력 데이터

분석할 의료 텍스트 데이터를 제공함.

### Amazon Comprehend Medical

**텍스트 데이터를 분석하여 임상적 엔티티, 관계, PHI 등을 추출**함.

### 출력 데이터

분석 결과를 반환하여 추가 처리나 시각화를 위해 사용함.


## 장점

* **정확성**

    머신 러닝 모델을 통해 높은 정확도의 텍스트 분석을 제공함.

* **자동화**

    의료 데이터 분석을 자동화하여 **시간과 비용을 절감**할 수 있음.

* **확장성**

    AWS 인프라를 활용하여 대규모 데이터도 빠르게 처리할 수 있음.

* **보안**

    의료 데이터의 보안 및 규정 준수를 위한 다양한 기능을 제공함.

## 단점

* **커스터마이징 제한**

    사전 정의된 모델을 사용하기 때문에 사용자 맞춤형 모델을 만들기 어려움.

* **비용**

    대규모 데이터 분석 시 비용이 많이 발생할 수 있음.

* **의존성**

    AWS 서비스에 의존하게 됨.

## Use case

* **임상 기록 분석**

    환자의 임상 기록에서 중요한 정보를 추출하고 구조화함.

* **의료 문서 관리**

    의료 문서를 자동으로 분류하고 필드를 추출하여 관리함.

* **PHI 관리**

    보호되는 건강 정보를 식별하고 관리하여 규정 준수를 지원함.

* **임상 연구**

    임상 연구 데이터를 분석하여 주요 인사이트를 도출함.

* **ICD-10-CM 코딩**

    질병 및 건강 상태를 ICD-10-CM 코드로 자동 매핑함.

## Summary

Amazon Comprehend Medical은 의료 텍스트 데이터를 분석하고 **임상적 엔티티, 관계, PHI 등을 추출하는 머신 러닝 서비스**임.

이를 통해 의료 데이터의 분석을 자동화하고, 시간과 비용을 절감하며, 데이터의 정확성과 보안을 보장할 수 있음. 

그러나 커스터마이징 제한, 비용, AWS 의존성 등의 단점이 있으며, **임상 기록 분석, 의료 문서 관리, PHI 관리, 임상 연구, ICD-10-CM 코딩 등의 다양한 사용 사례에 활용**할 수 있음.