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

### 연구의 중요성/독창성
* 해외-한국: 생태계, 기후의 차이<br>
* 잔디밭은 물이 잘 빠지는 마사토에서 기름<br>
* 제초제의 한계<br>
따라서 해당 연구에서는 단순한 녹화가 아닌 반려견을 탐지하고, 행동을 분류하여 특정 행동을 언제 했는지 탐지하고, 기록하는 기능을 구현하고자 한다.

#
### 데이터 수집
![2022-11-25 192944](https://user-images.githubusercontent.com/57976156/205491863-4c25934c-9d25-4fb5-bd70-6a9e96c4ec2a.png)

![44](https://user-images.githubusercontent.com/57976156/205491736-8a588fda-8e16-4c3e-a096-cde98d218968.png)
* 직접 데이터 수집(동영상 촬영)<br>
* 구글에서 이미지별 각 100~150개 수집<br>

### 사용 모델
#### Yolov5

![image](https://user-images.githubusercontent.com/72953874/204129399-d6973f11-36bc-41eb-b608-5932c09e65e3.png)

<br>

또한, 다른 yolo 버젼들과 비교하여 용량이적고 속도가 빠르다는 장점을 가지고 있다.

![image](https://user-images.githubusercontent.com/72953874/204129631-19418d3f-66e3-41ba-add1-9a0bfd45d0bf.png)
![image](https://user-images.githubusercontent.com/72953874/204129632-90e835a2-7d0b-41d3-9cbc-eeb2e8c1105d.png)



## 구현영상

https://youtu.be/pJJOp0dpv8g

## References
1. [You Only Look Once: Unified, Real-Time Object Detection](https://arxiv.org/abs/1506.02640)
2. [Google Teachable Machine](https://teachablemachine.withgoogle.com/)
3. [standard dogs Dataset](http://vision.stanford.edu/aditya86/ImageNetDogs/)
4. [yolov4-versus-yolov5](https://blog.roboflow.com/yolov4-versus-yolov5/)
