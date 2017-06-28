# Fundamentals of Machine Learning

Learn the most classical methods of machine learning
• Rule based approach
• Classical statistics approach
• Information theory appraoch

Rule based machine learning
• How to find the specialized and the generalized rules
• Why the rules are easily broken

Decision Tree
• How to create a decision tree given a training dataset
• Why the tree becomes a weak learner with a new dataset

Linear Regression
• How to infer a parameter set from a training dataset
• Why the feature engineering has its limit

## 1. Rule based machine learning

### 1.1 Find-S algorithm 
![](http://i.imgur.com/XGPSCx8.png)

- Candidate elimination algro.

- 문제점 : "we	don’t	live	in	the	perfect	world"


## 2. Decision	Tree

통계 기법 활용 학습 방법 

![](http://i.imgur.com/RJ6TTK3.png)

### 2.1 Entropy 
- Random Variable이 얼마나 불확실성이 높은지/낮은지 평가 하는 지표 
- Higher	entropy	means	more	uncertainty
- 공식 : $$H(X) = - \sum_x P(X=x)\log_b P(X=x)$$
    - $$ \sum_x$$ 의 x는 동전던지기는 F,T/ 주사위는 1~6 을 의미, Discrete한 경우 
    - 만일 Continuos한 경우는 $$\sum \rightarrow \int $$ 적분으로 변환하여 처리 


- Conditional	Entropy
    - We are interested in the	entropy	of	the	class	given	a	feature	variable
    - Need	to	introduce	a	given	condition	in	the	entropy
    - 일반적으로  Conditional	Entropy가 적용되는 경우가 많음 
    - 공식 : $$ H(Y|X) = \sum_x P(X=x) H(Y|X =x) = \sum_x P(X=x)\{-\sum_y P(Y=y|X=x) \log_b P(Y=y|X=x\}   $$ 
