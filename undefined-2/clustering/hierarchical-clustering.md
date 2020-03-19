# Hierarchical Clustering

## 1.   Introduction

계측적 군집화는 비 지도 학습 알고리즘 이다.

클러스터의 수를 사전에 정의할 필요 없다.

결과물로 `dendrogram`라는 트리 다이어그램을 생성한다.

## 2.   Key Terms

cluster : 유사도기반으로 모여진 점들

Cluster Centroid : 클러스터의 평균\(mean\)

Distance measure : 거리 측정 척도 \(Manhattan or L1, Euclidian or L2 distances, etc.\)

linkage criteria : 거리계산에 사용된 위치

* Single Linkage - 가장 가까운 것에서 계산 `distance is computed between the two MOST similar parts of clusters (two closest points).`
  * Single linkage suffers from chaining meaning that clusters can be too spread out, and not compact enough.
* Complete Linkage - 가장 먼곳에서 계산 `distance is computed between the two LEAST similar parts of clusters (two most distant points).`
  * Complete linkage avoids chaining but suffers from crowding meaning that Clusters are compact, but not far enough apart.
* Average Linkage - 중앙에서 부터 계산 `distance is computed between clusters’ centroids.`
  * This is a balanced approach: clusters tend to be relatively compact and relatively far apart.

![](https://i.imgur.com/HYvDuss.png)

## 3.   Data Representation and Preparation

