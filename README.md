# hybird_predict_model

## 프로젝트 목적
이 프로젝트는 홈쇼핑사의 편성 최적화 및 시청률 상승 전략 수립을 지원하기 위한 데이터 기반 AI 모델입니다. 
카테고리 특성과 시청 패턴을 정밀하게 반영하여, 시청자 예측을 구현합니다.

# 홈쇼핑 시청자 수 예측 모델링

본 프로젝트는 홈쇼핑 방송 데이터와 제품 카테고리를 활용하여 **시청자 수를 예측**하는 머신러닝 기반 모델링 시스템입니다. 각 카테고리를 그룹화하여 그룹별 맞춤 모델을 학습하고, 전체 데이터를 대상으로 한 통합 모델도 함께 구축합니다.

---

## 프로젝트 주요 특징

- **그룹별 모델 학습**: `상품별 카테고리`을 기준으로 Group A ~ J로 분류 후, 각 그룹에 특화된 모델 학습
- **데이터 증강 적용**: 데이터가 부족한 특정 그룹(`Group_B`, `Group_C`, `Group_D`, `Group_J`)에 대해 KMeans 기반 샘플링과 노이즈 추가 방식으로 증강
- **Optuna 하이퍼파라미터 튜닝**: XGBoost 모델에 대해 각 그룹별로 Optuna를 활용한 자동 최적화
- **모델 및 인코더 저장**: 학습된 모델과 인코더를 `.pkl`로 저장하여 재사용 가능

---

## 실행 방법

1. 필요 라이브러리 설치:
   ```bash
   pip install optuna
   pip install -U xgboost
   pip install optuna-integration[xgboost]


## 구글 들아ㅣ브 마운트 및 경로 설정

from google.colab import drive
drive.mount('/content/drive')

file_path = '데이터 경로'
model_dir = '모델 저장 경로'

## 모델 저장 구조

model_total.pkl: 전체 데이터로 학습된 통합 모델

model_Group_*.pkl: 그룹별로 학습된 맞춤형 모델

encoder_total_model.pkl: 범주형 변수 인코더

feature_list.txt: 학습에 사용된 feature 목록

## 주의사항

Group은 통합카테고리1 기준으로 수동 매핑되며, 존재하지 않는 카테고리는 Group_G으로 분류됨

모델 예측 시에는 동일한 인코더(encoder_total_model.pkl)로 인코딩 필수

각 그룹은 독립적으로 튜닝 및 학습되며, 예측 시 그룹명을 기준으로 모델 선택
