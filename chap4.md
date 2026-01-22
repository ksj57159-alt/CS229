# Generative learning algorithms

logistic regression learning algorithm은 p(y|x)를 training하는 과정이었다면,

generative learning algorithm은 p(x|y)를 training하는 과정이다. (y:class, x:feature)

예시) 코끼리와 개를 구별하는 상황에서, 코끼리와 개를 구별짓는 line(decision boundary)을 찾는 것이 목적이었다. 새 동물에 대해 line 기준 어디에 떨어지는 지를 통해 prediction을 하였다.

이제는 코끼리를 들여다보고, 개를 들여다본 후, 코끼리와 개가 어떻게 생겼는지에 대한 각각의 모델을 만들고, new animal에 대해 두 동물 중 어디에 더 가깝게 생겼는지를 매칭한다.

위의 예시(such as perceptron)는 discriminative learning algorithms, 아래 예시는 generative learning algorithms라고 한다.

우리는 p(x|y)를 찾기 위해 Bayes 정리를 이용할 것이다.

Bayes Rule: p(y|x)=p(x|y)p(y)/p(x)

우리는 분모 p(x)를 계산할 필요는 없다. argmax(y) p(y|x)= argmax(y) p(x|y)p(y)와 같기 때문이다. 

Gaussian discriminant analysis(GDA)
---
이진 분류 문제에 GDA 모델을 사용해보자.

GDA 모델에서는 p(x|y)가 multivariate normal distribution을 따른다고 가정한다.

y~Bernoulli, p(x|y=0)~N(mu0,cov matrix), p(x|y=1)~N(mu1, cov matrix) 여기서 parameter는 베르누이 확률 o(쉽게표기하겠음), mu0, mu1, cov matrix 총 4개이다.

4개 parameter에 대한 log likelihood는 다음과 같다.

log pi(x(i),y(i)) = log pi(x(i)|y(i))p(y(i)) 여기서 joint를 조건부 확률로 쪼개서 표현, pi는 모든항에 대한 곱셈 기호 파이를 의미(기호없어서 대체함)

Discussion: GDA and logistic regression
---
