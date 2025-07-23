# 🔍 S&P 500 지수 방향성 예측을 위한 경제지표 기반 머신러닝 모델링

## 📝 개요  
본 프로젝트는 금융 자산 가격 및 거시경제 지표를 활용해 **미국 S&P 500 지수의 단기 상승 여부를 예측**하는 분류 모델을 개발하고, 투자 판단을 위한 **데이터 기반 의사결정의 근거**를 제공하는 것을 목표로 합니다.

---

## 📌 주요 결과 요약  
- VIX, 금리, 원자재, 경제지표 등 30여 개 파생변수를 활용한 특성 엔지니어링 수행  
- SMOTE를 통한 클래스 불균형 보정 및 시간순 분할(train/test)로 과최적화 방지  
- Logistic Regression, Random Forest를 비교 분석 → RF 기준 AUC 0.94  
- **변화율 기반 변수와 S&P 기술지표**가 예측에 가장 큰 영향

---

## 🎯 타겟 정의  
- 다음 거래일 기준 **S&P 500 종가가 +0.2% 이상 상승하는지 여부**를 이진 분류

---

## 📁 데이터 소개  
- 기간: 2015.01.01 ~ 2024.12.31  
- 출처: Yahoo Finance, FRED 등  
- 주요 변수:
  - 금융 자산: `VIX`, `금`, `구리`, `원유`, `국채금리` 등  
  - 경제지표: `소비자물가(CPI)`, `실업률`, `소매판매`, `기대 인플레이션` 등  
- 파생 변수 예시: `CPI_change`, `VIX_MA_5`, `SP500_volatility`, `GOLD_to_SP500_ratio` 등

---

## 🧪 주요 전처리 및 모델링  
- **전처리**
  - 누락값 제거 및 경제지표 시차 정렬  
  - StandardScaler로 정규화  
  - SMOTE로 클래스 불균형 보정  
- **모델링**
  - 시계열 특성을 고려해 train(2015~2022) / test(2023~2024) 분할  
  - Logistic Regression / Random Forest 비교  

| 모델             | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|------------------|----------|-----------|--------|----------|---------|
| Logistic Reg.    | 0.7163   | 0.7179    | 0.6914 | 0.7044   | 0.79    |
| Random Forest    | 0.8753   | 0.8787    | 0.8642 | 0.8714   | 0.94    |

---

## 📈 주요 결과 시각화

- 변수 중요도  
  ![](./images/feature.png)

- Confusion Matrix  
  ![](./images/confusion.png)

- ROC Curve  
  ![](./images/ROC_Curve.png)

- Precision-Recall Curve  
  ![](./images/Precision_Recall.png)

---

## 🧠 핵심 인사이트 요약  
- **S&P500의 기술 지표 (모멘텀, 변동성)**이 가장 강력한 예측 변수  
- **변화율 기반 변수들(CPI_change, WTI_change 등)**이 절대값보다 예측 성능 우수  
- 금값과 S&P 간 역관계는 투자 심리(위험 회피)의 신호로 활용 가능  
- Random Forest가 경제적 해석력과 성능 측면에서 우수

---

## 🛠 사용 기술 스택  
- Python (pandas, numpy, scikit-learn, matplotlib, seaborn)  
- SMOTE (imbalanced-learn)  
- Jupyter Notebook

---

## 📁 폴더 구조
sp500-direction-prediction/
├── data/ # 원본 및 파생 데이터셋
├── images/ # 시각화 이미지
├── notebooks/ # 분석 노트북
├── reports/ # 최종 보고서
├── requirements.txt # 라이브러리 목록
└── README.md # 프로젝트 설명

---

## 📄 보고서 및 코드  
- 📘 [최종 보고서 PDF](./report/Project_Report.pdf)  
- 📓 분석 코드: `notebooks/` 폴더 참고

---

## ⚙️ 실행 환경  
```bash
conda create -n sp500env python=3.9
conda activate sp500env
pip install -r requirements.txt
```
---

## 🚀 향후 개선 방향
- 트리 기반 앙상블 모델 최적화 (XGBoost, LightGBM 등)
- 타겟 정의 다변화 (변동성 포함, 수익률 기반 분류 등)  
- 거래 전략 시뮬레이션 통합을 통한 실제 수익 가능성 검증  
- 경제 상황에 따른 조건부 모델링 (침체기 vs 확장기 등)

---

## 👥 팀 정보 및 역할
본 프로젝트는 5인 팀 프로젝트로 수행되었습니다.

| 이름  | 역할                                  |
| --- | ----------------------------------- |
| 김도현 | 데이터 수집, 변수 엔지니어링, Random Forest 모델링 |
| 김정운 | 경제지표 분석, Random Forest 모델 성능 개선     |
| 오현민 | 시각화 및 EDA, 최종 결과 정리 지원              |
| 이영섭 | 모델 비교, 최종 보고서 작성                    |
| 장다향 | 로지스틱 회귀, 피처 중요도 분석, 문서 편집           |
