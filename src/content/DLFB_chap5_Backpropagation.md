---
layout: post
title: Chap5 - Backpropagation
image: img/callum-shaw-555357-unsplash.jpg
author: 0verc10ck
date: 2020-01-15T10:00:00.000Z
tags:
  - 밑바닥 부터 시작하는 딥러닝
---


앞선 Chapter에서는 Neural network의 Training을 다루었다. Training의 과정에서 Costfunction의 Numerical differentiation을 통해 Gradient를 구하였다. 

Numerical differentiation은 구현이 쉽고 간단하지만 연산 시간이 오래 걸린다는 단점을 가지고 있다.

본 Chapter에서는 이러한 단점을 해결한 방법인 Backpropagtation을 배워 볼것이다.


# 1 Computational graph와 Chain rule

Backpropagation은 Backward propagation of error의 준말로 Neural Network에서의 Expected result와 real Result간의 Error를 이전 layer로 propagation하여 Parameter의 값을 조절한다.

Backpropagation의 이해를 위해 Computational graph와 Chain rule을 우선적으로 알아볼 것이다.


1. Computational graph

    Computational graph는 Computation 과정을 graph로 나타낸 것이다. 여기서 graph는 Data structure에서 사용되는 Graph로 Node와 Edge로 구성된다.
    
    시장에서 사과 2개와 귤 3개를 살 때의 과정을 Computational graph로 표현해 보도록 하자. 이때 사과의 가격은 개당 100원, 귤의 가격은 150원, 소비세는 10% 이라고 가정하자.

    ![graph1](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F997ED34B5B98F5F235)

    각 Node는 원으로 표현되고, 연산을 나타낸다. 각각의 Edge는 각 Node의 연산 결과를 나타낸다.

    위 사진의 예에서 100의 가격을 가진 사과를 2개 구입하였고, 150의 가격을 가진 귤을 3개 구입하였다.

    Computational graph는 Neural network와 마찬가지로 왼쪽에서 오른쪽으로 계산이 이루어지며 이러한 단계를 Forward propataion이라고 한다.

    Computational grap의 특징은 Local Computation을 Propagation함으로써 최종 결과를 얻는다는 점이다.

    Local 함이란 graph 전체에서 어떠한 일이 벌어지든 상관없이 자신과 관계된 정보만으로 결과를 출력할 수 있다는 말이다.

    예를 들자면 위의 graph에서 총 금액을 합산하는 부분은 전체 귤의 가격과 전체 사과의 가격이 어떠한 방법으로 계산되었느냐와는 상관없이 입력값인 귤의 총 가격과 사과의 총 가격 만을 알고 있으면 결과를 얻을 수 있다는 것이다.

    이것을 Neural network에 대입시켜 보자면, 이전 Layer에서 어떠한 일이 벌어졌든 간에 Input만 정확히 알고있다면 Output을 구할 수 있다는 것이다.

    그렇다면 Backpropagation을 Computational graph를 이용하여 푸는 이유는 무엇일까?

    Computational graph는 Local computation이라는 특성을 가지고 있다. 이는 아무리 복잡한 Computation이라도 단순한 Local computation들의 집합으로 나타낼 수 있기 때문에 큰 이점을 가진다.

    또한 중간 계산 결과를 모두 저장할 수 있기 때문에 Differentiation의 중간 결과들도 모두 저장된다 이는 이전 Layer의 Differentiation을 구하는데 큰 도움이 된다.


