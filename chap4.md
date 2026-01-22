# Generative learning algorithms

logistic regression learning algorithm은 p(y|x)를 training하는 과정이었다면,

generative learning algorithm은 p(x|y)를 training하는 과정이다. (y:class, x:feature)

예시) 코끼리와 개를 구별하는 상황에서, 코끼리와 개를 구별짓는 line(decision boundary)을 찾는 것이 목적이었다. 새 동물에 대해 line 기준 어디에 떨어지는 지를 통해 prediction을 하였다.

이제는 코끼리를 들여다보고, 개를 들여다본 후, 코끼리와 개가 어떻게 생겼는지에 대한 각각의 모델을 만들고, new animal에 대해 두 동물 중 어디에 더 가깝게 생겼는지를 매칭한다.

위의 예시(such as perceptron)는 discriminative learning algorithms, 아래 예시는 generative learning algorithms라고 한다.

우리는 p(x|y)를 찾기 위해 Bayes 정리를 이용할 것이다.

Bayes Rule: p(y|x)=p(x|y)p(y)/p(x)

우리는 분모 p(x)를 계산할 필요는 없다. argmax(y) p(y|x)= argmax(y) p(x|y)p(y)와 같다. (p(x)는 상수이기 때문)

Gaussian discriminant analysis(GDA)
---
이진 분류 문제에 GDA 모델을 사용해보자.

GDA 모델에서는 p(x|y)가 multivariate normal distribution을 따른다고 가정한다.

y~Bernoulli, p(x|y=0)~N(mu0,cov matrix), p(x|y=1)~N(mu1, cov matrix) 여기서 parameter는 베르누이 확률 o(쉽게표기하겠음), mu0, mu1, cov matrix 총 4개이다.

4개 parameter에 대한 log likelihood는 다음과 같다.

log pi(x(i),y(i)) = log pi(x(i)|y(i))p(y(i)) 여기서 joint를 조건부 확률로 쪼개서 표현, pi는 모든항에 대한 곱셈 기호 파이를 의미(기호없어서 대체함)

Discussion: GDA and logistic regression
---
GDA는 p(x|y=0), p(x|y=1) 모두 다변량정규분포를 따라야하고 parameter가 o, mu0, mu1, cov matrix 총 4개로 strong assumption을 가진다. 그로 인한 장점은 내 데이터(p(x|y))가 정규분포를 따를 땐 strong assumption에 의해 더 높은 performance를 보인다. 반면에, logistic regression은 데이터가 정규분포를 따르지 않아도 된다는 장점이 있지만 성능이 GDA보다는 다소 떨어진다는 단점이 존재한다. 내가 따르는 데이터의 분포를 확신할 수 없을 경우엔 distribution에 robust한 logistic regression을 택하는 것이 권장된다. GDA->logistic 따름은 맞지만, logistic->GDA 따름은 틀린 말이다. GDA는 poisson 등 exp fam에도 일반화 가능하다. 또한 softmax같은 multi class 분류 문제에도 위의 말들이 성립한다.

*추가로 알아두면 좋은 점은, 데이터가 방대할 수록 모델을 설계하는 데 필요한 기술적인 부분이 큰 성능 차이를 내지 못한다.(분포가 가우시안이냐, 포아송이냐 등 어떤 분포를 선택할 지, 직관을 통해 좋은 모델을 설계할지 등) 다만, 데이터가 몇백만개, 몇억개가 아니고 수십개, 수백개 단위일 경우 분포 선택과 모델 설계에 대한 skill이 성능을 크게 좌우한다.

Naive bayes
---
Naive bayes를 text classification 문제 중 하나인 classifying email 문제를 통해 알아볼 것이다.

우선 feature vector x를 정의한다. 이메일 데이터에서 자주 쓰이는 상위 10,000개의 단어리스트를 준비하고, x 벡터에 그 단어가 있을 경우 1, 없을 경우 0으로 설정한다. 이때, possible outcome은 2^10000개, parameter 수는 2^10000-1개 이므로 모델이 작동하지 않을 것이다. 따라서 우리는 Naive Bayes를 통해 이러한 문제를 해결한다.

우선, Naive Bayes assumption에 대해 알아본다.

이는 x_i's are conditionally indepenent given y 라는 가정이다.

의미를 설명해보면, y(스팸인지 아닌지)를 알면 등장하는 x1은 x7과 독립적이라는 것이다. 수학적으로 엄밀하지 않고, 틀렸지만 결과적으로 horrible하지 않기 때문에 이와 같은 가정을 사용한다.

따라서 p(x1,x2, ... , x10000|y)=p(x1|y)p(x2|y,x1)p(x3|y,x1,x2)... = p(x1|y)p(x2|y)p(x3|y)... 이다.

우리는 joint likelihood를 다음과 같이 쓸 수 있다.

L=products of p(x(i),y(i)) 여기서 product는 각각에 대해 모두 곱하는 pi이다.

우리는 maximum liklihood estimation을 통해 모든 파라미터에 대한 편미분을 진행하여 phi_j|y=1, phi_j|y=0, phi_y를 구할 수 있다.

그 결과중 하나를 예를 들어보면, phi_j|y=1은 y=1(스팸)인 메일들 중 j라는 단어가 포함되어 있는 메일의 비율을 의미한다.

Logistic regression으로도 동일한 분류 문제를 해결할 수 있지만,

MLE를 통해 구한 parameter의 결과가 단순한 counting, 상수들의 곱으로만 이루어져있다는 점에서 굉장히 효율적인 모델임을 알 수 있다.
