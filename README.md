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

### 사용 모델 선정
#### Yolov5s
다음과 같이 조건을 건다
* 매 프레임마다 검출할 필요가 없다
* 저사양 기기에서도 작동해야 한다
![204180385-84f3aca9-a5e9-43d8-a617-dda7ca12e54a](https://user-images.githubusercontent.com/57976156/205494634-abeafd17-de9d-4f1d-9628-dfcd067d08e6.png)
![54](https://user-images.githubusercontent.com/57976156/205495351-2fb34cf2-6542-4b15-9477-91440cc4d7bb.png)

### 학습결과


## 구현영상
![KakaoTalk_20221204_224739941](https://user-images.githubusercontent.com/57976156/205494386-20f2551d-b8e1-4a1a-bde1-29c43fa76ebd.jpg)
https://youtu.be/pJJOp0dpv8g

## References
1. YOLOv5(https://github.com/ultralytics/yolov5)
