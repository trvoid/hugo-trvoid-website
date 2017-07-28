---
Title: "ML02 - 선형 회귀"
---

## 1 소개

회귀 분석 과정을 다음 세 단계로 간단하게 정리할 수 있습니다.

1. 훈련 데이터 세트 (x, y)를 준비합니다. 여기서 x는 독립 변수, y는 종속 변수입니다.
1. 훈련 데이터 세트를 표현할 수 있는 모델을 만들고 가장 근접한 결과를 보여 주는 파라미터를 찾습니다. 
1. 새로운 데이터의 x값이 주어질 때  앞에서 얻은 모델을 사용하여 y값을 예측합니다.

모델을 만들 때 종속 변수 y를 독립 변수 x의 일차식으로 표현하면 이를 **선형 회귀**라고 말합니다. 그리고 x가 하나의 변수이면 **일변량 선형 회귀**, 둘 이상의 변수이면 **다변량 선형 회귀**라고 합니다.

이 문서를 작성하면서 사용하는 주요 용어들은 다음과 같습니다.

* hypothesis - 모델을 나타내는 함수 식
* feature - 독립 변수 x의 개별 요소
* cost function - 훈련 데이터 세트의 종속 변수 y와 모델의 예측값의 차이를 나타내는 함수 식

## 2 일변량 선형 회귀

### 2.1 Hypothesis와 cost function

훈련 데이터의 feature가 한 개일 때 hypothesis는 다음과 같이 표현할 수 있습니다. 

<div>$$ { h }_{ \theta  }(x)={ \theta  }_{ 0 }+{ \theta  }_{ 1 }{ x }_{ 1 } $$</div>

위의 식에서 \\(x\\)는 데이터의 feature들이고 \\(\theta\\)는 찾고자 하는 파라미터들입니다. \\(x_0=1\\)라고 하면 위의 식을 다음과 같은 형태로 표현할 수 있습니다.

<div>$$ h_\theta(x)=x^T\cdot\theta $$</div>
<div>$$ x=(x_0,x_1), \theta=(\theta_0,\theta_1) $$</div>

데이터의 개수가 \\(m\\)일 때 cost function은 다음과 같이 표현할 수 있습니다. \\(y\\)는 데이터의 결과값이고 \\((i)\\)는 \\(i\\)번째 데이터임을 의미합니다.

<div>$$
J(\theta )=\frac { 1 }{ 2m } \sum _{ i=1 }^{ m }{ { \left( { h }_{ \theta  }({ x }^{ (i) })-{ y }^{ (i) } \right)  }^{ 2 } } 
$$</div>

hypothesis를 대입하여 위 식을 전개하면 cost function은 각각의 파라미터에 대하여 아래로 볼록한 2차 함수가 됩니다.

<div>$$
J(\theta )=\frac { 1 }{ 2m } \sum _{ i=1 }^{ m }{ \left( { \theta  }_{ 0 }^{ 2 }+{ \theta  }_{ 1 }^{ 2 }{ x }_{ 1 }^{ (i)2 }+{ y }_{  }^{ (i)2 }+2{ \theta  }_{ 0 }{ \theta  }_{ 1 }{ x }_{ 1 }^{ (i) }-2{ \theta  }_{ 1 }{ x }_{ 1 }^{ (i) }{ y }_{  }^{ (i) }-2{ y }_{  }^{ (i) }{ \theta  }_{ 0 } \right) } 
$$</div>

이 cost function이 최소값을 가지도록 하는 파라미터 \\(\theta\\)를 찾는 방법은 **3 다변량 선형 회귀** 단원에서 다루겠습니다.

## 3 다변량 선형 회귀

### 3.1 Hypothesis와 cost function

훈련 데이터의 feature가 \\(n\\)개일 때 hypothesis는 다음과 같이 표현할 수 있습니다. \\(x\\)는 데이터의 feature들이고 \\(\theta\\)는 찾고자 하는 파라미터들입니다.

<div>$$
{ h }_{ \theta  }(x)={ \theta  }_{ 0 }+{ \theta  }_{ 1 }{ x }_{ 1 }+{ \theta  }_{ 2 }{ x }_{ 2 }+\cdots +{ \theta  }_{ n }{ x }_{ n }
$$</div>

데이터의 개수가 \\(m\\)일 때 cost function은 다음과 같이 표현할 수 있습니다. \\(y\\)는 데이터의 결과값이고 \\((i)\\)는 \\(i\\)번째 데이터임을 의미합니다.

<div>$$
J(\theta )=\frac { 1 }{ 2m } \sum _{ i=1 }^{ m }{ { \left( { h }_{ \theta  }({ x }^{ (i) })-{ y }^{ (i) } \right)  }^{ 2 } } 
$$</div>

### 3.2 Gradient descent

cost function의 편미분을 사용하여 cost를 최소화하는 파라미터 $\theta$를 찾을 수 있습니다. 다음은 gradient descent 방식을 나타내는 알고리즘입니다.

<div>$$
repeat \quad \{ \quad \quad \quad \quad \quad \quad \quad \quad\\

{ \theta  }_{ j }:={ \theta  }_{ j }-\alpha \frac { \partial J(\theta ) }{ \partial { \theta  }_{ j } } \\

\} \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad \quad
$$</div>

<div>$$
\frac { \partial J(\theta ) }{ \partial { \theta  }_{ j } } =\frac { 1 }{ m } \sum _{ i=1 }^{ m }{ \left( { h }_{ \theta  }({ x }^{ (i) })-{ y }^{ (i) } \right) { { x }_{ j } }^{ (i) } } 
$$</div>

위의 식에서 $\alpha$는 학습률(learning rate)입니다.

### 3.3 방정식의 해

아래로 볼록한 함수의 경우 기울기가 $0$일 때 최소값을 가지므로 다음 방정식을 풀어서 cost를 최소가 되게 하는 $\theta$를 구할 수도 있습니다.

<div>$$
\frac { \partial J(\theta ) }{ \partial { \theta  }_{ j } } =\frac { 1 }{ m } \sum _{ i=1 }^{ m }{ \left( { h }_{ \theta  }({ x }^{ (i) })-{ y }^{ (i) } \right) { { x }_{ j } }^{ (i) } } = 0
$$</div>

위 방정식을 $\theta$에 대해서 풀면 아래의 결과를 얻습니다.

<div>$$
\theta ={ \left( { X }^{ T }\cdot X \right)  }^{ -1 }\cdot { X }^{ T }\cdot y
$$</div>

여기서 $X$와 $y$는 다음과 같습니다.

<div>$$
X=\begin{bmatrix} { x }_{ 0 }^{ (1) } & { x }_{ 1 }^{ (1) } & { x }_{ 2 }^{ (1) } & \cdots  \\ { x }_{ 0 }^{ (2) } & { x }_{ 1 }^{ (2) } & { x }_{ 2 }^{ (2) } & \cdots  \\ { x }_{ 0 }^{ (3) } & { x }_{ 1 }^{ (3) } & { x }_{ 2 }^{ (3) } & \cdots  \\ \vdots  & \vdots  & \vdots  & \ddots  \end{bmatrix}, \quad
y=\begin{bmatrix} { y }^{ (1) } \\ { y }^{ (2) } \\ { y }^{ (3) } \\ \vdots  \end{bmatrix}
$$</div>

하지만 이 방식은 몇 가지 단점을 가지고 있습니다.

* 행렬 ${ { X }^{ T }\cdot X }$에 대한 역행렬이 존재하지 않을 수도 있습니다.
* $n$이 커짐에 따라 계산 비용이 gradient descent 방식보다 빠른 속도로 증가합니다.
