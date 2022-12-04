# Capstone_Design2
# YOLO를 이용한 잔디밭 잡초 검출
* 경희대학교 컴퓨터공학과 김민석
* 지도교수: 경희대학교 컴퓨터공학과 최진우


## 개요
### 연구 배경

![20160803_111043](https://user-images.githubusercontent.com/57976156/205490046-e41deb92-8499-4c08-b8cc-caeff7a6e6a7.jpg)
* 은퇴인구수 증가

* 자아실현(마당있는 단독주택에서 거주)

* 잔디는 조경의 베이스

# 
### 관련 연구 & 데이터
#### 해외 농업분야 잡초검출 연구
![41](https://user-images.githubusercontent.com/57976156/205490634-ab4ba1a5-d7a2-4210-b5de-dba9afe818f8.png)

대규모 농사를 짓는 미국, 호주 등 국가에서는 농지 잡초 검출 연구가 이미 활발히 진행되고 있음

#### AI-hub 잡초 데이터셋
![42](https://user-images.githubusercontent.com/57976156/205490730-21fe61ac-d0cb-4f95-9df0-9780e4a2c6cf.png)

### 연구의 중요성
* 해외-한국: 생태계, 기후의 차이

* 잔디밭은 물이 잘 빠지는 마사토에서 기름

* 제초제의 한계
따라서 해당 연구에서는 단순한 녹화가 아닌 반려견을 탐지하고, 행동을 분류하여 특정 행동을 언제 했는지 탐지하고, 기록하는 기능을 구현하고자 한다.

# 
### 사용 모델
#### Yolov5

![image](https://user-images.githubusercontent.com/72953874/204129399-d6973f11-36bc-41eb-b608-5932c09e65e3.png)

<br>

또한, 다른 yolo 버젼들과 비교하여 용량이적고 속도가 빠르다는 장점을 가지고 있다.

![image](https://user-images.githubusercontent.com/72953874/204129631-19418d3f-66e3-41ba-add1-9a0bfd45d0bf.png)
![image](https://user-images.githubusercontent.com/72953874/204129632-90e835a2-7d0b-41d3-9cbc-eeb2e8c1105d.png)


2. Google Teachable Machine

![image](https://user-images.githubusercontent.com/72953874/204129504-1ae917f4-cce3-4c3f-bbe9-4956a7911e33.png)

쉽게 모델을 학습하고 export하여 사용 할수있는 서비스로, js, keras 등등으로 export 할 수 있어서 편리하다. 본 연구에서는 행동분류를 위한 모델로 사용된다. 본 연구에서는 keras로 export하여 yolov5를 통과한 이미지에 대해서 행동분류를 진행한다.

3. Flask

파이썬 기반의 웹 프레임워크로 해당 연구에서 파이썬 기반으로 작성된 yolov5에 간편하게 덧입혀 쉽게 웹 서버를 구축한다. 또한 jinja 템플릿 엔진을 통해 동적 페이지를 만들어준다.


## Results
1. YOLOV5 학습

annotaion과 image가 함께 있는 [standard dogs Dataset](http://vision.stanford.edu/aditya86/ImageNetDogs/)을 이용하여 yolo를 학습시킨다. 단, 이미지가 너무 많으므로 (몰티즈, 푸들, 포메라니안, 치와와, 골든리트리버, 시추)로 한정시켜 약 1400장에 대해 학습시키며 annotation이 yolo의 형식과는 다르므로 변형하여 학습시켜준다.<br>
test data는 학습할때 사용한 종을 제외한 다른 종의 이미지 1000장으로 진행한다.


![image](https://user-images.githubusercontent.com/72953874/204130906-9877208b-dfac-4a9f-8a88-21ac93f75774.png)

![image](https://user-images.githubusercontent.com/72953874/204130918-ba3e2bf0-d82b-4b7a-95e9-06c82c81a8f4.png)

![image](https://user-images.githubusercontent.com/72953874/204130924-fdf966d8-c2d1-40a6-860e-b2dbd4c0dc94.png)

결과적으로 위와 같은 학습 결과를 얻었다.


2. Teachable Machine 학습

Teachable Machine을 학습시키기 위한 반려견 행동별 데이터는 찾지 못했다. 따라서 웹서치와 standard dogs dataset을 수작업으로 분류하여 행동 클래스별 100장에 대해 학습시켰다.
test data는 각 행동별 25장에 데이터로 구성하였다. 학습결과 0.72의 accuracy를 얻었으며, 엎드려서 밥을 먹거나, 다리를 쭉 뻗고 걷는 것 처럼 엎드린 모습 등 동시성이 있는 이미지나, 행동이 비슷한 이미지로 인해 정확도가 떨어지는 모습을 보였다.

3. 추가기능 

여러마리의 반려견이 등장할 경우, 각각의 반려견의 이름을 구별해주는 기능을 구현하려고 시도해보았다. 예를들어, 허스키와 말티즈의 경우 특징이 서로 뚜렷하기때문에 조금의 데이터만 사용자에게 받아도 구분이 가능할 것이라고 생각하여 사용자에게 이미지를 받아 아래의 모델로 학습하고, 구분하도록 해보았다.

![train_batch0](https://user-images.githubusercontent.com/57976156/205486964-818cecef-8bd4-435c-a83d-9e6c2a22e26c.jpg)

``` python
model = Sequential([
   layers.Input(shape=(224, 224, 3)),
   layers.Conv2D(16, 3, padding='same', activation='relu'),
   layers.MaxPooling2D(),
   layers.Conv2D(32, 3, padding='same', activation='relu'),
   layers.MaxPooling2D(),
   layers.Conv2D(64, 3, padding='same', activation='relu'),
   layers.MaxPooling2D(),
   layers.Flatten(),
   layers.Dense(128, activation='relu'),
   layers.Dense(1, activation="sigmoid")
])
```

결과적으로 각각의 이미지 10장에 대해서는 0.54의 정확도를 보여주었고 100장씩 넣어봐도 0.6을 조금 넘는 수준이라 적용하기는 어렵다고 판단됐다.

4. Flask 웹 서버 구축

플라스크는 다음과 같은 로직으로 구성되었으며, 1초에 30프레임이 들어오는 동영상의 특성상, 행동분류의 오류가 자주 발생할 것으로 예상되어 3초에 1번 이전 행동과 다르다면 기록하는 방식으로 진행하였다.

![image](https://user-images.githubusercontent.com/72953874/204131117-9710f54a-3a26-4f55-b0c0-5e0413d645de.png)


5. 결과

## Conclusion
* Summary

결과적으로 견주들의 가장 큰 걱정인 외출시 반려견이 걱정되는 문제를 덜어주기 위한 cctv의 기능 중, 기존의 기능들과는 다르게 반려견의 행동을 분석하고, 행동을 기록해주는 기능을 구현해 볼 수 있었다.

* Future plan
1. 이미지 1장에 1마리가 포함된 Stanford dogs data로 인해 떨어지는 YOLO모델의 여러마리 반려견에 대한 탐지 정확도 개선
2. 행동분류의 이미지 수집 및 과소적합 해소
3. 여러마리의 반려견 등장시 각각에 대한 처리


## References
1. [You Only Look Once: Unified, Real-Time Object Detection](https://arxiv.org/abs/1506.02640)
2. [Google Teachable Machine](https://teachablemachine.withgoogle.com/)
3. [standard dogs Dataset](http://vision.stanford.edu/aditya86/ImageNetDogs/)
4. [yolov4-versus-yolov5](https://blog.roboflow.com/yolov4-versus-yolov5/)
