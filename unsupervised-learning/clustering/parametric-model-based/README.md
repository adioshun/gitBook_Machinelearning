# Parametric-Model-based

정의 : 두개의 오프젝트 사이의 similarity를 측정하기 위해서 두 오브젝트 사이의 거리\(distance, dissimilarity\)를 측정

## 

## 1.0 유사도 계산

분류

* 민코스키 거리 : 벡터 공간 안의 두점 사이의
* 마하라노비스 거리 : 점들의 분호를 고려한 거리

#### A. 민코스키 거리

$$d(X,Y) = \sqrt[p]{\sum^M_{i=1} \mid x_i -y_i \mid ^p}$$

p=1 : 맨하탄\(=L1\) : \(실질적으로\) x축으로 이동 거리, y축으로 이동 거리, 보라색 p=2 : 유클리드\(=L2\) 거리 : \(우리가 일반적으로 아는\) 두 점사이의 직선 거리, 초록색

#### B. 마할라노비스 거리

$$d(X,Y) = \sqrt{(x_i - y_i)^r S^{-1}(x_i - y_i)}$$

두점 사이의 거리를 계산할때 데이터의 분포를 고려하는 거리

두 좌표값의 단위가 다른\(키 & 몸무게\)경우 각 축간의 공분산을 고려

* 공분산 고려 = X값의 증감과 Y값의 증감의 관계를 거리에계산에 넣기

공분산 : 두 변수가 얼마나 연관성이 있는지 나타내는 값,

$$Cov(X,Y) = E \left[(X-\mu_x)(Y-\mu_y) \right] , \mu = 평균$$

\[Distance function 과 Similarity function의 예\]

| ![image](https://user-images.githubusercontent.com/17797922/40976309-9a69c00c-6882-11e8-8dd3-bc4b3846834f.png) | ![image](https://user-images.githubusercontent.com/17797922/40976327-aedac18a-6882-11e8-8f83-6690531e52cd.png) | ![image](https://user-images.githubusercontent.com/17797922/40978071-87854ef2-6887-11e8-9785-27911ef9936e.png) |
| :--- | :--- | :--- |


> [clustering valuation\(군집 모델 평가하기\)](http://woolulu.tistory.com/50): ARI, NMI

### 1.1 분류

* 중심 기반 군집화 : 클러스터를 클러스터 중심점으로 정의하는 기법
* 계측적 군집화 : 클러스터의 크기에 따라 클러스터의 계층을 정의하고 계층의 상하위를 이용하는 기법
* 밀도 기반 군집화 : 클러스터를 데이터가 높은 밀도로 모여 있는 공간으로 보는 기법

> EM 알고리즘\( Expectation Maximization\)은 어디에 속하나??

#### A. 중심 기반 군집화

**가. K-중심 군집화 \(k-centroid, k-medoid\)**

클러스터 중심점을 정한 후 가까운것 데이터들을 모아가며 클러스터를 확장

분류 : 중심값을 구하는 방법에 따라

* k-mean\(평균\) 군집화
* k-median\(대푯값\) 군집화
* k-mode\(최빈값\) 군집화

#### B. 계측적 군집화

최상의 계층 클러스터 : 모든 데이터를 포함하는 하나의 클러스터 최하의 계층 클러스터 : 단 하나의 데이터만을 포함하는 데이터 수만큼의 클러스터

분류

* 하향식 : 분할적 군집화
* DIANA\(Divisive Analysis\)
* 상향식 : 집괴적 군집화

특징

* 클러스터 수를 지정할 필요가 없음

동작 과정 1. 하나의 데이터를 하나의 클러스터로 지정 2. 과정 1의 클러스터들에 대해 가장 유사도가 높은 클러스터 둘을 하나로 합침 3. 과정 2에서 생성된된 클러스터들에 대해 다시 같은 과정을 반복

클러스터를 합치는 방법 : 클러스터간의 유사도 측정

* 단일 연결법 : 가장 짧은 거리를 클러스터 사이의 거리로 간주
* 완전 연결법 : 가장 먼 거리를 클러스터 사이의 거리로 간주
* 평균 연결법 : 데이터 들의 거리 평균을 클러스터 사이의 거리로 간주

#### C. 밀도 기반 군집화

데이터 밀도가 높아지는 방향으로 데이터를 군집화 하는 방식

**가. 평균이동 군집화**

동작 과정

1. 임의의 초기 중심점 지정, 탐색 반경 지정
2. 지정한 중심점에서 지정된 탐색 반경의 밀집도 계산
3. 밀집도 높은 쪽으로 중심점 재 지정
4. 반복

> 중심점을 이동한다는 측면에서 일부에서는 `중심기반 군집화`로 분류 하기도 함

**나. DBSCAN**

TBD

My best guess from your description is that you have 100 data streams, all providing x,y,z data from different sources? What do you mean by 'cluster them'? Do you mean group data with similar x,y,x values? Or do want similar x,y,z values at a 'similar time' - in this case it is simply 4D data, time is just another dimension. Also, do you want hyper-elliptical clusters, or arbitary shapes of connected similairty? Considerations: You first have to consider what you mean by 'cluster'? What do you define as a cluster? You then have to consider how many clusters you want? A fixed number, or an appropriate number based on the data spread or clusters of fixed sizes? You then have to consider the importance of outliers - do you want to force them into the nearest custer, discard them or are they actually the most important data points? Then consider when you want to cluster? Offline after data collection, on-line during data collection or at discreet time intervals? If on-line how do you want the clusters to behave? To grow, move and be created based on all data so far or to fully evolve and allow clusters that are no longer receiving data to 'fade and die out'. Depending on your answers to these questions different techniques are more appropriate, e.g.

```text
Hierarchical - not really any use for anything except small, offline data sets as it takes waaaay too much memory
Subtractive - offline, finds an appropriate number of clusters, but slow
k-means - only useful if you have a fixed number of clusters and don't mind data being forced into clusters it doesn't belong in
DBScan - has a number of variants, offline will find arbitrary shaped clusters
ELM - online evolving hyper-elliptical clusters
My techniques:
DDC - very fast offline approach that will find an appropriate number of clusters
DDCAR - very fast offline and will find appropriate clusters with no user input whatsoever but is limited to hyper-spherical clusters
DDCAS - DDC adapted for arbitrary shaped clusters (unpublished as yet so you can't have any source code but I can run it for you)
CODAS - very fast, online and will find the required number of clusters and clusters of arbitrary shape (unpublished as yet so you can't have any source code but I can run it for you)
```

All of these are available for Matlab: hierarchical, subtractive and k-means are built in an implementation of DBScan is available online, I forget where DDC & DDCAR I have almost finished tidying up to a releasable version DDCAS & CODAS - I can run for you on test data There are also various implementations of other technqieus around including Matlab Central File Exchange

## 비교 방법

![](http://scikit-learn.org/stable/_images/sphx_glr_plot_cluster_comparison_001.png) [Comparing different clustering algorithms on toy datasets](http://scikit-learn.org/stable/auto_examples/cluster/plot_cluster_comparison.html#sphx-glr-auto-examples-cluster-plot-cluster-comparison-py)

