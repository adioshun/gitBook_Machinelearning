# Dimension-Reduction



## 1. 정의

관찰 공간 위의 샘플들에 기반으로 잠재 공간을 파악하는 것을 차원 축소\(dimensionality reduction technique\) 라고 합니다.

* 따라서 관찰 대상들을 잘 설명할 수 있는 잠재 공간\(latent space\)은 실제 관찰 공간\(observation space\)보다 작을 수 있습니다.

> 중요 : 차원축소는 단순히 데이터의 압축이나 잡음\(noise\)을 제거하는 것이 아니라는 것을 말씀드리고 싶습니다. 물론 차원축소로 데이터의 압축이나 잡음을 제거하는 효과도 있겠지만, 이것의 가장 중요한 의의는 **관측 데이터를 잘 설명할 수 있는 잠재 공간\(latent space\)을 찾는 것**입니다.

## 2. 차원 축소와 Feature extraction 관계

Feature extraction은 고차원의 원본 feature 공간을 저차원의 새로운 feature 공간으로 투영시킵니다.

새롭게 구성된 feature 공간은 보통은 원본 feature 공간의 선형 또는 비선형 결합입니다.

Feature extraction의 예로는

* Principle Component Analysis \(PCA\) \(Jolliffe, 2002\), 
* Linear Discriminant Analysis \(LDA\) \(Scholkopft and Mullert, 1999\), 
* Canonical Correlation Analysis \(CCA\) \(Hardoon et al., 2004\), 
* Singular Value Decomposition \(Golub and Van Loan, 2012\), 
* ISOMAP \(Tenenbaum et al., 2000\) and 
* Locally Linear Embedding \(LLE\) \(Roweis and Saul, 2000\)가 있습니다.
* t-sne 같은 고급 차원 축소 방법

장점 : 데이터양이 적더라도 활용 가능하다.

## 3. 공식화

### 3.1 차원 축소 표현 방법

### 3.2 정보 손실 수량화

* [차원축소와 특징선택이란 무엇인가?](http://terryum.io/korean/2016/05/05/FeatureSelection_KOR/)

