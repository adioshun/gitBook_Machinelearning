# Clustering

## 접근 방법

> \[A Semi-Supervised Approach for Kernel-Based Temporal Clustering\]\([https://www.semanticscholar.org/paper/A-Semi-Supervised-Approach-for-Kernel-Based-Araujo/51796da9284df8eae3a9ab6f2731f27fa8900095](https://www.semanticscholar.org/paper/A-Semi-Supervised-Approach-for-Kernel-Based-Araujo/51796da9284df8eae3a9ab6f2731f27fa8900095)\)

![](../../.gitbook/assets/image%20%281%29.png)

### 

### \*\*\*\*

### **매개변수 모델 기반 방식\(Parametric Model-based\) :**

1.  주어진 데이터를 가지고 임의의 그룹 중심점을 찾은 다음 반복적으로 그룹의 중심점을 찾아가는 과정
2. 서로 가까이 있는 대상은 같은 그룹으로 묶이고, 그 그룹의 핵을 중심으로 같은 그룹에 포함된 대상들이 밀집되어 분포하도록 하는 방식입니다. 
3. 주로 두 대상간의 거리 \( 유클리드 거리 등 \) 가 대상간의 유사도를 측정하는 척도로 사용됩니다. 
4. K-Means 알고리즘이 이 분류의 알고리즘에 속합니다.

 거리상으로 떨어져있는 2개의 그룹이 존재한다고 하였을 때 임의의 중심점 2개를 잡은 후 해당 점에서 가까운 데이터들을 그룹으로 만든 후 새로 만들어진 그룹 내의 중심점을 잡고, 다시 만든 중심점에서 가까운 데이터들을 그룹으로 만드는 방식을 반복하다 보면 위의 그림과 같이 한 점으로 수렴하게 됩니다. 

단점 : 결과가 항상 일정하지 않으며 가끔씩 잘못된 그룹으로 분류되는 경우가 발생할 수 있다는 점입니다.



### 그래프 기반 방식\(Graph-based\)

서로 연결되어 있거나 바로 옆에 있는 대상이 같은 그룹으로 묶입니다. 

두 대상의 거리가 매우 가깝더라도 대상이 연결되어 있지 않다면 같은 그룹으로 묶이지 않습니다. 

Spectral Clustering 알고리즘이 이 방법을 사용한 클러스터링 알고리즘에 해당합니다.

* Minimum cut
* Normalized cut

그래프 기반 방식은 각 데이터의 점들과 다른 점 사이에 선을 긋고 두 데이터 사이의 유사도에 따라 비중을 부여하는 방식입니다. 그래프 기반 방식에 따르면 두 데이터의 유사점이 많으면 비중을 키우고, 유사점이 낮으면 비중을 낮추는 식으로 하여 이를 기준으로 별개의 그룹으로 나누는 방식입니다.

장점 : 결과값이 거의 일정하게 나온다

