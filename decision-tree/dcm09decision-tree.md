# dcm09\_Decision\_tree

어느 자질에 대해 나눌것인지 판단 = 정보이득\(IG\)이용

$$IG(X,Y)= E(Y)- \sum_{x \in X} \frac{|x|}{|X|}E(x) = E(y) - E(y|x)$$

* E\(y\)=Entropy = 불확실성 정도 = y에 대한 정보를 나타내기 위해 평균적으로 알아야 할 Bit갯수 
* X = 모든 Attribute에 해당하는 set
* x = 하나의 Attribute에 해당하는 subset
* Y = label에 해당하는 set
* $$\frac{|x|}{|X|}$$는 P\(X=x\)로 정의 된다. 
* $$\sum\frac{|x|}{|X|}E(x)$$ = E\(x\)의 예상값\(expected value\)
  * 각각의 label, 그리고 x라는 자질에 대한 subset으로 나눈 후 평균적인 Entropy
  * 즉, E\(y\|x\) Conditional Entropy 

## ID3

## 배깅

## 부스팅

## Random Forest

## Pruning

