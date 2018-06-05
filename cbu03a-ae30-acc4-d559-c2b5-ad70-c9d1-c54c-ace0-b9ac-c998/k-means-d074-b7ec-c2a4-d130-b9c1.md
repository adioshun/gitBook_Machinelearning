## 3. K-근접이웃 알고리즘 

> 참고 : [처음배우는 머신러닝](https://books.google.co.kr/books?id=RQM5DwAAQBAJ&printsec=frontcover&hl=ko#v=onepage&q&f=false) : 미리보기 150page



### 3.1 개요
- 초반에는 (입력, 결과)가 있는 데이터들을 저장하고 있음 
- 새로운 입력에 대한 결과를 추정할 때 결과를 아는 최근접한 k개의 데이터에 대한 결과정보를 이용하는 방법

단점
- 학습단계에서는 실질적인 학습이 일어나지 않고 데이터만 저장 후 새로운 데이터가 주어지면 저장된 데이터를 이용하여 학습 
    - 학습데이터가 크면 메모리 문제
    - 게으른 학습(lazy learning
    - 시간이 많이 걸릴 수 있음
    
### 3.2 알고리즘 

###### Step 1. 질의(query)와 데이터간의 거리 계산

수치 데이터
- 유클리디언 거리(Euclidian distance) 
- 응용분야의 특성에 맞춰 개발

범주형 데이터
- 응용분야의 특성에 맞춰 개발

###### Step 2. 효율적으로 근접이웃 탐색

- 색인(indexing) 자료구조 사용: R-트리, k-d 트리 등

- 문제점 : 데이터의 개수가 많아지면 계산시간 증가 문제

###### Step 3. 근접 이웃 k개로 부터 결과를 추정

- 분류
    - 다수결 투표(majority voting) : 개수가 많은 범주 선택

- 회귀분석
    - 평균 : 최근접 k개의 평균값
    - 가중합(weighted sum) : 거리에 반비례하는 가중치 사용


---




### K-mean 클러스터링 

- 정의 : 같은 클러스터에 속하는 데이터들의 inner similarity를 증가시키는 방향으로 클러스터를 형성 

- 가정 : 데이터가 유클리디안 공간위에 있어야 한다 (평균을 구할수 있도록, 실수의 좌표값을 가져야 한다. )

- 동작 과정 
	1. k값을초기값으로먼저받고, 데이터를k개의초기군집으로나눔.
	2. k개의초기군집의centroid(중심점)을설정함.
	3. 각데이터개체와현재군집중심점(centroid)사이의거리를구함.
	4. 만약개체가현재군집평균에가까우면현재소속군집에포함.
	5. 그렇지않으면다른군집으로재할당.
	6. 개별군집의평균이다시계산되어, 클러스터의중심점(centroid)를다시계산.
	7. 반복하면서클러스터가더이상재지정되는점이없으면마침.

![image](https://user-images.githubusercontent.com/17797922/40976552-51ecafb4-6883-11e8-959c-8eb62d62bd57.png)

```
첫번째 그림과 같은 대상들에서(1번) 
랜덤하게 중심점을 잡습니다.
그림에 파란 동그라미와 빨간 동그라미가 중심점이 됩니다.
(2번)
그 중심점 외에 다른 점들과 두 중심점의 거리를 각각 계산하여(3번)
더 가까운 중심점과 군집을 이룹니다.(4번, 5번)
각 군집에서 대상들 사이의 평균점을 계산하여 중심점을
다시 지정해 줍니다.
그 중심점을 기준으로 다시 군집화 해 줍니다.(6번)
그렇게 계속 반복하여 군집이 변하지 않는다면 군집화가 완성됩니다.(7번)
```

장점(Strength)
- Simple, easy to implement and debug
- Intuitive objective function : optimize intra-cluster similarity
- Relatively efficient : 𝑂(𝑡𝑘𝑛), where 𝑛 is number of objects, 𝑘 is number of clusters and 𝑛 is number of iterations. Normally, 𝑘, 𝑡 ≪ 𝑛.

단점(Weakness)
- Applicable only when mean is defined. → k-medoids
- Often terminates at a local optimum. Initialization is important.
	-  Not suitable to discover clusters with non-convex shapes
- Need to specify 𝐾, the number of clusters, in advance.
- Unable to handle noisy data and outliers → k-medoids

요점(Summary)
- Assign members based on current centers
- Re-estimate centers based on current assignment