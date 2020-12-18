# predicting-house-prices
predicting-house-prices

# 머신러닝 방법론 적용 집값 예측

## 사용 데이터셋
[Kaggle King County 집값 데이터셋](https://www.kaggle.com/harlfoxem/housesalesprediction)

## 사용 라이브러리
1. numpy
2. seaborn (시각화 모듈)
3. pandas
4. scikit-learn

## 초기 전처리
1. 고유 ID 값 등 인덱스 제거
2. price 단위 스케일링

## 사용 모델
1. 단순 선형회귀
2. 다중 선형회귀
3. Lasso 회귀분석 (a = 0.1, 1, 100, 1000)
4. KNN (k = 5, 15, 25)
5. Tensorflow 활용 CNN (실패함)

## 변수 선택  
피어슨 상관관계 통계 분석 자료 활용  
집값 'price' 와 상관관계 크다고 나타난 변수 : 화장실 수, 평수, 거실평수, 전망 등  

## 초기 분석  
Lasso (a = 0.1) 일때 가장 우수
R-squared : 0.688
5겹 교차 검증 : 0.686

## 모델 성능 개선  
단순히 오차가 큰 인스턴스 아닌 실제 값에 대한 오차 비율이 큰 이상치 제거  

## 결과 분석
- 성능 개선 전 :
Lasso (a=0.1) > Lasso (a=1) > 다중선형회귀
KNN 평가 성능 낮음 : 집값 데이터가 밀집되어있지 않음

- 성능 개선 후 :
Lasso(a= 0.1) 5겹 교차 검증값 우수, 다중선형회귀가 RMSE 우수
단순 평수-집값 회귀도 어느정도 납득할만한 범위 (R-squared 0.569, 교차검증값 0.491), KNN 여전히 미흡



