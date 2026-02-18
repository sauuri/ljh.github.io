# Metallic Glass vs Non-Metallic Glass 분류 (대학교 프로젝트)

금속 유리(Metallic Glass)와 비금속 유리(Non-Metallic Glass)를 구별하는 이진 분류 문제이며,  
**Feature Selection(특성 선택)** 관점에서 “성능을 최대한 유지하면서 입력 특성을 어디까지 줄일 수 있는가?”를 실험한 프로젝트입니다.

## 문제 정의
- 입력: 시료의 수치형 특성(총 **196개 feature**)
- 출력: MG / NMG (binary classification)

## 실험 목표
- 196개 feature를 그대로 쓸 때 대비,
- **feature importance 기반으로 중요도가 낮은 특성부터 제거**하면서
- **성능을 크게 해치지 않는 최소 feature subset**을 찾기

## 접근 방법 (요약)
1. 데이터 전처리  
   - [결측치 처리 방식: 예) 제거 / 평균 대체 / 없음]  
   - [스케일링: 예) StandardScaler / MinMax / 없음]  
   - 학습/검증 분리: [예) train_test_split, stratify 사용 여부]

2. 베이스라인 모델 학습  
   - 사용 모델: [예) RandomForest / XGBoost / SVM / LogisticRegression]
   - 기준 성능을 확보한 뒤 feature selection 진행

3. Feature Selection 실험  
   - 모델의 **feature importance**를 계산
   - 중요도가 낮은 feature부터 단계적으로 제거
   - 각 단계에서 성능(Accuracy/F1 등) 측정
   - “성능이 유지되는 구간”과 “급격히 떨어지는 임계점”을 확인
    <img width="772" height="553" alt="image" src="https://github.com/user-attachments/assets/42103386-6551-4163-8220-29bfa6db8040" />

## 결과 요약
- 실험 내용: **196개 feature → [최소 N]개까지 감소**시키며 성능 변화 측정
- 평가 지표: [Accuracy / F1-score / ROC-AUC 중 사용한 것]
- 핵심 결론: 성능이 크게 하락하지 않는 범위는 **대략 [N1~N2]개 구간**이었고,  
  **[임계점: 예) 30개 이하부터 급락]** 형태를 확인함.
- 최종 선택 feature 개수: **[최종 N]개** (성능: [Accuracy 0.xx / F1 0.xx])

## 노트북 구성
- `Legacy_MG_NMG_model_learning.ipynb`  
  - 데이터 로드/전처리, 모델 학습, feature importance 계산, feature 줄이기 실험 전체 흐름
- `MG,NMG_그래프.ipynb`  
  - feature 수 변화에 따른 성능 그래프/시각화 중심 정리
  <img width="2990" height="2390" alt="image" src="https://github.com/user-attachments/assets/0564fda2-eb87-4773-ae12-04a1c4fa1c0a" />
  <img width="3385" height="4364" alt="image" src="https://github.com/user-attachments/assets/bda60c74-e297-4cea-87ad-5da1c246e88f" />
  <img width="1995" height="1589" alt="image" src="https://github.com/user-attachments/assets/85007e8b-9c15-42ac-9594-1946e79c654f" />
