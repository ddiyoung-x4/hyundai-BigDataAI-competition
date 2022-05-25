# hyundai-BigDataAI-competition
제2회 조선/해양 산업 디지털 혁신을 위한 Big Data/AI 대학생 경진대회  

## Schedule
22.01.24 ~ 22.02.18 과제 제출  
22.02.21 참가팀 online presentation  
22.02.25 결과 발표 및 시상  

## 1. 화물 이동 차량의 영상 분석: 화물 적재 유/무 판단(Classification)
1. 예외적인 image 분류  
-1) 화물차가 움직일 때 (특히, 차량이 회전할 때)  
-2) 화물이 카메라 전체를 가릴 때  
  
2. 데이터 분석  
-1) FP  
트레일러 위와 측면에 사람, 그림자, 차량 각도  
-2) FN  
작은 물체, 차량 각도, 평평한 물체, 바닥이 안보이는 경우  

<img width="80%" src="https://user-images.githubusercontent.com/69739208/170207564-c0ae69ce-cb10-4569-9d15-eab466b861bf.png"/>  

3. Solution  
  
-1) 데이터 전처리  
[1] MixUp  
같은 클래스의 이미지끼리 투명도를 주어 합침으로써 새로운 데이터를 구축함.  
[2] Cutblur  
이미지의 모든 부분을 골고루 보게하는 기술  
본 task의 경우 화물차를 제외한 부분에 blur 처리한 후 적용함.  
<img width="70%" src="https://user-images.githubusercontent.com/69739208/170208954-5efeff9e-8412-40d6-87b6-05db5ead2ab4.png"/>  
  
-2) 분석 모델, EfficientNet-b0  
  
|img_size|256x256|400x400|400x400 gray|400x400 gray+random_rotation|
|:------:|---:|---:|---:|---:|
|FP|32|17|26||
|FN|80|115|46|400 > |
|val_acc|none|none|none|none|
|분석||확실하게 구분하는 대신에, 구분하는 것에서 에러|확실하게 구분하지는 못했는데, 잘 못 구분한 것 감소||

-3) CAM(Class Activation Map)_grad  
  
이미지에서 어떠한 부분이 class를 구분하는데 중요한 정보를 나타내는지, 해당 중요도를 쉽게 알 수 있음.  
데이터 전처리를 통해, 화물 적재 영역에 해당하는 부분에 집중하고 있음을 볼 수 있음.  
<img width="70%" src="https://user-images.githubusercontent.com/69739208/170212928-8c3e242c-b10f-4efa-9e46-66d784d0ab99.png"/>  

4. 성능 지표 제시
  
-1) 제시된 Test Case 20개 이미지, 0.95의 정확도  
-2) Train Set에서 1300개 이미지 추출, Test Set 11%  
class label 1에 대한 예측: 0.9579  
class label 0에 대한 예측: 0.9915 비교적 우수  
  
|:------:|Accuracy|
|Test Case 20개|0.95|
|Aug Set_라벨1 475개|0.9579|
|Aug Set_라벨0 825개|0.9915|