2. Chain rule

    앞서 다룬 Computational graph는 중간 Differentiation을 저장할 수 있기 때문에 큰 이점을 가진다고 설명하였다. 그렇다면 그 이유는 무엇일까?

    Computational graph를 사용한 Backpropagation의 예를하나 살펴보도록 하자.

    ![bp](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile8.uf.tistory.com%2Fimage%2F999FD3425B98F63F1A9DDF)

    $y = f(x)$ 라는 function의 backpropagation은 위의 graph로 나타 낼 수 있다. Backpropagation은 signal E에 local differentiation($\frac{\partial y}{\partial x}$)를 곱한 후 이전 Node로 전달하는 것이다.

    local differentiation이란 forward propagation에서의 $y = f(x)$ 의 Differentiation을 구한다는 것이며, $\frac{\partial y}{\partial x}$ 를 구한다는것이다.

    그리고 이 local differentiation을 오른쪽에서 전달된 값(E)와 곱해 왼쪽으로 전달하는 것이 Backpropagation이 이루어지는 과정이다.

    이 방식을 사용하면 현재 Layer에서 목표로하는 Differentiation 값을 효율적으로 구할 수 있다. 이러한 일이 가능한 이유는 Chain rule 때문이다.

    Chain rule을 이해하기 위해서는 우선 function composition을 알아야한다. function composition이란 여러 function으로 구성된 function을 의미한다.
    
    예를 들어 $z = (x+y)^2$ 라는 식은 다음의 두가지 식으로 표현된다. $z = t^2$ , $t = (x + y)$ 

    Chain rule은 이러한 function composition의 Differentiation에 대한 성질로 다음과 같이 정의된다.

    function composition의 Differentiation은 function composition를 구성하는 각 function의 Differentiation의 multiply로 표현 될 수 있다.

    위 의 function을 예로 설명하자면 $\frac{\partial z}{\partial x}$ 은 $\frac{\partial z}{\partial t}$ 와 $\frac{\partial t}{\partial x}$ 의 곱으로 표현 될 수 있다는 것이다. 이를 식으로 표현하면 아래와 같은 식을 얻게된다.

    ${\frac{\partial z}{\partial x} = \frac{\partial z}{\color{red}{\partial t}}\frac{\color{red}{\partial t}}{\partial x}}$

    위 식의 빨간색으로 처리된 부분이 서로를 지울수 있기 때문에 왼쪽의 식을 오른쪽의 식 처럼 각 function의 Differentiation의 multiply로 표현 된다는 것이 Chain rule이다.

     $\frac{\partial z}{\partial t} = 2t$ 이고, $\frac{\partial t}{\partial x} = 1$ 이기 때문에 $\frac{\partial z}{\partial x}$ 은 $\frac{\partial z}{\partial t} = 2t = 2(x+y)$ 이다.

     Computational graph는 이러한 Differentiation의 중간 단계들을 저장할 수 있기 때문에 각 단계의 Differentiation을 구하기 위해 Chain rule을 적용하기 수월하다는 장점이 있다.







---



# 2 Backpropagation

위 Section에서 Backpropagation을 이해하기 위한 요소들인 Computational graph와 Chain rule에 대해 알아보았다. 

본 Section에서는 Computational graph와 Chain rule을 이용하여 Addition와 Multiply node의 Backpropagation을 구해보고 이를 간단하게 구현해 볼것이다.

