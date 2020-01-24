---
layout: post
title: Chap4 - Neural Network Training
image: img/callum-shaw-555357-unsplash.jpg
author: 0verc10ck
date: 2020-01-08T10:00:00.000Z
tags:
  - 밑바닥 부터 시작하는 딥러닝
---

이번 Chapter에서는 Chap 3에서 배운 Neural Network를 Training 하고자 한다. Machine Learning은 크게 Training과 Inference 두가지 단계로 구분된다. 

Training 단계에서는 Training data를 이용하여 최적의 Weight와 Bias 값을 얻는다.

Training 과정에서 최적의 Weight와 Bias 값을 얻기 위해 Cost function을 이용한다.

이 Cost function이 Minimum value를 가지도록 만드는 Weight와 bias 값을 찾는것이 training의 목표이다.


# 1 Training 과 Cost function

Neural Network의 특징은 Data를 보고 학습할 수 있다는 것이다. Data를 학습한다는 말은 Data를 통해 Weight와 bias를 조절할 수 있다는 뜻이다.

앞서 다룬 Perceptron이나, 3층 Neural Network는 weight와 bias를 임의의 값으로 직접 결정하여 구현하였다.

하지만 실제 Neural network에는 수백 개에서 수천 개 이상의 Weight와 bias가 존재하기 때문에 이를 사람이 일일이 지정해주기란 쉽지 않은 일이기다.

우리는 이 작업을 Neural Network를 Training 하여 해결하고자 한다.

1. Data

    Machine Learning은 Data 중심적인 방식으로 접근하게 된다.

    인간은 어떤 문제를 해결해야할 때, 특히 어떠한 Pattern을 찾아야 할때 자신의 경험과 직관을 토대로 이런저런 생각과 추론을 통해 문제를 해결한다.

    하지만 컴퓨터는 인간과 같은 직관이나 경험을 가지고 있지 않다. Machine Learning은 주어진 Data에서 Pattern을 찾으려 시도한다.

    구체적인 예를 들어 생각해보자면 손글씨로 쓰여진 숫자들에서 5라는 숫자를 인식하는 프로그램을 개발한다고 생각해보자.

    사람은 5라는 숫자에 대한 경험적 지식이 있기에 자신의 경험과 직관을 통해 주어지는 Data가 5라는것을 쉽게 알아차릴 수 있다.

    하지만 이를 Algorithm화 시킨다면 어떨까?? 주어진 글씨들 사이에서 명확한 규칙성을 찾고 이들간의 Logic을 찾아 Algorithm화 시키는 것은 쉽지 않을 것이다.

    이러한 경험과 직관이 요구되는 문제를 컴퓨터를 통해 해결하기 위해 우리는 컴퓨터를 Training하여 경험을 쌓게 하고자 한다.

    주어진 Data에서 Feature를 추출하고 그 Feature의 Pattern을 학습하여, 학습(경험)하지 않은 새로운 Data가 주어지더라도 이 Data의 Feature와 Pattern을 파악 할 수 있게 하는 것이다.

2. Data의 종류

    Machine Learning은 크게 Training과 Inference 2가지 단계로 나뉜다.

    Training 단계는 Data들의 Feature와 그들간의 Pattern을 기계가 경험하는 과정이고, Inference 단계는 경험을 토대로 주어진 문제를 해결하는 과정이다.

    이를 위해 Data를 크게 Training data와 Test data 2가지로 분류해야 한다.

    Training data만을 이용하여 Neural Network를 Training 하고, Neural Network의 범용성을 시험하기 위해 Training data와는 다른 Test data를 사용하여 Network를 시험한다.

    범용성이란 아직까지 경험해보지 못한 문제를 올바르게 풀어내는 능력이다. Machine Learning은 Computer가 사람처럼 이전의 경험을 토대로하여 처음보는 새로운 문제(Data)를 스스로 해결해 나가기는 것을 목표로 하기 때문에 범용성은 아주 중요한 요소중 하나이다.

    그렇기 때문에 하나의 Data set만을 이용하여 Training과 Test를 수행하면 올바른 평가가 될 수 없다.

    Data set을 하나만 사용한다면 사용한 Data set에 대해서는 상당히 높은 Accuracy를 보일지라도 새로운 Data set에 대해서는 좋지 못한 결과를 얻을 가능성이 농후하다.

    이렇게 특정 Data set에 지나치게 최적화된 상태를 Overfitting이라고 한다. Machine Learning에서 Overfitting을 방지하는것은 중요한 과제중 하나이다.


