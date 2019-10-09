---
layout: post
title: Chap1 - Hello Python
image: img/callum-shaw-555357-unsplash.jpg
author: 0verc10ck
date: 2019-10-09T10:00:00.000Z
tags:
  - 밑바닥 부터 시작하는 딥러닝
---

본 챕터에서는 앞으로 필요한 python의 기본적인 문법과 자료형, 유용한 라이브러리의 사용법에 대해 알아볼 것이다. 

# 1 Python 기본 문법

## 자료형(Data type)

1. 숫자형(Numeric)

    숫자형 데이터에는 정수형(Integer)와 실수형(Real number) 두개의 자료형이 있다.

    파이썬은 다른 프로그래밍 언어인 Java나 Cpp, C#등의 언어들과 달리 자동형변환(Auto type casting)을 통해 우리가 일반적으로 사용하는 계산기와 같은 연산결과를 보여준다.

    다음은 숫자형 자료형을 이용한 간단한 사칙연산 예제이다

    
    ```python
      #basic operation
      a = 2
      b = 2.3
      c = 3
      print(a+b) # add ans : 4.3
      print(b-a) # sub ans : 0.3
      print(b*c) # multiply ans : 6.9
      print(c/a) # divide ans : 1.5
      print(c//a) # floor division ans : 1
      print(c%a) # modulus ans : 1
      print(c**a) # Exponent ans : 9 
    ```

    Python의 특이한점은 나누기 연산이 /와 // 두가지로 이루어져 있다는 것이다.

    / 연산은 연산의 결과가 항상 실수형이고, // 연산은 나누기 연산의 몫을 뜻한다.

    또한 **를 이용하여 손쉽게 제곱 연산을 할 수 있다.




2. 문자열(String)
    
    문자열(String)은 문자 집합을 다루는 자료형이다.
      
    문자열은 큰따음표(" ") 또는 작은 따음표(' ')로 둘러싸여 있다.

    문자열또한 연산 기호를 이용하여 다양한 작업을 수행 할 수 있다.
    
    다음은 문자열 연산과 문자열의 기능의 활용법이다.

    ```python
    
      str1 = "Python"  
      str2 = " is fun"
      str3 = "ab"

      print(str1 + str2) #string concatenation ans : 'Python is fun'
      print(str3 * 3) #string multiply ans : 'ababab'

      len(str3) #length of string ans : 2

      #indexing
      a = "Life is too short, You need Python"
      b = a[0] + a[6] + a[2] + a[3]
      print(b) # ans : 'Life'

      #slicing
      a[0:4] #ans : 'Life'
      a[0:3] #ans : 'Lif'
      a[5:7] #ans : 'is'
      a[:] #ans :'Life is too short, You need Python'
      a[19:-7] #ans : 'You need'

      #formatting
      day = "Mon"
      "Today is %sday" % day #ans : 'Today is Monday'
      duration = 5
      time = 3
      "You need to take this pills %d times per day during %d days" % (time, duration) #ans : 'You need to take this pills 3 times per day during 5 days'
    ```

    문자열 자료형 또한 숫자형 자료형 처럼 몇가지 연산이 가능하다.
      
    두 문자열을 + 연산을 통해 하나의 문자열로 만들고, *연산을 통해 한 문자열을 여러번 출력 할 수 도 있다.

    len()함수를 이용하면 문자열의 길이를 알 수 있다.

    Indexing은 문자열의 특정 위치의 값을 가져오는 기능이다.
      
    다만 해댱 위치의 값을 수정하는 것은 불가능하다.

    만약 문자열의 일부를 바꾸어야 한다면 slicing과 concatenation을 이용하여 새로운 문자열을 만들어야 한다.

    slicing은 문자열을 특정 구간을 잘라 사용할 수 있게 해준다.

    Indexing은 문자열에서 한 문자 만을 뽑아 내지만, slicing은 문자열에서 단어, 혹은 문장 단위를 뽑아낼 수 있다.

    Formatting은 문자열에 변수를 사용하여 불필요한 반복을 줄여주는 기능이다.  



