---
description: >-
  조회된 화면에서 데이터를 수정하여 저장하고, 저장 과정에 대해 신호등 표시로 보이게끔 기능을 추가해본다. 이 때, 데이터 수정 및 저장하는
  구문은 BAPI Function을 사용한다.
---

# 수정 기능 추가

## 1. Screen status 기능 추가

Screen 설정 중 SET PF-STATUS 에서 Function에 대한 아이콘과 Function code를 설정해준다. 

![Screen 0100 &amp;gt; PBO &amp;gt; SET PF-STATUS](../../.gitbook/assets/image%20%28316%29.png)

Function code에 따른 action을 module로 작성해서 PAI에 작성해준다. 

![Screen 0100 &amp;gt; PAI &amp;gt; USER\_COMMAND\_0100](../../.gitbook/assets/image%20%28293%29.png)



## 2. 수정 기능 추가

> ALV에 조회된 화면에서 수정이 발생한 경우 신호등 색상을 노란색, 오류가 발생한 경우 빨간색으로 변경하고자 한다. ALV 데이터에서 변화가 생겼다는 정보를 담은 EVENT를 활용한다.

{% hint style="info" %}
CL\_GUI\_ALV\_GRID 클래스의 DATA\_CHANGED 이벤트 활
{% endhint %}



### 1\) Class 생성

ALV GRID에서 데이터 변경이 발생하엿을 때, HANDLE\_DATA\_CHANGED method를 실행하도록 선언해준다. 

![Class &amp;gt; LCL\_EVENT\_RECEIVER](../../.gitbook/assets/image%20%28286%29.png)

### 2\) Method 정의

위에서 생성한 HANDLE\_DATA\_CHANGED 이름의 method가 발생했을 때, 실행 method를 다음과 같이 정의해준다. 

{% hint style="info" %}
CL\_GUI\_ALV\_GRID 클래스의 MODIFY\_CELL 메소드 활용 
{% endhint %}

CL\_GUI\_ALV\_GRID 클래스의 MODIFY\_CELL 메소드를 불러서 사용하는데, 변경 데이터에 대한 값이 클래스 형태여서 혼란을 줄 수 있다. 따라서 이를 아얘 다른 변수\(ex. LT\_CHANGED\)로 선언하고 사용해도 된다. 

![Class &amp;gt; HANDLE\_DATA\_CHANGED](../../.gitbook/assets/image%20%28283%29.png)



### 3\) 참조 변수 선언

참조 변수는 이벤트를 참조해서 선언하고, TOP이 아닌 CLASS 선언 밑에 해준다. 

![Class &amp;gt; LCL\_EVENT\_RECEIVER](../../.gitbook/assets/image%20%28279%29.png)



### 4\) 객체 생성

선언한 참조 변수로 객체를 생성해준다. Display ALV 이전에 해주면 되고, 깔끔한 코드 정리를 위해 PERFORM으로 묶어 정의했다. 

![Screen 0100 &amp;gt; SET\_ALV\_0100](../../.gitbook/assets/image%20%28317%29.png)

![SET\_ALV\_0100 &amp;gt; SET\_EVENT](../../.gitbook/assets/image%20%28304%29.png)



### 5\) SET HANDLER 선언

Class를 사용하기 위한 마지막으로 SET HANDLER를 선언해준다. 

![SET\_ALV\_0100 &amp;gt; SET\_EVENT](../../.gitbook/assets/image%20%28282%29.png)





