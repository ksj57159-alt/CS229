# Generalized linear Model(GLM)

The exponential family
---
p(y;η) = b(y)exp(η^T*T(y)-a(η))의 형태일 때 우리는 class의 분포가 exponential family에 속해 있다고 말한다. 

(여기서 y는 data, η는 natrual parameter 또는 canonical parameter, T(y)는 sufficient statistic, a(η)는 log partition function)

예를 들어, Bernoulli distribution은 p^y(1-p)^(1-y)인데, exp(log())를 취해주어 형태를 바꿔줄 수 있다.

exp((log(p/1-p)y+log(1-p))로 바뀌고, 여기서 b(y)=1, η=log(p/1-p), T(y)=y, a(η)=log(1-p)로 생각할 수 있다.

가우시안 분포도 이와 같이 생각할 수 있다.

Constructing GLMs
---
GLM을 구축하기 위해서는 다음 3가지 assumption을 만족해야 한다.

1. y|x;θ ~ ExponentialFamily(η)

2. h(x)=E[y|x] (우리의 목적은 x가 given되었을 때 T(y)의 기댓값을 예측하는 것이다. 대부분의 상황에서 T(y)=y이기 때문에 E[y]로 표현한 것이고, x가 given된 상황이니 E[y|x]이다.)

3. η와 x는 linear한 관계이다. η=θ^T*x (if vector-valued, 에타와 세타에는 i th가 붙을 것임)

3번째 가정은 위의 가정들보다 덜 정당화된다고 느낄 수 있는데, 가정 그 자체로 생각하기 보다는 "design choice"라고 생각하는 편이 나을 것이다.

정리하면, x를 linear model θ^T*x를 거친다. 이것은 η와 같고(가정 3) η는 exp fam의 parameter와도 같다. 해당 분포의 mean=h(x)이다. (= E[y;η] =E[y;θ^T*x])

최종 목적은 η같은 parameter가 아니라 θ를 최적화 하는 것임을 잊지 말아야 한다. max θ : log p(y(i)θ^T*x(i)) <-- log likelihood

Ordinary least squares
---
ordinary least squares는 GLM family model의 special case로, target variable(response variable) y가 continous, and y|x ~ Gaussian으로 모델링 하는 경우이다.

h_θ(x)=E[y|x;θ]=mu(gaussian)=η=θ^T*x (2번 가정, Gaussian 따른다는 사실, exp fam, 3번가정 순으로 등식이 완성됨)

Logistic Regression
---
Logistic regression도 GLM으로 표현된다. 우선, binary classification이기 때문에 y={0,1}을 고려한다. 따라서 binary value는 베르누이 분포를 선택하는 것이 자연스럽고,

h(x)를 GLM 가정으로 연결지을 경우 1/(1+e^-(θ^T*x))로 귀결된다. 이는 sigmoid와 같음을 알 수 있다.