3. 리스트(List Type)

    리스트는 많은 데이터를 한번에 다루기 위해 사용되는 자료형이다.

    리스트는 대괄호([ ])로 감싸주고, 요소값을 쉼포(,)로 구분한다.

    리스트 또한 문자열 처럼 Indexing과 Slicing이 가능하다.

    다만 리스트의 경우 문자열과 달리 Indexing을 통한 값 수정이 가능하다.

    또한 문자열의 +, *, len과 같은 연산자와 함수가 사용가능하다.

    다음은 리스트의 생성과 삽입/삭제 및 리스트의 다양한 함수들의 사용법이다.

    ```python
      a = [1,2,3]
      a[2] = 4
      a #ans : [1,2,4]

      del a[1]
      a #ans : [1,3]

      #리스트 함수

      #append : 리스트 맨 마지막에 요소를 추가한다.
      a = [1,2,3]
      a.append(4)
      a #ans : [1,2,3,4]
      a.append([5,6]) # ans : [1,2,3,4, [5,6]]

      #sort : 요소를 정렬한다.
      a = [1,4,3,2]
      a.sort()
      a #ans : [1,2,3,4]

      #reverse 리스트를 뒤집는다.
      a = ['a'. 'c', 'b']
      a.reverse()
      a #ans : ['b', 'c', 'a']

      #index : 요소에 x라는 값이 있으면 그 위치를 반환한다.
      a = [1,2,3]
      a.index(3) #ans : 2
      a.index(1) #ans : 0

      #insert : a위치에 b요소를 삽입
      a = [1, 2, 3]
      a.insert(0, 4)
      a #ans : [4, 1, 2, 3]

      #remove : 첫번째로 나오는 요소를 제거한다.
      a = [1, 2, 3, 1, 2, 3]
      a.remove(3)
      a#ans : [1, 2, 1, 2, 3]

      #count : 리스트에 포함된 요소의 개수를 센다.
      a = [1,2,3,1]
      a.count(1)#ans : 2

      #extend : 리스트 뒤에 리스트를 더한다.
      a = [1,2,3]
      a.extend([4,5])
      a#ans : [1,2,3,4,5]
      b = [6,7]
      a.extend(b)
      a#ans : [1,2,3,4,5,6,7]
    ```


    리스트는 다양한 내장 함수를 포함하고 있다.

    주의해서 볼 점은 append 와 extend의 차이점이다.
    
    두 함수 모두 리스트의 끝에 요소를 추가하지만, append의 경우 리스트가 요소로 들어 올 경우
    리스트가 하나의 요소로 인식되고, extend의 경우 리스트의 리스트의 각 요소를 각각 하나의 원소로 처리한다.

    또한 extend의 경우 함수의 parameter로 리스트만을 넘겨 줄 수 있다.


4. 튜플(Tuple)

    튜플은 몇가지 특징을 제외하면 리스트와 같다.

    리스트와 다른 점은 다음과 같다

    - 리스트는 []대신 ()을 사용한다.
  
    - 튜플은 요소의 값의 수정이 불가능하다.
    
    이 두 가지 특징을 제외하고, 튜플은 리스트와 같이 slicing, len, +, *등의 기능을 모두 사용 할 수 있다.


5. 딕셔너리(Dictionary)

    딕셔너리는 Index 대신 Key와 Value 형태를 통해 데이터를 관리하는 자료형이다.

    딕셔너리는 {}로 둘러쌓여 있으며, 각각의 요소는 Key:Value의 형태를 띄고 있다.

    각 요소들은 리스트나 튜플과 마찬가지로 쉼표(,)을 통해 구분된다.

    다음은 딕셔너리의 사용 예제이다

    ```python
     
      #요소추가
      a = {1: 'a'}
      a[2] = 'b'
      a #ans : {1: 'a', 2: 'b'}

      #요소 삭제
      del a[1]
      a #ans : {2: 'b'}

      #요소 접근
      a[2] # 'b'
    ```


6. 집합(Set)

    집합에 관련된 것을 쉽게 처리하기 위해 만든 자료형이다.
    
    집합은 set 함수를 사용해 만들 수 있다. 

    집합이 리스트나 튜플과 같은 자료형과 다른점은 다음과 같다.
        
    - 중복을 허용하지 않는다.

    - 순서가 없다(Unordered)

    집합은 순서가 없기 때문에 리스트나 튜플처럼 Indexing을 사용하여 요소에 접근 할 수 없다.

    집합 자료형은 수학의 집합과 같이 교집합, 차집합, 합집합을 구할 수 있는 기능을 가지고 있다.

    다음은 집합의 함수와 그 사용법이다.

    ```python
     s1 = set([1, 2, 3, 4, 5, 6])
     s2 = set([4, 5, 6, 7, 8, 9])
     
     #교집합
     s1 & s2 #ans {4, 5, 6}
     s1.intersection(s2) #ans {4, 5, 6}

     #합집합
     s1 | s2 #ans {1, 2, 3, 4, 5, 6, 7, 8, 9}
     s1.union(s2) #ans {1, 2, 3, 4, 5, 6, 7, 8, 9}
     
     #차집합
     s1 - s2 #ans : {1, 2, 3}
     s2 - s1 #ans : {8, 9, 7}
     s1.difference(s2) #ans : {1, 2, 3}
     s2.difference(s1) #ans : {8, 9, 7}
     
     #add : 값 추가하기
     s1 = set([1, 2, 3])
     s1.add(4)
     s1 #ans : {1, 2, 3, 4}
     
     # update : 여러개의 값 추가하기
     s1 = set([1, 2, 3])
     s1.update([4, 5, 6])
     s1 #ans : {1, 2, 3, 4, 5, 6}
     
     #remove : 특정 값 제거
     s1 = set([1, 2, 3])
     s1.remove(2)
     s1 #ans : {1, 3}
    ```


        
## 제어문

조건문과 반복문으로 이루어진 제어문은 프로그램의 분기를 결정하고, 프로그램의 구조를 단순화 시키는데 도움을 준다.

