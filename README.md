# Scoring-Risk-from-Drivers-Lane-Change-Video

## 팀원
* 염수웅(팀장)
* 강지우
* 이도영
* 이보영
* 차유경

## 프로젝트 배경 및 목적

쏘카 앱의 누적 다운로드 수가 1000만을 돌파하는 등 카셰어링 업계는 계속해서 성장함에 따라 보험료도 세분화할 필요가 있다고 생각했다. 여러가지 교통사고 발생 원인 중 가장 분쟁이 많은 유형인 차선 변경을 통해 주행 위험도를 감지할 수 있는 프로젝트를 진행하기로 결정했다. 이러한 위험도 수치화는 향후 안전 운전 회원에게는 쿠폰 및 보험료 할은(Benefit)을, 부주의 회원에게는 보험료 인상(Penalty)을 통해 주행 습관 연계 보험 적용에 활용될 수 있다.
 
## 차선 변경 영상에서 위험도 추출

<img src=“https://github.com/ykcha0608/Scoring-Risk-from-Drivers-Lane-Change-Video/issues/1#issue-1304787861” style="width:200px">
</img>

<img src=“https://github.com/ykcha0608/Scoring-Risk-from-Drivers-Lane-Change-Video/issues/2#issue-1304789482” style="width:200px">
</img>

![compressed_safe 0 58](https://user-images.githubusercontent.com/93107210/178995797-129dda5d-6d98-484a-9177-d6b08751947d.gif)


## 학습에서 중요한 요소
* 주변에 차가 많은가
* 주변에 보행자가 많은가
* 차선 변경 시 옆 차선에 차가 있는가
* 차선 변경 시 앞 차와의 간격이 가까운가

## 모델

# Detectron2 (Mask-RCNN)
Mask-RCNN 구조를 활용한 Detectron2를 활용하여 Instance Segmentation

# CNN-LSTM
CNN-LSTM 모델을 통해 데이터의 공간적 특성과 시계열 특성을 학습

## 데이터
* UC Berkeley Deep Dive Dataset의 차선 변경 관련 영상 135개 선정
* 5명의 팀원이 주행자의 차선 변경을 안전/위험으로 Labeling & Scoring
* OpenCV를 이용하여 Frame 이미지로 변환