---

# 2 Cost function

Neural Network는 현재의 상태를 하나의 지표로 사용하고, 그 지표를 가장 좋게 만들어 주는 Weight와 Bias 값을 찾으려 한다.

이 때 사용하는 지표가 Cost function이다. Cost function에는 여러 종류가 있지만 대게 MSE와 CEE를 사용한다.

1. MSE(Mean Squared Error)

    MSE는 가장 많이 사용되는 Cost function 중 하나로 다음의 수식을 가진다.

    $E = \frac{1}{2}\sum_{k}(y_{k} - t_{k})^2$

    여기서 $y_k$ 는 Neural Network의 Output(Input Data에 대한 추정치)을 나타낸다. $t_k$ 는 Answer label, $k$ 는 Dimension의 크기를 나타낸다.

    MSE는 추정값 $t_k$ 과 Answer label $y_k$ 의 차를 제곱한후 그 총합을 구한다. 아래는 MSE를 구현한 Python 코드이다.

    ```python
      import numpy as np
      def mean_squared_error(y,t):
        return 0.5 * np.sum((y-t)**2)
    ```

    여기서 Argument y와 t는 Numpy array이다. 두가지 예시를 통해 MSE의 결과값을 살펴보도록 하겠다.



    ```python
      import numpy as np
      def mean_squared_error(y,t):
        return 0.5 * np.sum((y-t)**2)
        
      t = np.array([0,0,1,0,0,0,0,0,0,0])
      y = np.array([0.1, 0.05, 0.1, 0.0, 0.05, 0.1, 0.0, 0.6, 0.0, 0.0])#class 7일 확률이 60%로 가장 높음
      mean_squared_error(y,t)#0.5975

      y = np.array([0.1, 0.05, 0.6, 0.0, 0.05, 0.1, 0.0, 0.1, 0.0, 0.0])#class 2일 확률이 60%로 가장 높음
      y = np.array([0.1, 0.05, 0.6, 0.0, 0.05, 0.1, 0.0, 0.1, 0.0, 0.0])
      mean_squared_error(y,t)#0.09750000000000003
    ```

    위의 코드에서 numpy array t처럼 단 하나의 값만이 1이고 나머지 값은 0의 값을 가지게 표현하는 표기법을 One-hot Encoding이라고 한다.

    첫번째 예시는 정답이 class 2이지만 Neural Network는 class 7이 60%의 확률로 정답이라고 판단하였다.
    
    이때 MSE는 0.5975의 값을 가진다.

    두번째 예시는 정답이 class 2 이고, Neural Network 또한 class 2가 60% 확률로 정답이라고 판단하였다.

    이때 MSE는 0.09750000000000003이다.

    Cost function은 Answer label $t$ 와 Output data $y$ 의 차이가 적으면 적을수록 작은 값을 가지게 된다.

    즉, 정답에 근접한 Output을 내놓을 수록 MSE의 값은 감소한다는 뜻이고, Output이 정답에 가까워 질수록 MSE는 0에 수렴하게 된다.