이러한 제어문의 사용을 통해 더 복잡한 명령을 수행 할 수 있는 프로그램을 작성 할 수 있게 된다.

1. 조건문

    조건문은 프로그램의 분기를 나누는 역할을 하는 제어문이다.

    조건문은 if, elif, else로 이루어 져 있으며, if, elif 뒤에 오는 조건문의 참, 거짓 여부에 따라 조건문 아래의 명령을 실행 여부가 결정된다.

    조건문의 끝에는 :이 존재하고, : 뒤에 오는 문장들은 모두 조건문 보다 들여쓰기 된 상태여야 한다.

    조건문에는 <, >, ==, !=, <=, >=과 같은 비교연산자가 사용 될 수 있다.

    조건문에는 or ,and, not과 같은 논리 연산자 또한 사용 될 수 있다.

    python에서는 x in s, x not in s와 같은 제어문 또한 사용 가능하다.

    다음은 조건문의 예제이다.

    ```python
      money = 2000
      card = False
      pocket = ['cellphone, wallet']

      if money > 3000 or card: # money가 3000이상이거나 card가 true이면 실행
        print("take taxi")

      elif money > 2000:
        print("take bus")
      
      elif "cellphone" in pocket:
        print("call friends")
      else:
        print("Let's walk!")
    ```

2. 반복문

    파이썬에는 for 문과 while문 두가지의 반복문이 존재한다.

    반복문은 반복문 내의 조건문이 참인 동안 반복문 내의 명령을 실행 한다.

    조건문이 거짓이 되면 반복문에서 탈출 한다.

    반복문이 내부 명령중 continue를 만나면 continue 이후의 명령들을 무시하고 지나친다.

    반복문이 내부 명령중 break를 만나면 즉시 반복을 중단하고 반복문을 빠져나온다.

    다음은 for문과 while문의 사용방법이다.
    
    ```python
      #for
      test_list = ['one', 'two', 'three'] 
      for i in test_list: 
        print(i)

      #ans : one, two, three


      #for 문의 range 함수
      #range 함수는 숫자 리스트를 자동으로 만들어 주는 함수이다.

      add = 0
      for i in range(1,11): #range 함수를 통해 1이상 11미만의 숫자를 포함하는 range 객체생성
        add = add+i

      print(add) #ans : 55

      #while
      money = 1600
      while money >= 500:
        print("playing game")
        moeny -= 500

      #ans : playing game playing game playing game
    ```

  

---

# 2 Numpy

Numpy는 배열이나 행렬 계산을 편리하게 해주는 파이썬 외부 라이브러리 이다.

Machine Learning에서 배열과 행렬 연산은 가장 빈번히 일어나는 연산 이기 때문에 Numpy는 필수적인 라이브러리중 하나이다.

Numpy의 배열 클래스인 numpy.array에는 배열과 행렬 연산을 위한 메서드가 구현되어 있어 손쉽게 배열과 행렬 연산을 수행 할 수 있다.

Numpy 배열은 Scalar value와 vector의 연산에서 scalar를 연산할 vector와 같은 형상의 vector로 변형 시켜주는 broadcast 기능이 있다.

다음은 Numpy의 기본적인 사용법이다.


```python
  import numpy as np

  x = np.array([1.0,2.0,3.0])
  print(x) #ans : [1.,2.,3.]

  y = np.array([2.0,4.0,6.0])
  print(x+y) #ans : [3.,6.,9.]
  print(x-y) #ans : [-1.,-2.,-3.]
  print(x*y) #ans : [2., 8., 18.]
  print(x/y) #ans : [0.5,0.5,0.5]
  
  A = np.array([[1,2],[3,4]])
  print(A) #ans : [[1,2], [3,4]]
  A.shape #(2,2)

  #Broadcast
  A * 10 #ans : [[10, 20], [30,40]]
  #scalar 값 10은 (2,2) vector [[10,10],[10,10]]으로 broad cast된다.


  #indexing
  A[0] #ans : array([1,2])
  A[1][1] #ans : 4

  #flatten
  A = A.flatten()
  print(A) #ans : [1,2,3,4] -> 2차원의 배열이 1차원 배열로 flatten(평탄화) 되었다.

  A > 2 #ans : [False, False, True, True]
  A[A>2] #ans : array([3,4])
```

이 처럼 numpy는 python list에서는 지원하지 않는 broadcast, flatten등의 다양한 기능을 지원하여 행렬과 배열을 손쉽게 처리 할 수 있도록 한다.



---

# 3 matplotlib

matplotlib은 그래프 그리기와 데이터 시각화에 사용되는 외부 라이브러리아다.

다음은 matplotlib을 이용하여 데이터를 그리는 방법이다.


```python
  import numpy as np
  import matplotlib.pyplot as plt

  x = np.arrange(0,6,0.1)
  y = np.sin(x)

  plt.plot(x,y)
  plt.show()
```

![pyplot1](http://xhy.pw/assets/img/Deep%20Learning%20from%20Scratch/output_74_0.png)