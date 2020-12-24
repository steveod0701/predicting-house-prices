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
2. price 단위 스케일링 ```('price' / 10000)```  

## 사용 모델
1. 단순 선형회귀
2. 다중 선형회귀
3. Lasso 회귀분석 (a = 0.1, 1, 100, 1000)
4. KNN (k = 5, 15, 25)
5. Tensorflow 활용 CNN (실패함)

## 변수 선택  
피어슨 상관관계 통계 분석 자료 활용  
집값 'price' 와 상관관계 크다고 나타난 변수 : bathrooms(화장실 수), bedrooms(침실 수), sqft_* (평수), view (전망) 등  

## 초기 분석  
Lasso (a = 0.1) 일때 가장 우수
R-squared : 0.688
5겹 교차 검증 : 0.686

평수-집값 단순 선형 회귀  
![alt text](https://github.com/steveod0701/predicting-house-prices/blob/main/f1.PNG?raw=true)  

다중 선형 회귀    
![alt text](https://github.com/steveod0701/predicting-house-prices/blob/main/f2.PNG?raw=true)  

Lasso 회귀분석 a = 1
![alt text](https://github.com/steveod0701/predicting-house-prices/blob/main/f3.PNG?raw=true)  

KNN 회귀분석 k = 15
![alt text](https://github.com/steveod0701/predicting-house-prices/blob/main/f4.PNG?raw=true)

## 모델 성능 개선  
단순히 오차가 큰 인스턴스 아닌 실제 값에 대한 오차 비율이 큰 이상치 제거  
``` 'error/actual': (actual - predicted)/actual ``` 비율 0.6 이상 이상치 제거


## 결과 분석
| Model         | Details       | RMSE  | R-squared (training) | R-squared (test) | 5-Fold Cross Validation|
| ------------- |:-------------:| -----:| -------------------- |  --------------- |  --------------------- |
| Multiple Regression Error Rate Used | all features| 18.858 | 0.674 | 0.736 | 0.674|
| Lasso Regression Error Rate Used | alpha = 0.1| 18.953 | 0.671 | 0.733 | 0.740|
| Lasso Regression | alpha=0.1|	20.017|	0.671	|0.688|	0.686|
|	Lasso Regression|	alpha=1 |	22.447|	0.601|	0.607	|0.601| 
|	Simple Linear Regression Error Rate Used|	-	|24.097	|0.492	|0.569|	0.491|
|	KNN Regression|	k=15|	24.283|	0.562	|0.541	|0.434|
|	KNN Regression Error Rate Used	|k=5|	24.401|	0.671|	0.558|	0.474|
|	KNN Regression	|k=25	|24.703	|0.529	|0.525	|0.423|
|	Multiple Regression|all features|	24.851|	0.514|	0.519|	0.512|
|	KNN Regression	|k=5|24.938	|0.671	|0.516	|0.421|
|	Lasso Regression|	alpha=100|24.954	|0.510	|0.515	|0.508|
|	Lasso Regression	|alpha=1000	|25.165|	0.500	|0.507|	0.501|
|	Simple Linear Regression|	-	|25.429|	0.492|	0.496|	0.491|

- 성능 개선 전 :
Lasso (a=0.1) > Lasso (a=1) > 다중선형회귀  
KNN 평가 성능 낮음 : 집값 데이터가 밀집되어있지 않음

- 성능 개선 후 :
Lasso(a= 0.1) 5겹 교차 검증값 우수, 다중선형회귀가 RMSE 우수  
단순 선형(평수-집값) 회귀도 어느정도 납득할만한 평가 메트릭을 나타냄 (R-squared 0.569, 교차검증값 0.491)  
KNN 여전히 미흡 (R-squared 0.541, 교차검증값 0.434)  

[서울시 주택가격지수 통계](https://data.seoul.go.kr/dataList/10185/S/2/datasetView.do;jsessionid=CA5940711C15F682C16F622901BD2246.new_portal-svr-21)  
작성된 모델을 위 서울 주택가격지수 통계와 같은 다른 데이터셋에도 적용해 볼 계획  
추가로 Keras를 이용한 인공신경망 모델도 공부해 볼 계획  



