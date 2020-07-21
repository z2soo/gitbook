# Tensorflow 기초

## 1. Tensorflow 기본 개념

Google의 Tensorflow 프로그램을 통해서 머신러닝을 해볼 것이다.  
다른 package, module에 비해 살짝 특이한 형태의 library이다. Tensorflow의 3가지 구성요소는 다음과 같다. 

### 3가지 구성요소

* Node: 수학적 연산을 담당, 데이터의 입출력을 담당
* Edge: 동적 데이터를 노드로 실어나르는 역할을 담당
* Tensor: 다차원 배열 형태의 동적 데이



## 2. Tensorflow 설치

{% hint style="info" %}
Anaconda prompt 관리자 권한 실행 &gt; 가상환경 진입 &gt;  **pip install tensorflow==1.5.0** 
{% endhint %}

```python
pip install tensorflow==1.5.0
# 그냥 설치하면 많이 바뀐 최신 버전이 설치되기 때문에 기존 버전을 설치

import tensorflow as tf
# 설치 후 python import
```

 

## 3. Tensorflow 사용 

#### \[코드 입력\]  

```python
import tensorflow as tf

# 그래프를 그려주는  tensorflow
node1 = tf.constant("Hello World!")

# graph를 실행시키기 위해서는 runner 필요
# session이라고 불리는 runner 생성
sess = tf.Session()

# run 함수를 이용해서 해당 node 실행

print(sess,run(node1))
# print 했을 때, 앞에 붙는 b는 bite string의 약자
# 일반적인 문자열 처리를 원하면 decode 필요

print(sess.run(node1)decode())
```

#### \[결과 출력\] 

```python
10.0
[10.0, 20.0]
30.0
```

#### \[코드 입력\] 

```python
# 위의 node는 실행 시점에 값이 정해져 있음
# constant(상수)이기 때문!
# 만약 ndoe1,2에 대한 값을 직접 입력해서 실행하고 싶다면?

import tensorflow as tf
node4 = tf.placeholder(dtype=tf.float32)
node5 = tf.placeholder(dtype=tf.float32)

node6 = node4 + node5
sess = tf.Session()

# node 1,2에 값을 feed하되 dict 사용
result = sess.run(node6, feed_dict={node4: input(), node: input()})
print(f'덧셈결과: {result}')
```

#### \[결과 출력\]

```python
10
40
덧셈결과: 50.0
```



