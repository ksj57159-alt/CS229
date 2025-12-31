# Chapter 1 Linear Regression

Linear regression:
---
h(x): hypothesis, h(x)=θ^Tx

J(θ): cost function, h(x)-y의 "제곱"합x1/2 (실제 값과의 차이)

LMS algorithm(Least Mean Square):
---
J(θ)를 minimize하는 θ를 찾는다->목적

Gradient descent: initial θ에서 learning rate(알파)와 J(θ)의 미분값의 곱을 step마다 빼주는 방식

convergence까지 반복함. data example이 n개 있을 때, batch gradient descent라고 부름.

Stochastic gradient descent: Loop를 통해 convergence하진 않지만 near한 θ값을 정할 수 있는 방식

쓰는 이유? data의 크기가 너무 클 경우 batch 방식은 θ를 새로 구하기 위해서는 data를 모두 훑는 데 expensive하기 때문에 loop를 통해 θ를 update하는 방식을 쓴다.

The normal equations:
---
design matrix를 이용하여 J(θ)를 미분하여 0이되는 지점의 θ를 한 번에 찾는 것(step by step의 descent 방식이 아니라)

어차피 J(θ)는 전역 최적해(global minimum) 하나만 가지기 때문. (local optimum에 대한 부담 X)

Probabilistic interpretation, MLE:
---
y=θ^Tx+e (e: error) 일때, e는 정규분포를 따르고 IID하다고 가정하면 probability of y given x(x is paramiterized by θ)는 똑같이 평균만 더해진(θ^Tx) 정규분포를 따른다.

이를 통해, data는 고정이고(x가 given되니까) θ가 vary할 때의 likelihood function을 정의한다. -> L(θ)

여기에 log를 씌운 것은 l(θ)이고, 우리는 likelihood가 최대화되는 θ를 찾는 것이 목적이므로 maximize l(θ).

이는 minimize cost function과 같아진다.(minimize h(x))

이를 Maximum Likelihood Estimation (MLE)라고 부른다.

Locally weighted linear regression:
---
: 추정하고자 하는 x 값 주위에 가까운 애들에게 가중치를 높게 부여하여 regression하는 방식. bandwidth(타우)로 weight function의 너비를 조절한다.


