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
  
3. Solution  
EfficientNet-b0  
  
|img_size|256x256|400x400|400x400 gray|400x400 gray+random_rotation|
|:------:|---:|---:|---:|---:|
|FP|32|17|26||
|FN|80|115|46|400 > |
|val_acc|none|none|none|none|
|분석||확실하게 구분하는 대신에, 구분하는 것에서 에러|확실하게 구분하지는 못했는데, 잘 못 구분한 것 감소||