2. CEE(Cross Entropy Error)

    또 다른 Cost function인 CEE 도 자주 이용되는 Cost function으로 다음의 수식을 가진다.

    $E = - \sum_kt_klogy_k$

    여기서 log는 밑이 자연상수 $e$ 인 자연로그($log_e$)이다. $y_k$는 Neural Network의 Output, $t_k$는 Answer label이다.

    sigmoid function의 식은 다음과 같다.

    $h(x) =$ $1 \over 1 + e^(-x)$

    여기서 e는 자연상수 e를 뜻한다. 여기서 $t_k$ 는 One-hot Encoding 되었기 때문에 정답에 해당하는 Index의 원소만 1의 값을 가진다.

    즉 CEE의 값은 정답인 Index의 $-logy_k$ 가 결과값이 된다. 정답인 Index 이외의 $t_k$ 값은 모두 0 이기 때문에 0으로 계산된다.

    아래는 $ - log x$의 그래프이다.

    ![cross](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile7.uf.tistory.com%2Fimage%2F250AEB34579AF9B42492C3)

    $log x$의 그래프는 x의 값이 1 일 때 0의 값을 가지고, 0에 가까워 질수록 $- \infty$ 에 가까워 지는 값을 가진다.

    CEE는 $-logx$의 형태이기 때문에 x의 값이 1(정답)에 가까워 질 수록 0에 가까운값(적은 오차)를 가지고 x가 1에서 멀어질 수록 $\infty$ 에 가까운값(큰 오차)를 가지게 된다.

    아래는 CEE를 Python으로 구현한 코드와 CEE의 실사용 예이다.

    ```python
      import numpy as np
      def cee(y,t):
        delta = 1e-7
        return -np.sum(t * np.log(y + delta))
    ```

    위의 코드에서는 기존의 수식에서 찾아볼 수 없었던 delta라는 것이 추가되었다. delta는 컴퓨터가 np.log(0)의 값인 $-\infty$ 를 계산 할 수 없기 때문에 이를 방지하기 위해 아주 작은 값을 더하기 위해 사용된다.

    ```python
      import numpy as np
      def cee(y,t):
        delta = 1e-7
        return -np.sum(t * np.log(y + delta))

      t= np.array([0,0,1,0,0,0,0,0,0,0])
      y = np.array([0.1, 0.05, 0.6, 0.0, 0.05, 0.1, 0.0, 0.1, 0.0, 0.0])
      cee(y,t)#0.510825457099338

      y = np.array([0.1, 0.05, 0.1, 0.0, 0.05, 0.1, 0.0, 0.6, 0.0, 0.0])
      cee(y,t)#2.302584092994546
    ```

    첫번째 예는 Neural Network가 정답일 때 출력이 0.6일 때로 이때의 CEE는 약 0.51 정도이다. 

    두번째 예는 Neural Network가 정답일 때 출력이 0.1일 때로 이때으 CEE는 무려 2.3 이다.

    이렇듯이 CEE는 정답일 때 0에 가까운 값을 가지게 된다.

