---
layout: draft
title: Chap2 - Perceptron
image: img/callum-shaw-555357-unsplash.jpg
author: 0verc10ck
date: 2019-10-11T10:00:00.000Z
tags:
  - 밑바닥 부터 시작하는 딥러닝
---

본 챕터에서는 Perceptron을 다룬다.

Perceptron은 1957에 Frank rosenblatt가 고안한 알고리즘이다.

Perceptron은 Nueral Network의 기원이 되는 알고리즘이다.


# 1 Perceptron이란?

Perceptron은 다수의 신호를 입력으로 받아 하나의 신호를 출력한다.

Perceptron은 신호가 흐른다, 흐르지 않는다(1 과 0) 두개의 값을 가진다.

![2inputPerceptron](https://www.google.com/url?sa=i&source=images&cd=&ved=2ahUKEwj0mKj2_pHlAhU1K6YKHVjsBaEQjRx6BAgBEAQ&url=http%3A%2F%2Fblog.naver.com%2FPostView.nhn%3FblogId%3Dinfoefficien%26logNo%3D221069835408%26parentCategoryNo%3D%26categoryNo%3D367%26viewDate%3D%26isShowPopularPosts%3Dtrue%26from%3Dsearch&psig=AOvVaw00n3t-6rXyyMo5z5U2_vQW&ust=1570807188193841)

위 그림은 입력으로 2개의 신호를 받는 Perceptron의 예이다.

$x_1$과 $x_2$는 입력신호, y는출력 신호를 뜻하고, $w_1$과 $w_2$는 Weight를 뜻한다.

그림의 원을 Neuron 혹은 Node라고 부른다.

입력신호는 각각의 Weight값과 곱해져 다음 Nueron으로 전해진다.

이러한 과정을 거쳐 출력층으로 전해진 신호의 값이 임계값 $\theta$(theta)를 넘어서면 1 넘어서지 못하면 0을 출력한다.

위 과정을 하나의 수식으로 나타내면 다음과 같다.

$
y=
\begin{cases}
0 \, (w_1x_1 + w_2x_2 \leq \theta)\\
1 \, (w_1x_1 + w_2x_2 > \theta)\\
\end{cases}
$


​퍼셉트론은 복수의 입력 신호 각각에 고유한 가중치를 부여합니다.

가중치는 각 신호가 결과에 주는 영향력을 조절하는 요소로 작용한다.

가중치가 클수록 해당 신호가 중요한 역할을 한다는 것을 뜻한다.

---


# 2 단순한 논리회로 구현

이번에는 Perceptron을 이용하여 간단한 논리 회로를 구성해 볼 것이다.

구현하기 전에 우선적으로 위 에서 정의한 Perceptron의 수식을 조금 수정하려 한다.

Perceptron은 $w * x$ 값과 $\theta$ 값을 비교하여 출력 값을 결정한다.

$\theta$는 값이 변하는 변수이기 때문에 우리는 비교의 대상을 0으로 삼아 조금 더 직관적인 수식을 얻고자 한다.


$
y=
\begin{cases}
0 \, (w_1x_1 + w_2x_2 + b \leq 0)\\
1 \, (w_1x_1 + w_2x_2 + b > 0)\\
\end{cases}
$


위 수식은 $\theta$를 이항한 식이다. 새롭게 나타난 변수 $b$는 $-\theta$를 뜻하며 **bias**라고 불리운다.

변경된 식은 입력값과 *weigth* 값의 곱에 *bias*를 더한것이 0보다 크면 1을 0보다 작으면 0을 반환한다.

이러한 수식은 출력의 기준이 0 이 되기 때문에 기존의 식보다 직관적이다.


1. AND 게이트

    AND 게이트는 입력이 둘이고 출력이 하나이다.

    AND 연산은 두 입력값이 모두 True 일 때만 결과값이 True가 된다.

    AND의 연산 결과는 아래의 표와 같다.
    
    | x_1 | x_2 | y |
    | ---------- | :--------- | :----------: |
    | 0 | 0 | 0 |
    | 1 | 0 | 0 |
    | 0 | 1 | 0 |
    | 1 | 1 | 1 |

    위 AND 게이트를 퍼셉트론으로 표현하려먼 위의 표와 같이 Perceptron이 작동하도록 *w_1, w_2, bias*의 값을 정해야한다.

    아래의 코드는 AND 게이트를 파이썬으로 구현한 것이다.

    ```python
      import numpy as np
      def AND(x1,x2):
        x = np.array([x1,x2])
        w = np.array([0.5, 0.5])
        b = -0.7
        tmp =np.sum(w*x) + b
        if tmp <= 0:
          return 0
        else:
          return 1
      
      AND(0,0) #ans : 0
      AND(0,1) #ans : 0
      AND(1,0) #ans : 0
      AND(1,1) #ans : 1
    ```

   입력값과 weight의 곱과 b의 합이 0 보다 크거나 같으면 1을 작으면 0을 반환한다.


2. NAND 게이트

    NAND 게이트는 Not AND를 뜻하며, AND연산의 결과와 반대의 결과를 가진다.

    NAND의 연산 결과는 아래의 표와 같다.
    
    | x_1 | x_2 | y |
    | ---------- | :--------- | :----------: |
    | 0 | 0 | 1 |
    | 1 | 0 | 1 |
    | 0 | 1 | 1 |
    | 1 | 1 | 0 |

    위 NAND 게이트를 퍼셉트론으로 표현하려먼 위의 표와 같이 Perceptron이 작동하도록 *w_1, w_2, bias*의 값을 정해야한다.

    아래의 코드는 NAND 게이트를 파이썬으로 구현한 것이다.

    ```python
      import numpy as np
      def NAND(x1, x2):
        x = np.array([x1,x2])
        w = np.array([-0.5, -0.5])
        b = 0.7
        tmp =np.sum(w*x) + b
        if tmp <= 0:
          return 0
        else:
          return 1
      
      NAND(0,0) #ans : 1
      NAND(0,1) #ans : 1
      NAND(1,0) #ans : 1
      NAND(1,1) #ans : 0

    ```

    AND와 마찬가지로 입력값과 weight의 곱과 b의 합이 0보다 크거나 같으면 1을 작으면 0을 반환한다.

3. OR 게이트

    OR 게이트는 두 입력값중 하나라도 True라면 True의 결과값을 가진다.

    OR의 연산 결과는 아래의 표와 같다.
    
    | x_1 | x_2 | y |
    | ---------- | :--------- | :----------: |
    | 0 | 0 | 0 |
    | 1 | 0 | 1 |
    | 0 | 1 | 1 |
    | 1 | 1 | 1 |

    위 OR 게이트를 퍼셉트론으로 표현하려먼 위의 표와 같이 Perceptron이 작동하도록 *w_1, w_2, bias*의 값을 정해야한다.

    아래의 코드는 OR 게이트를 파이썬으로 구현한 것이다.

    ```python
      import numpy as np
      def OR(x1, x2):
        x = np.array([x1,x2])
        w = np.array([0.8, 0.8])
        b = -0.7
        tmp =np.sum(w*x) + b
        if tmp <= 0:
          return 0
        else:
          return 1
      
      OR(0,0) #ans : 0
      OR(0,1) #ans : 1
      OR(1,0) #ans : 1
      OR(1,1) #ans : 1
    ```

    OR또한 입력값과 weight의 곱과 b의 합이 0보다 크거나 같으면 1을 작으면 0을 반환한다.

 





위의 예제들을 통해 우리는 Perceptron을 직접 구현해 보았다.

3가지 논리 게이트 모두 같은 형태의 Perceptron에서 Wegith값과 bias값만을 조정하여 서로 다른 역할을 하는 게이트를 완성하였다.

# 3 Perceptron의 한계와 해결책

앞서 다룬 내용에서 우리는 Perceptron의 weight와 bias 값을 수정하여 다양한 논리회로를 구성해 보았다.

그렇다면 Perceptron을 이용하여 더 복잡한 구조의 논리 게이트도 구현 할 수 있을까??

XOR 게이트를 Perceptron으로 만들어 보자.

1. Perceptron의 한계



