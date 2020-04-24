# Evaluation 


|![](https://hoya012.github.io/assets/img/object_detection_fourth/fig3.PNG) |![](https://hoya012.github.io/assets/img/object_detection_fourth/fig4.PNG)|
|-|-|
![](https://i.imgur.com/4MHBJoz.png)

- True Positivie(TP)	True 인데, True라고 맞춘 경우(잘한 경우)
- False Negative(FN)	True 인데 False 라고 한 경우(틀렸어요.)
- False Positive(FP)	False 인데, True라고 한 경우(틀렸어요.)
- True Negative(TN)	False 인데, False라고 맞춘 경우(잘한 경우)

---

![](https://i.imgur.com/atBT1ux.png)

|![](https://i.imgur.com/OFpcgAc.png)|![](https://i.imgur.com/p6npcBu.png)|![](https://i.imgur.com/hf80DVr.png)|
|-|-|-|
|Accuracy|Error Rate|Precision|
|![](https://i.imgur.com/3VDqaKg.png)|![](https://i.imgur.com/LPZyApp.png)|![](https://i.imgur.com/qrtq4AU.png)|
|Recall|True negative rate(Specificity)|False Positive rate|


### Accuracy : 정확도 
- 전체 중에 틀린걸 틀리다고, 맞는걸 맞는다고 한 경우 
- (TP+TN)/전체 

### Error Rate : 에러율 
- 전체 중에 잘못 분류한 비율 
- (FN+FP) / 전체 

### Precision : 정밀도, (검출한 것의) 정확도
- True라고 한것 중에서 진짜 맞는게(True) 몇개인지? Positive 정답률 `positive predictive value(PPV)`
- Recall의 반대 
- TP / (TP + FP)

### Sensitivility/Recall : 민감도/검출율 / 재현율 (True positive Rate)
- 진짜 True 중 얼마나 True를 몇개나 맞추었나. (다 맞다고 하면 Recall은 100%)
- Precision의 반대 
- TP / (TP + FN) 
- True Set을 넣었을때 True로 인식한 것의 비율 `1이라는 값을 넣었을때 1이 나올 비율  `

### 특이도 : Specificity (True negative rate)
- 값은 Negative 로 판단한것중에, 실제 Negative 값의 비율
- SP = TN / TN+FP
- False Set을 넣었을때 False로 인식할 비율  `0이라는 값을 넣었을때 0이라는 결과를 얻을 비율 `

### False Positive rate
- 원래는 Positive 값인데, 잘못해서 Negative로 판단한 비율
- FPR = FP / N
- 암환자 분류에 중요, 잘 맞추는 것보다 못 맞추는걸 줄이는게 필요 

---

## IOU

|![](https://hoya012.github.io/assets/img/object_detection_fourth/fig1.PNG)|![](https://i.imgur.com/MiOToDt.png)|
|-|-|

Let’s say you set IoU to 0.5, in that case

-   IoU ≥0.5 : 제대로 탐지함 `True Positive(TP)`

-   IOU <0.5 : 잘못 탐지함 `False Positive(FP)`

-   사물이 있는데(GT) 탐지를 못하면 : 탐지 실패 `False Negative(FN)`

-   없는것을 없다고 표시 : 물체 탐지에서 무의미함 , 사용 안함 `True Negative (TN)`



---



### ROC 
|![](https://i.imgur.com/UJAOjp8.png)|![](https://scikit-learn.org/stable/_images/sphx_glr_plot_roc_001.png)|
|-|-|

- X축 : Specificity = TN / TN+FP
- Y축 : Sensitive (Recall) = (TP) / P
- 모델 선별 기준 : 파란선(x-y)보다 위쪽에 있는 경우 
	- 왼쪽 모서리에 가까우면 좋음 

>  AUC : ROC는 그래프라 수치화 못함, AUC그래프의 아래 면적값을 계산 하여 수치화 (1에 가까우면 좋음)  
---


## PR(Precision Recall) 그래프 

- ROC 와 유사
- 주로 데이타 라벨의 분포가 심하게 불균등 할때 사용
- 모델 선별 기준 : 베이스라인(=P/P+N) 보다 위쪽에 있는 경우
	- P는 데이타에서 Positive 레이블의 수, N 은 전체 데이타의 수  
	- 그래프가 위로 갈수록 정확도가 높은 모델 

|![](https://i.imgur.com/7QmnbQf.png)|![](https://i.imgur.com/9mRWgCj.png)|
|-|-|
-   X축 : Sensitive (Recall) = (TP) / P  
-   Y축 : Precision = TP / (TP+FP)
    


### PR 그래프로 AP(Average Precision)계산 하기 

Precision과 Recall은 반비례 관계를 갖기 때문에 Object Detection에서는 Average Precision, 이하 **AP** 라는 지표를 주로 사용합니다.
- Precision과 Recall로 그래프 생성 
- Recall을 0부터 0.1 단위로 증가 (1까지, 총 11개)
- 각 단위 마다 Precision 값을 계산하여 평균 도출 
	- 즉 11가지의 Recall 값에 따른 Precision 값들의 평균이 AP를 의미
	- 하나의 Class(개, 고양이) 마다 고유의 AP 값을 계산할 수 있습니다.

### AP에서 mAP (mean Average Precision)계산하기 

- 단순히 오른쪽 각 Class마다의 AP값의 평균을 내어 왼쪽 mAP에 기입한것  [[조대협의 블로그]](https://bcho.tistory.com/1206)

![](https://i.imgur.com/eFMxqgv.png)

---


### F-1 Score 
- Precision과 Recall의 조화평균입니다. `큰 비중이 끼치는 bias가 줄어든다`
- 2*[(Precision * Recall) / (Precision + Recall)  ]
- label이 불균형 구조일 때, 모델의 성능을 정확하게 평가


---
[https://github.com/adioshun/gitBook_Semantic_Segmentation/blob/master/ref01evaluation-map.md](https://github.com/adioshun/gitBook_Semantic_Segmentation/blob/master/ref01evaluation-map.md)