1. Additon node

    $z = x + y$ 라는 식이 있을 때 이 식에서의 Backpropagation을 살펴보자. $z = x + y$ 의 Differentiation은 아래와 같이 계산될 수 있다.

     $\frac{\partial z}{\partial x} = 1$ ,  $\frac{\partial z}{\partial y} = 1$

     Partial Differentiation에서 Differentiation해야할 Variable 이외의 Variable은 Constant로 취급하기 때문에 위와 같은 결과가 나타나게된다.

     이를 Computational Graph로 나타내면 아래의 사진과 같다.

     ![additiaon](https://t1.daumcdn.net/cfile/tistory/99771C465AA4FFEA13)

     위의 예에서 Addition Node는 상류에서 전달된 Differentiation($\frac{\partial L}{\partial z}$)에 1을 곱하여 하류로 흘려보낸다.

     상류에서 전달된 Differentitaion을 $\frac{\partial L}{\partial z}$ 이라고 표현하였는데, 이는 최종적으로 L이라는 결과를 출력하는 큰 Computational graph를 가정하고 $z = x + y$ 라는 연산은 그 graph의 어딘가에 존재하며, 상류로 부터 해당 값을 전달받았다고 가정한 것이다.

     즉 Addition node는 1을 곱하기만 할 뿐이므로 입력된 값을 그대로 다음 node로 보내게 된다.


2. Multiply node 

   $z = xy$ 라는 식이 있을 때 이 식에서의 Backpropagation을 살펴보자.  $z = xy$ 의 Differentiation은 아래와 같이 계산되고 이들의 Computational Graph는 다음과 같다.
   
   $\frac{\partial z}{\partial x} = y$ ,  $\frac{\partial z}{\partial y} = x$

   ![mul](https://t1.daumcdn.net/cfile/tistory/99A6DB435AA502DF0A)

   Multiply node의 Backpropagation은 전달된 상류의 값에 Forward propagation에서의 signal을 '서로 바꾼 값'을 곱해서 하류로 보낸다.

   '서로 바꾼 값'이란 위의 그림에서와 같이 Forward propagation에서 x였다면 Backpropagation에서는 y, Forward propagation에서 y였다면 Backpropagation에서는 x로 바꾼다는 의미이다.

   Additio node의 경우 입력된 값을 그대로 전달하기 때문에 Forward Propagation의 값이 필요하지 않았지만, Multiply node의 경우 Forward propagation의 값이 사용되기 때문에 이를 변수에 저장해 두어야 한다.

3. 간단한 예
   
    앞선 Section에서 예시로 들었던 시장 문제를 가져와 Addition node와 Mulitply node의 Backpropagation이 적용되는 방식을 자세히 살펴보자

    ![bp](https://t1.daumcdn.net/cfile/tistory/9964A5465AA506AA22)

    앞서 설명한 내용 처럼 Addition node는 상부에서 전달받은 signal를 그대로 하부에 전달한다. +에 해당하는 Node가 오른쪽에서 1.1 이라는 값을 전달받고 이를 그대로 왼쪽으로 Propagation하는것을 볼 수 있다.

    Multiply node역시 앞서 다룬 내용처럼 상부에서 전달받은 signal을 서로 바꾸어 하부로 전달하는 것을 확인할 수 있다.

    가장 오른쪽에 있는 node를 보면 1 이라는 singal을 상부로 부터 전달 받고 Forward propagation의 결과를 곱한 것을 서로 바꾸어 전달하는것을 볼 수있다. 나머지 x가 표시된 node들도 동일한 방식으로 동작하는것을 볼 수 있다.

    이렇게 Computational graph와 Chain rule을 이용하여 Backpropagation을 graph로 나타내면 복잡한 구조의 수식이라도 Backpropagation을 쉽게 구할수 있다.

4. 구현하기
   
    위에서 다룬 시장 문제를 Python으로 구현하여 Backpropagation을 직접 구현해보았다.

    ```python
      class MulLayer:
        def __init__(self):
          self.x = None
          self.y = None
        
        def forward(self, x, y):
          self.x = x
          self.y = y
          out = x * y
        
          return out
    
        def backward(self, dout):
          dx = dout * self.y
          dy = dout * self.x
        
          return dx, dy
    
      class AddLayer:
        def __init__(self):
          pass
    
        def forward(self, x, y):
          out = x + y
        
          return out
    
        def backward(self, dout):
          dx = dout * 1
          dy = dout * 1
        
          return dx, dy

      #Variable
      apple = 100
      apple_num = 2
      orange = 150
      orange_num = 3
      tax = 1.1

      #Layer
      mul_apple_layer = MulLayer()
      mul_orange_layer = MulLayer()
      add_apple_orange_layer = AddLayer()
      mul_tax_layer = MulLayer()

      #forward propagation
      apple_price = mul_apple_layer.forward(apple, apple_num)
      orange_price = mul_orange_layer.forward(orange, orange_num)
      all_price = add_apple_orange_layer.forward(apple_price, orange_price)
      price = mul_tax_layer.forward(all_price, tax)

      #backpropagation
      dprice = 1
      dall_price, dtax =mul_tax_layer.backward(dprice)
      dapple_price, dorange_price = add_apple_orange_layer.backward(dall_price)
      dorange, dorange_num = mul_orange_layer.backward(dorange_price)
      dapple, dapple_num = mul_apple_layer.backward(dapple_price)

      print(price)#715
      print(dapple_num, dapple, dorange, dorange_num, dtax)#110, 2.2, 3.3, 165, 650
    ```

    모든 Layer는 forward()와 backward()라는 공통의 Method를 가진다.

    MulLayer는 forward()에서는 두입력의 곱을 반환하고, backward()에서는 상류에서 넘어온 Dout과 서로바꾼 값을 곱하여 반환한다.

    AddLayer는 forward에서는 두 입력의 합을 반환하고, backward()에서는 상류에서 넘어온 Dout을 그대로 반환한다.

    forward propagation만 진행하였을 때 사과 2개와 귤 3개의 가격은 650원이고 10%의 소비세가 추가되어 715라는 결과를 얻게 된다.

    Backpropagation의 결과값을 저장한 변수들을 확인해 보면, 사과의 개수가 변하면 전체 가격은 110원 만큼 변하고, 사과의 가격은 전체 가격에 1원당 2.2 만큼의 영향을 미친다.

    오랜지또한 개수 별로 165의 변화율을, 가격 1원당 3.3의 변화율을 가진다. 소비세의 경우 1% 당 650의 변화율을 가지게 되는것을 알 수 있다.

    이처럼 Computational graph와 Chain rule을 사용하여 Backpropagation을 쉽게 구할 수 있다.

    다음 Section에서는 실제 Nueral Network에 이를 적용시켜 볼것이다.
---

# 3 실제 구현

1. Activation function

    1. ReLU
      
        Activation function으로 사용되는 ReLU의 수식은 다음과 같다.

        $y = \begin{cases} x (x \geq 0)\\ 0(x > 0)\end{cases}$

        ReLU를 Partial Differentiation 하면 아래와 같은 값을 얻을 수 있다.

        $\frac{\partial y}{\partial x} = \begin{cases} 1 (x \geq 0)\\ 0(x > 0)\end{cases}$

        Computational graph에서는 다음과 같이 표현된다.

        ![ReLU](https://youngwonseo.github.io/public/deep_learning_images/fig%205-18.png)

        이를 코드로 구현하면 아래와 같은 ReLU class로 표현할 수 있다.

        ```python
          class Relu:

            def __init__(self):
              self.mask = None
            
            def forward(self, x):
              self.mask = (x <= 0)
              out = x.copy()
              out[self.mask] = 0

              return out
            
            def backward(self, dout):
              dout[self.mask] = 0
              dx = dout

              return dx
        ```

        Relu class는 Mask라는 Instance Variable을 가진다. mask는 True/False로 구성된 Numpy array이다.

    2. Sigmoid

        Activation function으로 사용되는 Sigmoid의 수식은 다음과 같다.

        $y = \frac{1}{1 + e^{=x}}$

        Sigmoid의 경우 $e^{-x}$ 를 구하기 위해 exp라는 function이 사용되고, / 연산이 있기 때문에 4개의 단계로 이루어진다.

        ![sig](https://youngwonseo.github.io/public/deep_learning_images/fig%205-19.png)

        / Node의 Gradient는 다음과 같다.

        $\frac{\partial y}{\partial x} = - \frac{1}{x^2} = -y^2$

        즉 / Node에서는 상류에서 흘러온 값에 $-y^2$ 를 곱해서 하류로 전달한다.

        exp Node는 $y = e^x$ 연산을 수행하며, Differentiation은 다음과 같다.

        $\frac{\partial y}{\partial x} = e ^ x$

        exp Node는 상류의 값에 $e^{-x}$ 를 곱해서 하류로 전달한다.

        \+ Node와 x Node는 기존의 Addition Node와 Multiply Node 이므로 생략하였다.
  
        sigmoid의 전체 Computational graph는 다음과 같이 표현된다.

        ![sigmoid](https://youngwonseo.github.io/public/deep_learning_images/fig%205-20.png)

        이를 간략화 하면 아래와 같이 하나의 Node로 표현이 가능하다.

        ![sig2](https://camo.githubusercontent.com/d484f493b61ce6d2ff28f11cf63d8ffe65c71187/68747470733a2f2f692e696d6775722e636f6d2f715a6e47454d4e2e706e67)

        아래는 Sigmoid class이다.

        ```python
          class Sigmoid:
            def __init__(self):
              self.out = None
            
            def forward(self, x):
              out = 1 / (1 + np.exp(-x))
              self.out = out

              return out

            def backward(self, dout):
              dx = dout * (1.0 - self.out) * self.out

              return dx
        ```

2. Affine Layer

   Neural network의 Forward propagation에서는 한 Neuron의 signal의 총합을 계산하기 위해 Matrix multiply 연산을 진행하였다.(Numpy 에서 np.dot())

   geometry에서는 이러한 Matrix의 Multiply를 Affine transformation이라고 한다. 우리는 이러한 Affain transformation을 수행하는 layer를 Affine layer라는 이름으로 구현하고자한다.

   한 Neuron의 Signal 값은 y = w * x + b이다. 이는 matrix multiply 와 bias summation으로 이루어진 연산이다. 이를 Computational graph로 나타내면 다음과 같다.

   ![aff](https://camo.githubusercontent.com/450cc9a05dc2f5c7986ed2d1dd2b2cbc5e55bae5/68747470733a2f2f692e696d6775722e636f6d2f415a7a5a7664702e706e67)

   앞서 다룬 Computational graph들과 위 graph가 다른점은 이전의 graph들은 Scalar 값이 흐르지만 이 graph는 matrix가 흐른다는 것이 다른점이다.

   X, W, B는 matrix이다. 그렇다면 위 수식의 backpropagation은 무엇일까?

   $Y = WX + B$ 의 Partial Differentiation은 아래와 같다.

   $\frac{\partial L}{\partial X} = \frac{\partial L}{\partial Y} W^T$  ,  $\frac{\partial L}{\partial W} =  X^T \frac{\partial L}{\partial Y}$

   하지만 위의 결과값은 하나의 Data가 아닌 여러개의 Data를 Input으로 가진다. 이러한 batch affine layer를 computational graph로 나타내면 다음과 같다.

   ![baff](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile7.uf.tistory.com%2Fimage%2F994510365B98F75122F136)

   이를 python code로 구현하면 아래와 같다.

   ```python
    class Affine:
    def __init__(self, W, b):
        self.W = W
        self.b = b
        
        self.x = None
        self.original_x_shape = None
        self.dW = None
        self.db = None

    def forward(self, x):
        self.original_x_shape = x.shape
        x = x.reshape(x.shape[0], -1)
        self.x = x

        out = np.dot(self.x, self.W) + self.b

        return out

    def backward(self, dout):
        dx = np.dot(dout, self.W.T)
        self.dW = np.dot(self.x.T, dout)
        self.db = np.sum(dout, axis=0)
        
        dx = dx.reshape(*self.original_x_shape)
        return dx
   ```


3. Softmax

    마지막으로 Output layer에서 사용하는 softmax function의 back propagation을 구해보도록 하자.

    sofmax function은 Input을 Normalize하여 출력한다.

    이를 구현할 때 Cost function인 Cross entropy function을 softmax function과 함께 구현하도록 하겠다.

    Sofmax_with_Loss layer의 computational graph는 아래와 같다.

    ![swc](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile29.uf.tistory.com%2Fimage%2F99EBF5395B98F7792B42CE)

    Softmax_with_Loss layer의 Computational graph는 앞서 다룬 graph들과 달리 다소 복잡하다. 이를 간소화 하면 아래와 같은 graph를 얻을 수 있다.

    ![eas](https://camo.githubusercontent.com/3ff916b571f5034ee612ddf4a756d3bc892580a7/68747470733a2f2f692e696d6775722e636f6d2f656f72787978642e706e67)

    간소화된 graph는 3 class classification을 가정한것이다.
    
     softmax는 input a를 받아 normalize하여 output y를 출력한다 cross entry는 input y와 Answer label t를 받아 이들로 부터 cost L을 계산한다.

    여기서 주목할 점은 softmax의 back propagation의 결과이다. 결과는 각각 $(y_1 - t_1, y_2 - t_2, y_3, t_3)$ 이다. 
    
    이는 Answer label과 result간의 차이를 뜻한다. 이 차이를 통해 Neural network를 조절하게 된다. 이를 코드로 구현하면 아래와 같다.

    ```python
      class SoftmaxWithLoss:
        def __init__(self):
          self.loss = None
          self.y = None
          self.x = None

        def forward(self, x, t):
          self.t = t
          self.y = softmax(x)
          self.loss = cross_entropy_error(self.y, self.t)

          return self.loss
        
        def backward(self, dout = 1):
          batch_size = self.t.shape[0]
          dx = (self.y - self.t) / batch_size

          return dx
    ```
    
4. Gradient check

    지금까지 gradient를 구하는 두가지 방법인 Numerical Differentiation과 Backpropagation에 대해 알아보았다.

    Numerical Differentiation은 구현하기 쉽지만 느리다는 단점이 있다. 이러한 이유때문에 Backpropagation을 사용할것이다.

    그렇다면 Numerical Differentiation은 더이상 필요가 없는것일까?

    Numerical Differentiation은 Backpropagation이 잘 이루어 졌는지 검증하기 위해 사용된다. 

    Backpropagation은 빠르지만 구조가 복합하면 구현하기 복잡하기 때문에 종종 실수가 발생하곤 한다. 그래서 Numerical Differentiation과 Backpropagation의 결과를 비교하여 Backpropagation이 버그없이 잘 구현 되었는지 검증하는데 이러한 절차를 Gradient check이라고 한다.

    

