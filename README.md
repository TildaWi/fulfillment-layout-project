# 물류센터 피킹 효율성 개선을 위한 머신러닝 기반 '진열 방식 최적화' 프로젝트

### 분석 카테고리: 데이터 활용 모델링
> **분석 기간** &nbsp;|&nbsp;  2025.05 - 2025.05 <br/>
> **분석 주체** &nbsp;|&nbsp;  개인 프로젝트 <br/>
> **분석 기법** &nbsp;|&nbsp;  ABC 분석, 예측 모델링, 시뮬레이션 <br/>
> **분석 기술** &nbsp;|&nbsp;  <img src="https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white"/> <img src="https://img.shields.io/badge/Seaborn-3776AB?style=flat&logo=seaborn&logoColor=white"/> <img src="https://img.shields.io/badge/Tableau-E97627?style=flat&logo=tableau&logoColor=white"/> <img src="https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white"/>  

---

## 0. 들어가기 전에

### 📂 디렉토리 구조

```plaintext
📁 fulfillment_layout_project/
 ┣ 📁 data/              원천 데이터 (상품, 주문, 피킹 이력 등)
 ┣ 📁 notebooks/         분석 및 모델링 코드 (Colab)
 ┣ 📁 images/            시각화 결과 (파레토차트, 모델 성능 비교 등)
 ┣ 📁 reports/           보고서 및 발표자료 (PDF, PPT)
 ┣ 📄 README.md          프로젝트 설명 문서
 ┗ 📄 requirements.txt   사용한 Python 패키지 목록
```

---
## 1. 프로젝트 개요

### 📌 세 줄 요약
- 물류센터의 피킹 작업 생산성 향상을 위해 진열 방식을 분석하고 최적화 방안을 제시했습니다.  
- 주문 빈도 기반 ABC 등급 분류 및 머신러닝 모델을 통해 상품을 구획화하고, 진열 시뮬레이션을 수행했습니다.  
- 시뮬레이션 결과, ABC 기반 진열 방식은 기존보다 피킹 효율성을 35.3%, 전체 처리시간을 19.5% 개선했습니다.  

---

## 2. 문제 정의 및 접근 방식

### 🔍 Situation
- 기존 물류센터는 상품 주문 빈도를 고려하지 않고 무작위로 진열되어 있어 피킹 동선이 비효율적이며 생산성 저하 발생  

### 💡 Task  
- 주문 빈도 기반 진열 최적화 방안을 설계하고, 기존 진열과의 효율 차이를 검증  

### 🏃 Action
- 피킹 로그 및 주문 데이터를 바탕으로 EDA → ABC 등급 분류 → 효율성 지표 수립  
- 진열 방식에 따른 시뮬레이션 설계 및 통계적 가설 검정  
- ABC 등급 예측을 위한 머신러닝 모델 설계 및 성능 비교  

### 🚀 Result
- ABC 기반 진열 방식은 기존 방식 대비 피킹 효율성, 작업시간, 처리속도, 오류율 등 모든 지표에서 유의미한 개선 효과  
- 최종적으로 Random Forest 모델을 활용한 ABC 예측 정확도는 97.4%로 확인됨  

---

## 3. 프로젝트 진행

### 3-1) 📊 EDA 요약

- 전체 주문의 80%는 상위 20% 상품에서 발생하는 파레토 분포 확인  
- 상위 상품일수록 위치 분산도가 높고, 피킹 동선 낭비 발생  
- 작업자별 피킹 시간, 주문 밀도, 카테고리별 이동거리 등 시각화 분석 수행  

📊 **삽입 이미지**: `images/pareto_chart.png`  
📊 **삽입 이미지**: `images/location_distribution_heatmap.png`  

---

### 3-2) 🧪 가설 검정: 진열 방식별 효율 비교

- **H0 (귀무가설)**: 기존 방식과 ABC 기반 진열 방식 간 피킹 효율성에는 유의미한 차이가 없다  
- **H1 (대립가설)**: 두 방식 간 피킹 효율성에는 유의미한 차이가 존재한다  

#### 검정 방법
① 정규성 검정 → ② 등분산 검정 → ③ 일원분산분석(ANOVA)  
④ 사후 검정 → ⑤ 효과 크기 검정 → ⑥ t-검정  

**결과**: 모든 주요 지표에서 유의미한 차이가 나타나 귀무가설을 기각하고 대립가설을 채택함  

📊 **삽입 이미지**: `images/stat_test_summary.png`  

---

### 3-3) 🤖 모델링 및 시뮬레이션

#### 머신러닝 기반 ABC 예측 모델링
- 단변량 예측 모델 설계  
- 주요 변수: 주문 빈도(`order_frequency`), 주문 밀도(`order_density`), 카테고리 등급 등  

| 모델 | 정확도 | 교차검증 평균 |
|------|--------|----------------|
| Random Forest | **0.9740** | **0.9663 ± 0.0066** |
| Logistic Regression | 0.9594 | 0.9659 ± 0.0091 |
| SVM | 0.9594 | 0.9659 ± 0.0091 |

📊 **삽입 이미지**: `images/model_accuracy_comparison.png`  

---

## 4. 프로젝트 회고

✏️ Learned Lessons
- 물류센터는 단순히 “많이 팔리는 상품”이 아닌 **작업 동선과 접근성**을 함께 고려한 진열이 필요함을 실감  
- 분석 결과를 실제 운영 방안으로 제안할 수 있도록, **정량 지표 기반 시나리오 설계와 시각화**가 중요  
- 머신러닝을 통해 **‘진열 전략’을 데이터 기반으로 뒷받침**할 수 있는 가능성을 확인한 실용적 프로젝트였음  
