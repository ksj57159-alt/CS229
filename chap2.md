## Classification and logistic regression

Logistic Regression:
---
기존 linear regression h(x) form에서 결과가 {0,1}로 나오게 하기 위해 구조를 변경한다

h_θ(x)=g(θ^Tx)로, g는 sigmoid function(logistic funtion)이다.

g'=g(1-g)를 이용해서 log likelihood를 구하면 sum y(logh)+(1-y)log(1-h)이고, maximize likelihood estimation을 이용해서 log likelihood의 gradient를 구하고, likelihood를 최대화하기 위해 θ를 그 gradient로 update한다. (log likelihood를 업데이트하는 방식은 결과적으로 앞에서 봤던 linear regression의 loss를 최소화하기 위해 업데이트하는 방식과 수식적으로 같음을 알 수 있다. losgistic regression에서는 +부호, ascent로 부르기만 하는 것일 뿐)

Multi-class classification:
---
θ^Tx를 양수로 만들기 위해 exp를 취해주고, 확률화(sum으로 나눠주기)를 한다. 최종적으로는 확률 결과가 (0,1,0)으로 나오길 원한다. (3개의 class 상황으로 가정하면)

(0,1,0)과 같은 결과를 만든다는 것은 cross entropy 최소화와 같은 말이다.cross entropy(=negative log likelihood, =loss function 아마)

softmax function은 k개(차원)의 input을 다시 k개(차원)의 output(이때 output은 kx1의 column vector 인듯)으로 반환해주고, 각 값은 확률이다.

Newton's method:
---
f(θ)=0이 되는 지점을 찾고 싶을 때 쓰는 방법

θ := θ-f/f' 이고, 여기에 f 대신 l'(θ)로 생각하면 l'(θ)=0이 되는 지점을 찾는 것과 같다.

따라서 θ :=θ-l'/l''이고, vector valued losgistic regression setting으로 바꾸면 θ := H^(-1)▽l(θ)이다. (H:Hessian)
