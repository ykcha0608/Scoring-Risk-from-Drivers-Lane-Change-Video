# Scoring-Risk-from-Drivers-Lane-Change-Video

## Team members
* Yukyung Cha
* Suwoong Yeom
* Jiwoo Kang
* Doyoung Lee
* Boyoung Lee

## Motivation and Goal

As the market size of car sharing industry in Korea is growing up rapidly, we came to a conclusion that the insurance fee should be subdivided by driver's habit of driving. Since lane changing was one of the most conflictful reasons that occurs car accident, we decided to implement a project that we can detect the degree of risk in driving from lane changing dashcam videos. By quantifying the driver's habit of driving, we intend to leverage this data into rewarding the customers with coupons and insurance fee discount as well as imposing penalties to them.
 
## Extracting risk scores from the lane changing videos

The two examples below show the risk scores when the drivers change the lane each. First one video scored as 0.41 and second video was scored as 0.31.

![compressed_safe 0 58](https://user-images.githubusercontent.com/93107210/178995797-129dda5d-6d98-484a-9177-d6b08751947d.gif)

![safe 0 68](https://user-images.githubusercontent.com/93107210/178995930-6042e342-fbae-4c4a-964b-eac8faba80d7.gif)


## Important factors in model training
* Is there a lot of cars around?
* Is there a lot of pedestrians around?
* Is there a car in the next lane when the driver changes the lane?
* Is it close from the car in front when the driver changes the lane?

## Model

# Detectron2 (Mask-RCNN)
Implemented instance segmentation on each frames of videos leveraging Detectron2 that has Mask-RCNN structure. It showed a remarkable performance exactly detecting person, car, traffice light etc.

# CNN-LSTM
The model learned spatial and time-series characteristics of the data through CNN-LSTM model

## Data
* Picked 135 lane changing video from UC Berkeley Deep Dive Dataset
* Each of the team members labeled and scored the videos with risk score from 1(safe) to 5(dangerous)
* Utilized Mask RCNN which was trained with Microsoft COCO2017 Dataset in Detectron2

## 1st Trial (165 videos, scoring 1~3)

### The result of testing first 5 videos

![image](https://user-images.githubusercontent.com/83010037/179005489-bd8a9b5e-1f9d-4d41-8ada-d5377b6745e8.png)

### Result and Feedback of 1st Trial

1. In the first test, we tested 5 videos with the moddel right after the completion of model but the results from each video were all same.
2. We came to a conclusion that this overfitting has occured since we set the epoch as 1000.
3. Utilizing Wandb tool, we figured out the optimal epoch is 100 and applied it to the model.
4. From the results that almost every video got scored as safe, we judged scoring the videos only from 1 to 3 was not enough.
5. We enlarged the range of score from 1 to 5, removed the videos that were not relevant to lane changing.
6. As a result, the video data that were used in the training decreased from 165 into 135. 

## 2nd Trial (Downscaled into 135 videos, scoring1~5)

### The result of testing first 5 videos

![image](https://user-images.githubusercontent.com/83010037/179006095-8e1ed66c-9843-40db-b0b9-88a21a47f7aa.png)


        
### Result and Feedback of 2nd Trial

1. Implemented second test after analyzing the result of the first test.
2. Likewise, carried out the first test with 5 videos that were used in model training and derived various results.
3. The first video that appeared on the result was judged as safe, and second video was judged as dangerous before the test.
4. The results didn't meet our expectations.
5. From reviewing Instance Segmentation result, we realized that the objects in same category was covered with different colors in each fram and we assumed this caused the problem.


![image](https://user-images.githubusercontent.com/83010037/179006421-9216a30f-8783-401b-b457-993c06c743a9.png)
![image](https://user-images.githubusercontent.com/83010037/179006445-56185118-f052-4e76-94a5-3152b1d89b9f.png)
![image](https://user-images.githubusercontent.com/83010037/179006461-413eab84-104f-4678-8d9d-0b32209c04f5.png)
![image](https://user-images.githubusercontent.com/83010037/179006484-9f3e3f5f-5e98-4546-a142-0c3076da90b9.png)
        
## Mini Alpha Trial(Without segmentation)

### The result of testing two videos
![image](https://user-images.githubusercontent.com/83010037/179006841-d9547307-36f9-4119-9a5e-5bc9d90ac6e5.png)
![image](https://user-images.githubusercontent.com/83010037/179006859-fd2c2597-12bc-4606-aef9-a04a1ec2e8c8.png)



### Result and Feedback from Mini Alpha Trial

1. The result from testing some videos that were not applied Instance Segmentation met our expectation.
2. From this result, we concluded that the same objects covered by different colors affected the training
3. Since we splited the videos into frames first then implemented Instance Segmentation, same objects had different colors in each frame.

### Explanation about each directory

- test : The file that we implemented test on Google Colab
- Mask_RCNN : We conducted image fram Instance Segmentation with Detectron2 which is Meta's open source and is based on Mask RCNN that is trained with COCO dataset.
- lane_change_risk_detection : It contains the real model including cnn_lstm, Trainer file, as well as cnn and ResNet to compare the performance with cnn_lstm.

### Limitation

- There was no clear and professional norm in scoring the risk. All the videos were scored from from team members' perspectives.
    → It is considered that this affected to the degradation in assessing the risk
    
- Objects in same categories were covered by different colors in each frame.
    → If the objects in same categories are covered by same colors, the performance will be improved.


--------
### Reference
- Risky Action Recognition in Lane Change Video Clips using Deep Spatiotemporal Networks with Segmentation Mask Transfer
  Paper : https://arxiv.org/pdf/1906.02859.pdf
  GitHub : https://github.com/Ekim-Yurtsever/DeepTL-Lane-Change-Classification


- Scene-Graph Augmented Data-Driven Risk Assessment of Autonomous Vehicle Decisions
  Paper : https://arxiv.org/pdf/2009.06435.pdf
  GitHub : https://github.com/louisccc/sg-risk-assessment

----------
