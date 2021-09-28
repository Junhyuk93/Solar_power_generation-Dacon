# ☀데이콘 태양광 발전량 예측 AI 경진대회☀

## 대회 주제

예시로 제시된 지역의 기상 데이터와 과거 발전량 데이터를 활용하여, 시간대별 태양광 발전량을 예측

기대효과: 시간대별 소비자 그룹의 전력소비량 예측 데이터와 결합하여 가장 효율적인 시간대별 태양광 발전과 국가 전력망을 조합 가능. 각 소비자 그룹에 최적화된 공급계획 수립 가능.  

## 대회 배경

신재생 에너지 태양광 발전량 예측을 위한 시계열 데이터 분석기법 발굴  
신재생 에너지 관리 솔루션 개발 활용 및 에너지 서비스 산업 발전 촉진   

## 대회 설명

태양광 발전은 매일의 기상 상황과 계절에 따른 일사량의 영향을 받음. 이에 대한 예측이 가능하다면 보다 원활하게 전력 수급 계획을 세울 수 있음.

신재생에너지의 생산 효율성을 극대화하고, 사용자들에게 저렴한 전력을 공급할 수 있도록 인공지능 기반 태양광 발전량 예측 모델을 만들 것.

**모델은 7일(Day0 ~ Day6) 동안의 데이터를 인풋으로 활용하여, 향후 2일(Day7 ~ Day8) 동안의 30분 간격의 발전량(Target)을 예측해야 함. (1일당 48개씩 총 96개 timestep에 대한 예측)**

## Dataset

- train.csv : Day0 ~ Day1094 (3년) 동안의 기상 데이터와 발전량(target) 데이터
- test fold files : 81개의 폴더로 이루어진 2년 동안의 기상데이터와 발전량(target) 데이터
    - 시계열 순서와 무관하며 순서는 랜덤
- submission.csv : test 폴더의 각 파일에 대해서 시간대별 발전량을 9rodml quantile(0.1 ~ 0.9)에 맞춰서 예측.
    - '파일명_날짜_시간' 형식(ex:0.csv_Day7_0h00m --> test 폴더 0.csv 파일의 7일차 0시 00분 예측 값)

## Explanation of columns


* Day : 날짜
* Hour : 시간
* Minute : 분
* DHI : 수평면 산란일사량(Diffuse Horizontal Irradiance (W/m2))
* DNI : 직달일사량(Direct Normal Irradiance (W/m2))
* WS : 풍속(Wind Speed (m/s))
* RH : 상대습도(Relative Humidity (%))
* T : 기온(Temperature (Degree C))
* Target : 태양광 발전량 (kW)


## Model

### RandomForestRegressor

![](https://i.imgur.com/HOwmusB.png)

*수정예정*


## Evaluation

- Metric : Pinball Loss
- Public Score : 1.79638 20th (20/469)
- **Private Score : 2.02358 13th (13/469)**

Public score에 연연하지않고 과적합을 방지하기 위해 앙상블 기법을 활용하여 Robust한 모델을 사용했기 때문에 Private Score에서 좋은 점수를 받아낸 것 같음.

![](https://i.imgur.com/rwJ171g.png)
