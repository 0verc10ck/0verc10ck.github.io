---
layout: post
title: Chap3 - Neural Network
image: img/callum-shaw-555357-unsplash.jpg
author: 0verc10ck
date: 2020-01-05T10:00:00.000Z
tags:
  - 밑바닥 부터 시작하는 딥러닝
---

본 chapter에서는 Multi layer Perceptron을 이용하여 구성한 Nerual Network에 대해 알아보고자 한다.


# 1 Neural Network

Nerual Network는 multi layer Perceptron과 유사하다.

아래는 Neural Network를 나타낸 그림이다.

![NN](https://4.bp.blogspot.com/-qZUY49EyEvo/W9FvnpymXaI/AAAAAAAAAIk/2pkCr5aLrIApcDywt7z_rnStdsUDaJFKQCLcBGAs/s1600/2.JPG)

위의 Neural Network에서 가장 왼쪽에 위치한 줄을 Input layer(입력층), 가장 오른쪽에 위치한 줄을 Output layer(출력층), Input layer와 Output layer의 사이에 위치한 줄을 Hidden layer(은닉층)이라고 한다.

Hidden layer의 Neuron은 Input layer나 Output layer의 것과 달리 겉으로 드러나지 않는다.

Neural Network의 Hidden layer는 single layer 일 수도 있고 multi layer일 수도 있다.

Neural Netwrok의 Input layer를 0 또는 1층 이라고 하고 오른쪽으로 갈 수록 층이 높아지게 된다. 대부분의 컴퓨터 언어는 0을 Array의 첫 Index로 판단하기 때문에 Neural Network 또한 0 층부터 세도록 하겠다.

Neural Network의 구조는 MLP와 비슷하다 이를 좀 더 자세히 알아보기 위해 Perceptron을 잠깐 되돌아 보도록 하자

Perceptron은 input data x 를 weight w와 곱한 뒤 bias b를 더한 값이 0보다 크면 1의 값을 0보다 작으면 0의 값을 가진다.

이를 식으로 나타내면 다음과 같다.

$
y=
\begin{cases}
0 \, (wx + b \leq 0)\\
1 \, (wx + b > 0)\\
\end{cases}
$

이때 wx + b의 값에 따라 y의 값을 0 또는 1로 결정하는 함수를  h(x)라고 하면 위의 식은 아래의 식으로 나타낼 수 있다.

$
 h(x)=
\begin{cases}
0 \, (x \leq 0)\\
1 \, (x > 0)\\
\end{cases}
$

이처럼 신호의 총합을 출력 신호로 변환하는 h(x)와 같은 함수를 activation function이라고 한다. 

Neural Network는 다양한 종류의 activation function을 이용하여 최적의 weight 값을 구한다.

이어지는 section에서 activation function에 대해 알아보자

---

# 2 Activation function

Activation function은 임계값을 경계로 출력의 결과가 바뀌는 function이다. 

앞서살펴본 Perceptron의 경우 weigth * input data + bias의 값이 0보다 크면 1의 값을 작으면 0의 값을 반환하였다. 이러한 함수를 Step function이라고 한다.

Nerual Network는 Step function 이외에도 sigmoid, ReLu와 같은 다양한 Activation function을 이용한다. 


1. Step function

    Step function에 대한 내용은 앞선 chapter에서 많이 다루었기 때문에 이번 절에서는 step function을 직접 구현해보고 그 그래프를 그려보도록 할것이다.

    step function은 input이 1을 넘으면 1을 반환하고 input이 1보다 작으면 0을 반환하는 function이다.

    다음은 step function을 python으로 구현한 것이다.


    ```python
      def step_function(x):
        if x > 0:
          return 1
        else :
          return 0
    ```

    위의 코드는 상당히 간단하게 step function을 나타내었지만 input data로 실수값만을 받아들인다.  input data로 numpy array를 사용하고 싶다면 다음과같은 코드를 사용하면 된다.

    ```python
      import numpy as np
      def step_function(x):
        y = x > 0
        return y.astype(np.int)
    ```

    3째 줄의 y = x > 0은 x의 값에 따라 true 또는 false의 boolean data를 y에 할당한다.

    return 문에서는 boolean type의 data y를 int type으로 typecasting하여 0 또는 1의 값을 가지는 numpy array를 반환하도록 한다.

    다음은 위의 함수를 이용한 간단한 예시이다.

    ```python
      import numpy as np
      x = np.array([-1.0, 1.0, 2.0])
      step_fucntion(x)#array[0, 1, 1]
    ```

   step function을 좀더 직관적으로 이해하기 위해 그래프를 그려보자. 
   
   다음은 matplotlib을 이용하여 step_function의 그래프를 그리는 코드와 그 결과이다.

   ```python
      import numpy as np
      import matplotlib.pyplot as plt

      def step_function(x):
        return np.array(x > 0, dtype=np.int)

      x = np.arange(-5.0, 5.0, 0.1)
      y = step_function(x)
      plt.plot(x,y)
      plt.ylim(-0.1, 1.1)#y축의 범위 지정
      plt.show()
   ```

    ![stepfunc](https://raw.githubusercontent.com/0verc10ck/0verc10ck.github.io/master/src/content/img/DLFB_chap3/stepfunc.PNG)

   np.arange(-5.0, 5.0, 0.1)은 -5.0부터 5.0까지 0.1 간격의 numpy array를 생성한다.

   이 numpy array x는 step_function()으로 전달이 되고, 1 또는 0의 값을 가진 numpy array y로 반환된다.

   x,y의 값으로 그래프를 그리면 위와 같이 0까지 0의 값을 가지고, 0 이상부터 1의 값을 가지는 그래프가 그려진다.

   이처럼 step_function은 그래프가 마치 계단의 모양과 흡사하기 때문에 step_function(계단함수)라는 이름을 가지게 된 것이다.



2. Sigmoid function

    Sigmoid function은 Neural Network에서 가장 자주 사용되는 activation function중 하나이다.

    sigmoid function의 식은 다음과 같다.

    $h(x) =$ $1 \over 1 + e^(-x)$

    여기서 e는 자연상수 e를 뜻한다. 
    
    sigmoid function은 수식만을 보면 상당히 복잡해 보이지만 그 목적은 step function과 같다. 다만 step function과 달리 0,1 이외의 값도 반환한다는 차이를 가지고 있다.

    step_function을 activation function으로 이용하면 오로지 0 또는 1의 값만을 다음 layer의 input으로 전달하지만 sigmoid function을 이용하면 다양한 값을 input으로 전달 할 수 있기 때문에 Neural Network를 좀더 세세하게 조정할 수 있다.

    아래는 sigmoid function을 python으로 구현한것이다.

    ```python 
      def sigmoid(x):
        return 1/(1+np.exp(-x))
    ```

    여기서 np.exp(-x)는 $e^(-x)$를 뜻한다.

    아래는 matplotlib을 이용하여 sigmoid function을 그래프로 나타낸 것이다.

    ```python
      import numpy as np
      import matplotlib.pyplot as plt

       def sigmoid(x):
        return 1/(1+np.exp(-x))

      x = np.arange(-5.0, 5.0, 0.1)
      y = sigmoid(x)
      plt.plot(x,y)
      plt.ylim(-0.1, 1.1)#y축의 범위 지정
      plt.show()
    ```

    ![sigmoid](https://raw.githubusercontent.com/0verc10ck/0verc10ck.github.io/master/src/content/img/DLFB_chap3/sigmoid.PNG)


    Sigmoid function은 step function과 달리 매끄러운 형상을 가지고 있다.

    sigmoid function은 부드러운 곡선의 형태를 띄고 있으며, input에 따라 output이 연속적으로 변화한다.

    하지만 step function은 0을 경계로 하여 output이 갑작스럽게 변화한다.

    0,1 두개의 output만을 가지는 step function과 달리 sigmoid function은 0 ~ 1사이의 모든 값을 output으로 가질 수 있다.

    Step function과 Sigmoid function은 공통적으로 input이 커지면 output이 1에 가까워지거나 1이 되고, input이 작아지면 output이 0에 가까워거나 0이 되는 구조를 가지고 있다.

    다만 Step function이 Discret한 output을 가진다면 Sigmoid function은 Continuous한 output을 가진다는 차이점이 있다.


3. ReLu(Rectified Linear Unit)

    ReLu(Rectified Linear Unit)는 이름에서 알 수 있듯이 정류된 선형 Unit이다.

    ReLu는 BackPropagation 방식을 활용하여 Neural Network를 학습시킬 때 발생하는 Gradient Vanishing을 어느정도 해결해준다.

    Gradient Vanishing과 BackPropagation은 나중에 따로 다루도록 하고 지금은 ReLu 함수의 구조에 대해 알아보도록 하자

    ReLu는 input이 0을 넘으면 input을 그대로 output으로 사용하고 0 이하이면 output의 값이 0이 된다.

    아래는 ReLu를 수식으로 표현한것이다.

    $
    h(x)=
    \begin{cases}
    0 \, (x \leq 0)\\
    x \, (x > 0)\\
    \end{cases}
    $

    아래는 python으로 ReLu를 구현하고, 이를 그래프로 나타낸 것이다.

    ```python
    import numpy as np
    import matplotlib.pyplot as plt

    def ReLu(x):
      return np.maximum(0,x)

    x = np.arange(-5.0, 5.0, 0.1)
    y = ReLu(x)
    plt.plot(x,y)
    plt.ylim(-0.1, 5.1)#y축의 범위 지정
    plt.show()
    ```
    ![ReLu](https://raw.githubusercontent.com/0verc10ck/0verc10ck.github.io/master/src/content/img/DLFB_chap3/ReLu.PNG)

    위 코드에서 np.maximum(0,x)는 0과 x중 큰것의 값을 반환하는 function이다.

    ReLu는 input이 0보다 크면 input을 그대로 output으로 사용하기 때문에 선형적인 형태를 띈다.

    Sigmoid의 경우 input이 일정값을 넘어설 경우 1 또는 0에 수렴하기 때문에 2개의 intput이 큰 차이를 가지더라도 output이 큰차이를 가지지 않을 수 있다.

    하지만 ReLu의 경우 0 이상의 값들은 Input의 차이가 Output의 차이를 불러오게 된다. 

    물론 ReLu도 음수값이 항상 0이라는 문제점이 존재한다. 이러한 문제제점을 해결하기 위해 Leaky ReLU 및 Parametric ReLU과 같은 Activation function등이 개발되고 있다.


4. Linear & Nonlinear function
   
    앞서 살펴본 3개의 Activation Function은 모두 NonLinear function이라는 공통점을 가지고 있다.

    $y = ax + b$ 와 같이 1차 함수의 꼴을 하고 있는 함수를 Linear function이라고 한다.

    Neural Network에서는 Activation function으로 Nonlinear function을 사용해야한다.

    다르게 말하면 Linear function은 사용할 수 없다는 말이다.

    Linear function을 Activation function으로 사용하면 안되는 이유는 무엇일까?

    만약 2개의 Hidden Layer를 가진 Neural Network가 있다고 가정해보자

    이 Nerural Network의 Activation function이 $h(x) = ax + b$라고 하고, 이 Neural Network의 Input이 x라고 하면 Output은 다음과 같다.

    $y = h(h(h(x)))$ 이고 $h(x) = ax +b$ 를 대입하면 $y = a^3x + a^2b$ 가 된다.

    $a^3$ 을 $A$ , $a^2b$ 를 $B$ 라고 하면 $y = Ax +B$ 로 나타낼 수 있고, 이는 $y = ax + b$ 에서 계수만을 바꾼것이된다.

    결론적으로 아무리 Hidden layer가 많더라도 Activation Function이 Linear 하다면 그 Neural Network는 Hidden Layer가 없는 Input, Output Layer로 표현할 수 있기 때문에 Linear 한 Activation Function을 사용하지 않는 것이다.

---

# 3 Neural Network 구현하기

Neural Network는 Multi-dimension numpy array을 이용하여 구현된다.

본 Section에서는 Python을 이용하여 3층 Nural Network를 구현해볼 것이다.

1. Neural Network 구현하기

    ![3NN](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99651A475A6926431F)

    우리는 위 사진과 같이 Input, Output Layer와 2개의 Hidden Layer를 가진 3층(입력층을 0층으로 가정하였음) Neural Network를 구현할 것이다.

    편의를 위해 Input layer에서 첫번째 Hidden layer로 가는 weight를 W1, bias를 B1이라고 하자.

    첫번째 Hidden layer에서 2번째 Hidden layer로 가는 weight는 W2, bias는 B2가 된다.

    마지막으로 Output layer 향하는 weight는 W3, bias는 B3가 된다.

    Activation function으로는 Sigmoid function을 이용할 것이고, Output Layer에서는 Identity function을 이용하여 값을 출력하도록 하겠다.

    아래는 위 사진의 Neural Network를 Python 코드로 구현한 것이다.

    각 weigth, x, bias의 값은 임의로 적당한 값을 설정하도록 하겠다.

    ```python
      import numpy as np
      def Init_network():
        network = {}
        network['W1'] = np.array([[0.1, 0.3, 0.5], [0.2, 0.4, 0.6]])
        network['B1'] = np.array([[0.1,0.2,0.3]])
        network['W2'] = np.array([[0.1,0.4],[0.2,0.5],[0.3,0.6]])
        network['B2'] = np.array([0.1,0.2])
        network['W3'] = np.array([[0.1,0.3],[0.2,0.4]])
        network['B3'] = np.array([0.1,0.2])
        
        return network

      def forward(network, x):
        W1, W2, W3 = network['W1'],network['W2'],network['W3']
        B1, B2, B3 = network['B1'],network['B2'],network['B3']
    
        a1 = np.dot(x, W1) + B1
        z1 = sigmoid(a1)
    
        a2 = np.dot(z1, W2) + B2
        z2 = sigmoid(a2)
    
        a3= np.dot(z2, W3) + B3
        y= identity_function(a3)
    
        return y

      def sigmoid(x):
        return 1/(1+np.exp(-x))

      def identity_function(x):
        return x
        
      network = Init_network()
      x = np.array([1.0, 0.5])
      y = forward(network, x)
      print(y)
      #[[0.31682708 0.69627909]]
      ```

    위 코드는 Neural Network를 구현하는 Init_network, Input signal을 Output signal로 변환하는 forward, Activation function sigmoid와 Identity_function으로 구성 되어 있다.

    Identity_function은 Input을 그대로 반환하기 때문에 굳이 구현할 필요는 없지만 Neural Network의 흐름을 통일하기 위해 구현하였다.

    Init_network에서는 각 Neural Network의 각 Layer별 Weight와 Bias 값을 지정한다.

    forward에서는 Init_network에서 지정한 W값과 B 값을 이용하여 a에 x * W + B의 값을 저장하고, 이를 sigmoid 또는 Identitiy_function을 거쳐 값을 z 또는 y 에 저장하고, 최종 결과인 y를 반환한다.

    function name으로 forward를 사용한 이유는 signal이 Input에서 Output 방향인 순방향만을 향해서만 진행되기 때문이다. 

    추후에 Output에서 Input 방향인 역방향으로의 진행에 대해서도 다루도록 하겠다.


2. Output layer 설계하기

    Neural Network는 Classification과 Regression에 모두 이용할 수 있다. 
    
    다만 둘중 어떤 문제에 사용하느냐에 따라 Output layer에서 사용하는 Activation function이 달라진다.

    Regression은 Input data에서 연속된 수치를 예측하는 문제이고, Classification은 Input data가 어떤 class에 속하는지를 찾는 문제이다.

    일반적으로 Regression에는 Identitiy function을 Classification에는 Softmax를 사용한다.

    Identitiy function은 Input을 그대로 Output으로 사용한다. 한편 Softmax function은 다음의 수식을 가진다.

    $y_{k} =\frac{ e^{a^{k}}}{\sum_{i=1}^n e^{a^{i}}}$

    위 수식에서 n은 Output layer의 Neuron의 수이고, $y_{k}$는 n개의 Neuron중 k번째 Neuron의 Output임을 나타낸다.

    아래는 softmax function을 python으로 구현한 것이다.

    ```python
      def softmax(a):
        exp_a = np.exp(a)
        sum_exp_a = np.sum(exp_a)
        
        return exp_a / sum_exp_a
    ```

    위 코드는 위의 softmax의 식을 완벽하게 구현하였지만 한가지 큰 결함이 있다.

    그것은 바로 컴퓨터 상에서 동작할 때 Overflow 문제가 발생한다는 것이다.

    일반적으로 Exponential 하게 증가하는 수치는 아주 큰 값이 된다. $e^{100}$ 만 되어도 2.6881171e+43의 값을 가지기 때문에 float의 범위를 한참 뛰어 넘는다.

    이를 해결하기 위해 exp_a를 계산하는 과정에서 Inputsignal의 Max 값을 c라고 하고 이 값을 a에서 빼주면 Overflow를 방지할 수 있다.

    아래는 이러한 해결책을 적용한 코드이다.

     ```python
      def softmax(a):
        c = np.max(a)
        exp_a = np.exp(a - c)
        sum_exp_a = np.sum(exp_a)
        
        return exp_a / sum_exp_a
    ```

    그렇다면 Classification에서 Output layer의 Activation function으로 softmax를 사용하는 이유는 무엇일까?

    이를 알아보고자 하면 softmax의 특징에 대해 알아야 한다.

    Softmax는 0 ~ 1 사이의 Output을 가진다. 또한 Softmax의 모든 Output의 summation은 1이 된다.

    이말인 즉슨 Softmax의 각 Output은 확률로 해석될 수 있다는 말이다.

    이해를 돕기 위해 아래의 예시코드를 이용하여 설명을 진행하도록 하겠다.

    ```python
      import numpy as np
      def softmax(a):
        c = np.max(a)
        exp_a = np.exp(a - c)
        sum_exp_a = np.sum(exp_a)
        
        return exp_a / sum_exp_a

      a = np.array([0.3, 2.9, 4.0])
      y = softmax(a)
      print(y)//[0.01821127 0.24519181 0.73659691]
      np.sum(y)//1.0
    ```

    위의 예에서 Input data가 y[0]일 확률은 0.0018(1.8%), y[1]일 확률은 0.245(24.5%), y[2]일 확률은 0.737(73.7%)로 볼 수 있다.

    이러한 결과로 부터 "2번째 Class일 확률이 74%로 가장 높으니 해당 Data는 2번째 Class 일것이다"와 같은 결론을 내릴 수 있게 되는 것이다.

    모든 y값의 summation은 1.0이므로 각 y 값이 나타내는 것을 확률로 이해할 수 있기 때문에 Classification에서 Softmax를 사용한다.

    Softmax 함수는 Input의 대소관계가 Output에서 달라지지 않는다는 특징을 가지고 있다. np.exp() 연산에 많은 Computing source가 요구되기 때문에 Softmax는 주로 Training 단계에서만 사용되고 Inference 단계에서는 생략하는것이 일반적이다.

    그렇다면 Output layer의 설계는 어떻게 해야할까?

    Output layer 또한 Activation function처럼 Classification, Regression에 따라 달라진다.

    Classification에서 Output layer는 Classificate할 Class의 개수만큼 Neuron을 설정해야 한다.

    가령 0 ~ 9 까지의 숫자를 분류하고자 한다면 Output layer는 10개의 Neuron을 가진다.


    