3. Cost function의 사용이유

    Training에서 우리의 궁극적인 목표는 높은 Accuracy를 끌어내는 Weight와 bias 값을 찾는데 있다.

    그렇다면 Accuracy를 직접 사용하지 않고 Cost라는 우회로를 택하는 이유는 무엇일까?

    이 의문을 해결하려면 Neural Network에서 Differential의 역할을 이해해야 한다.
    
    Training에서는 최적의 Weight와 bias를 탐색할 때 Cost function의 값을 최소화 하게 하는 weight와 bias를 찾으려한다.

    이 때 Cost function를 Differentiate하여 얻어지는 Cost function의 Gradient를 단서로 Weight와 bias의 값을 조절하게 된다.

    Gradient가 0에 가장 가까워 지도록 weight와 bias를 게속해서 수정하는 것이다.

    Gradient값이 0이 되면 cost 값을 가장 작게 만드는 weight와 bias값이라고 판단하여 수정이 더이상 이루어 지지 않는다.

    그렇다면 Cost를 최소화 하듯이 Accuracy를 최대화 하는 방식을 거꾸로 적용할 수 있지 않을까?

    Accuracy를 사용하지 않고 Cost를 사용하는 이유는 Accuracy function은 Differentiate 하였을 때 대부분의 장소에서 0의 값을 가지기 때문에 weight와 bias가 적절히 수정되지 못하기 때문이다.

    Accuracy는 Data의 개수에 따라 정해진 만큼 불연속적으로 변화한다. 예를 들어 100개의 Data 중 32개를 올바르게 인식하였다면 Accuracy는 32%이다.

    Data가 100개일 때는 1%씩, 1000개일 때는 0.1% 처럼 정해진 만큼 불연속적으로 변화하기 때문에 아래와 같은 형상이 된다.

    ![Gauss](https://i.stack.imgur.com/lIlGw.jpg)

    이러한 function을 Differentiate 할 경우 거의 모든 구간에서 0의 값을 가지기 때문에 이를 이용하여 Accuracy의 최대값을 찾는것은 불가능에 가깝다.

    이러한 이유로 Training 단계에서 Weight와 bias의 수정 지표로 Cost function을 이용하는 것이다.

    Activation function으로 Step function 대신 sigmoid나 ReLu를 사용하는 이유도 동일한 이유이다.

    Step function이 Weight와 bias가 주는 변화를 말살하여 Cost function의 값에 아무런 변화가 일어나지 않아 Training이 잘 이루어지지 않을 수 있기 때문이다.
 
4.  Batch training
   
    지금까지 알아본 Cost function은 모두 Data 하나에 대한 Cost를 구할 수 있었다. 하지만 실제 Machine Learning에서는 수백 ~ 수천 혹은 수만개 이상의 모든 Data에 대한 Cost를 구해야 한다.

    즉 Training data가 100개라면 Cost function의 결과값도 100개 가 되고, Neural Network는 100개의 Cost function의 결과값을 참고하여 Weight와 bias를 조정하게 된다.

    이제 부터는 Data 한 개가 아닌 모든 Training Data에 대한 Cost function 결과값을 구하는 방법에 대해 알아보도록 하겠다.

    앞서 배운 CEE는 N개의 Data에 대해 아래와 같은 수식을 가진다.

    $E = -\frac{1}{N}\sum_n \sum_k t_{nk}logy_{nk}$

    이때 N은 Training Data의 개수이고, $t_{nk}$ or $y_{nk}$는 n 번째 data의 k 번째 값을 뜻한다.

    기존의 식과 달라진 점은 N개의 Data에 대한 Cost function의 결과값을 모두 더한뒤 N으로 나누어 Normalize 했다는 점이다.

    Normalize를 통해 N개의 Data에 대한 Average Cost function을 구할 수 있다.

    하지만 이러한 방식으로 전체 Training Data를 학습하는데에는 많은 Computing source와 시간이 요구된다.

    Training Data의 개수가 너무 많을 경우 Data의 일부를 추려 Cost의 근사치를 구해 사용할 수 있다.

    이 때 추려지는 일부 Data를 mini-batch라고 하고, 이러한 Training 방식을 mini-batch training 이라고 한다.


---

# 3 Differentiation와 Gradient

Neural Network의 Training에서 최적의 Weight와 bias를 찾기 위해 가장 자주 사용되는 기법은 Gradient descending이다.

Gradient descending은 Cost function의 Gradient값을 기준으로 Weight와 bias를 수정할 방향을 정한다.

본 Section에서는 Gradient와 이이를 구하기 위한 Differentiation를 간단하게 알아보도록 하겠다.

1. Differentiation

    Differentiation는 한 순간의 변화량을 나타내는 지표이다. 그렇다면 변화량이란 무엇일까?

    예를들어 여러분이 마라톤 자동차를 타고 3시간동안 300km라는 거리를 이동했다고 하면 이때의 속력는 100km/h로 나타낼 수 있다.

    즉, 1시간에 100km만큼의 속력(변화량)으로 달렸다고 해석할 수 있다.

    하지만 이는 1시간 동안 자동차의 평균 속력(평균 변화량)을 구한것이다. 1 시간이라는 시간동안 자동차는 항상 100km/h로 달리지 않는다.

    Differentiation는 이러한 평균적 변화량을 구하는것이 아니라 그 순간의 순간 변화량을 구한다.

    즉 자동차가 지금 달리고 있는 찰나의 순간의 변화량을 구하는것이 Differentiation이고, 아래와 같은 수식으로 표현된다.

    $\frac{\text{d}f(x)}{\text{d}x} = \lim_{h \rightarrow 0}\frac{f(x+h)-f(x)}{h}$

    식의 좌변은 $f(x)$ 의 $x$ 에 대한 Differentiation를 나타내는 Symbol이다.

    $x$ 의 작은 변화가 function $f(x)$ 를 얼마나 변화시키느냐를 의미한다.

    우변의 $\frac{f(x+h)-f(x)}{h}$ 는 평균변화량을 의미한다 $h$ 라는 단위 동안 함수 $f(x)$ 가 얼마나 변화하였는가를 나타낸다.

    위의 자동차를 예로 들자면 $f(x)$ 는 처음의 이동거리, $f(x+h)$ 는 $h$ 시간 동안 달린 후의 이동거리 $h$ 는 자동차가 달린 시간이다.

    즉, $\frac{f(x+h)-f(x)}{h}$ 는 단위 당 함수 $f(x)$ 의 변화량을 나타내는 것이다.

    이 때 $h$ 가 0에 수렴하게 된다면 아주 짧은 단위 동안의 평균 변화량이 된다. 우리는 이와같은 아주짧은 시간의 평균 변화량을 순간 변화량으로 보는것이다.

    어떠한 function $f(x)$ 가 있을 때, 그 function의 derivative를 구하는 즉 $f'(x)$ 를 구해 순간 변화량을 얻는 방식을 Analytical differentiation 이라고 한다.

    우리가 사용한 방식은 아주 작은 차분을 이용하여 근사치를 얻는 Numerical differentiation이다.
    
    Numerical differentiation은 근사치를 얻는 방법이기 때문에 오차가 발생한다. 아래의 그림은 오차가 발생하는 원인을 보여주는 예이다.
    
    ![AD&ND](https://mblogthumb-phinf.pstatic.net/MjAxODA2MTVfMTQ1/MDAxNTI5MDUyMjE0MTkw.Gye5r5O_sHAWk79HZbGyQpi7rE4Gwmb3bCVRXTrvj6Ig.FmqyWXoIfUXckKwoPPPOQza0ZRz5G7jtcMGol1ypjlUg.PNG.ssdyka/fig_4-5.png?type=w2)

    이러한 오차를 최소화 시키기 위해 전방 차분을 이용하는 $f(x+h) - f(x)$ 을 중앙 차분(중심 차분)을 이용하도록 아래와 같이 변경할 것이다.

    $\frac{\text{d}f(x)}{\text{d}x} = \lim_{h \rightarrow 0}\frac{f(x+h)-f(x-h)}{2h}$

    이를 적용한 Python 코드는 다음과 같다

    ```python
       def numerical_diff(f,x):
        h = 1e-4
        return (f(x+h) - f(x-h)) / (2*h)
    ```

    h의 값은 작으면 작을 수록 오차가 적어져 좋지만 너무 작아지면 rounding error가 발생할 수 있기 때문에 통상적으로 사용되는 $e^-4$ 를 사용하였다.

2. Partial Differentiation

    만약 Differentiation 하려는 function이 $f(x_{0}, x_{1}) = x_0^2 + x_1^2$와 같은 multivariate function 이라면 어떻게 해야할까?

    아래는 위 function의 graph이다. 2개의 Variable을 가지기 때문에 3 Dimension으로 표현된다.

    ![func1](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F21E391335977F5BD20EBDB)

    Variable이 $x_{0}$ 와 $x_{1}$ 로 2개이기 때문에 어떤 Variable에 대해 Differentiate 할것인지를 구별해야 한다.

    이렇게 2개 이상의 Variable을 가지는 function에 대한 Differentiation을 Partial differentiation이라고 한다.

    기존의 Differentiation은 $\frac{\text{d}f(x)}{\text{d}x}$ 으로 표현하였지만 Partial Differentiation은 $\frac{\partial f}{\partial x_{0}} , \frac{\partial f}{\partial x_{1}}$ 으로 표현된다.

    Partial Differentiation에서는 현재 Differentiation 할 Variable 이외의 Variable은 Constant로 취급한다.


3. Gradient

    지금까지 cost function의 Gradient를 구하기 위한 Differentiation에 대해 알아보았다. 그렇다면 Gradient란 무엇이고 Cost function의 Gradient를 구해야하는 이유는 무엇일까?

    Gradient란 function에서 모든 Variable의 Partial Differentiation을 Vector로 정리한것이다.

    아래는 Python으로 Gradient를 구현한 것이다.

    ```python
      import numpy as np
      def numerical_gradient(f,x):
        h = 1e-4
        grad = np.zeros_like(x)

        for idx in range(x. size):
          tmp_val = x[idx]

          x[idx] = tmp_val + h
          fxh1 = f(x)

          x[idx] = tmp_val - h
          fxh2 = f(x)

          grad[idx] = (fxh1 - fxh2) / (2 * h)

          x[idx] = tmp_val
          
        return grad
    ```

    numerical_gradient(f,x)는 앞서 구현한 numerical_diff(f,x)와 상당히 유사하게 동작한다.

    다만 diff의 경우 하나의 x에 대해서만 동작하고 gradient의 경우 해당 function의 모든 variable인 x array에 대해서 동작한다는 점이 다르다.

    np.zero_like(x)는 x와 shape가 같고, 0으로 채워진 Array를 생성하는 동작을 한다.

    그렇다면 Gradient를 구함으로써 얻을 수 있는 정보는 무엇일까? 이를 알아보기 위해 $f(x_0, x_1) = x_0^2 + x_1^2$ 의 Gradient를 그래프로 나타내 보았다.

    ![grid](https://poddeeplearning.readthedocs.io/ko/latest/%EB%B0%91%EB%B0%94%EB%8B%A5%EB%B6%80%ED%84%B0%20%EC%8B%9C%EC%9E%91%ED%95%98%EB%8A%94%20%EB%94%A5%EB%9F%AC%EB%8B%9D/4_neuralnet_pulpan92_image/image5.png)

    Gradient는 위의 그림처럼 방향을 가진 Vector로 그려진다. 이 그림을 보면 Gradient는 function의 가장 낮은 장소(Minimum)을 가리키고 있다.

    또한 Minimum에서 멀어질 수록 화살표의 길이가 길어짐을 알 수 있다.

    Gradient는 각 지점에서 낮아지는 방향을 가르키고 있다.

    정확하게 말하자면 Gradient가 가르키는 쪽은 각 장소에서 function의 output을 가장 크게 줄일 수 있는 방향이다.

    Gradient 정보를 이용하여 function의 output을 줄일수 있는 곳에 대한 정보를 얻을 수 있는 것이다.

    우리는 이러한 Gradient 정보를 이용하여 cost function의 output을 줄이는 방법에 대해 알아볼 것이다.
    
4. Gradient descent method

    우리는 Neural network의 cost function이 minimum value를 가지게 하는 Weight와 Bias 값을 찾아야 한다.

    하지만 cost function은 일반적으로 매우 복잡하고, Parameter space가 복잡하여 minimum value를 찾기가 쉽지 않다.

    이를 해결하기 위해 Gradient를 이용하여 function의 minimum에 최대한 가까운 값을 찾기 위해 사용되는 방법이 Gradient descent method이다.

    하지만 Gradient descent method에서는 Gradient가 0인 지점이 항상 function의 minimum value라는 보장이 없다는 것이다.

    ![grad](https://www.safaribooksonline.com/library/view/hands-on-machine-learning/9781491962282/assets/mlst_0405.png)

    위 사진 처럼 Gradient가 0인 지점은 minimum value 일 수도 있고, local minimum point 혹은 saddle point 일수도 있기 때문이다.

    복잡한 모양의 function의 경우 plateau라고 하는 평평한, Training이 거의 진행되지 않는 구간도 존재할 수 있다.

    그럼에도 불구하고, Gradient descent method는 Minimum value를 찾을 수 있는 가장 효율적인 방법중 하나이기 때문에 널리 사용되고 있다.

    Gradient descent method는 다음의 과정으로 진행된다.

    현재의 Gradient를 구하고 이를 기점삼아 일정 거리만큼 이동한다.

    이후 이동한 위치에서의 Gradient를 구하고 이동하는 과정을 반복한다.

    이를 수식으로 나타내면 다음과 같다.

    $x_k = x_k - \eta\frac{\partial f}{\partial x_{k}}$

    위 수식중 기호 $\eta$ 는 Learning rate를 나타내는 기호이다.

    Learning rate는 한 번의 학습으로 얼마만큼 학습할지, 즉 Parameter를 얼마나 갱신 할지를 결정하는 Parameter이다.

    Learning rate는 0.1 또는 0.001과 같이 사용자가 미리 특정한 값을 지정해야 한다.

    Learning rate는 Weight나 Bias와 같이 Neural network가 Training을 통해 스스로 값을 결정하는 Parameter와 달리 사람이 직접 설정해야 하는 Parameter이다.

    이러한 Parameter를 Hyper Parameter라고 한다. Hyper Parameter는 여러번의 실험을 거쳐 최적의 값을 찾는 과정을 필요로 한다.

    일반적으로 Learning rate의 값이 너무 크거나 작으면 Minimum value를 찾아갈 수 없다.

    ![lr](https://jaehyeongan.github.io/image/learning_rate_sl.png)

    위의 예처럼 Learning rate가 너무 작으면 Weight와 Bias를 갱신하는데 너무 많은 시간이 요구되고, 여러번 학습을 하더라도 거의 변화가 이루어지지 않는다.

    반대로 Learning rate가 너무 크면 Cost가 감소하지 않고, 증가하는 Overshooting이 발생할 수 있기 때문에 적절한 값을 사용해야 한다.

    아래는 Gradient descent method와 적용 예를 Python으로 구현한것이다.


    ```python
      def gradient_descent(f, init_x, lr =0.01, step_num=100):
        x = init_x

        for i in range(step_num):
          grad = numerical_gradient(f,x)
          x -= lr * grad

        return x
    ```

    Argument f는 cost function, init_x는 초기값, lr은 Learning rate, step_num은 반복횟수이다.

    아래는 이를 적용하여 $f(x_0, x_1) = x_0^2 + x_1 ^2$ 의 Minimum value를 찾는 예이다.

    ```python
      import numpy as np
      def gradient_descent(f, init_x, lr =0.01, step_num=100):
        x = init_x
      
        for i in range(step_num):
          grad = numerical_gradient(f,x)
          x -= lr * grad
        
        return x

      def function_2(x):
        return x[0]**2 + x[1]**2

      def numerical_gradient(f,x):
        h = 1e-4
        grad = np.zeros_like(x)
    
        for idx in range(x.size):
          tmp_val = x[idx]
        
          x[idx] = tmp_val + h
          fxh1 = f(x)

          x[idx] = tmp_val - h
          fxh2 = f(x)
        
          grad[idx] = (fxh1 - fxh2) / (2 * h)

          x[idx] = tmp_val
        
        return grad

      init_x = np.array([-3.0, 4.0])
      gradient_descent(function_2, init_x=init_x, lr=0.1, step_num=100)
      #array([-6.11110793e-10,  8.14814391e-10])
    ```

    결과는 (-6.1e-10, 8.1e-10)으로 실제 Minimum value인 (0,0)에 상당히 가까운 값을 보인다.

    ![method](https://2.bp.blogspot.com/-ocZJ6T_Nf7A/WZ53x63h9jI/AAAAAAAAAJ4/3gGtOmhSEUYmmNEzMKaaBZOeYFBOOBUsQCLcBGAs/s1600/sgd_1.png)

    위의 사진과 같은 절차로 $x_0, x_1$ 의 값이 갱신되며 점차 (0,0)에 가까워지는 모습을 보인다.

5. Neural Network에서의 Gradient

    지금까지 Neural Network의 최적의 Parameter 값을 찾기위한 방법인 Gradient descent method에 대해 알아보았다.

    이제 이를 실제 Neural Network에 적용하는 방법을 알아보고 직접 실습해 보도록 하겠다.

    Neural Network에서의 Gradient는 Weight Parameter에 대한 cost function의 Gradient를 뜻한다.

    예를들어 shape가 2x3, Weight가 W, Cost function이 L인 Neural Network가 있다고 가정하자.

    이경우 Gradient는 $\frac{\partial L}{\partial W}$ 으로 나타낼 수 있고 다음과 같은 수식으로 표현된다.

    $W =\begin{pmatrix} 
    w_{11} & w_{12} & w_{13}\\
    w_{21} & w_{22} & w_{23}
    \end{pmatrix}$

    $\frac{\partial L}{\partial W} = 
\left(\begin{array}{c} \frac{\partial L}{\partial w_{11}} & \frac{\partial L}{\partial w_{12}} & \frac{\partial L}{\partial w_{13}}\\ \frac{\partial L}{\partial w_{21}} & \frac{\partial L}{\partial w_{22}} & \frac{\partial L}{\partial w_{23}}\end{array}\right)$

    $\frac{\partial L}{\partial W}$의 각 원소는 각각의 원소에 대한 Partial Differentiation이다. 예를 들어 $\frac{\partial L}{\partial w_{11}}$ 은 $w_{11}$을 변경하였을 때 L이 얼마나 변하는지를 나타낸다.







  

