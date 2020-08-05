---
description: >-
  조회된 화면에서 데이터를 수정하여 저장하고, 저장 과정에 대해 신호등 표시로 보이게끔 기능을 추가해본다. 이 때, 데이터 수정 및 저장하는
  구문은 BAPI Function을 사용한다.
---

# 수정 및 저장 기능 추가

## 1. Screen status 기능 추가

Screen 설정 중 SET PF-STATUS 에서 Function에 대한 아이콘과 Function code를 설정해준다. 

![Screen 0100 &amp;gt; PBO &amp;gt; SET PF-STATUS](../../.gitbook/assets/image%20%28309%29.png)

Function code에 따른 action을 module로 작성해서 PAI에 작성해준다. 

![Screen 0100 &amp;gt; PAI &amp;gt; USER\_COMMAND\_0100](../../.gitbook/assets/image%20%28287%29.png)



## 2. 수정 및 저장 기능

조회된 화면에서 수정이 가능한 데이터는 전화번호 및 생성자이다. 데이터를 수정한 후 저장 아이콘을 눌렀을 때, 저장이 되기 위해서 다음 과정을 생각해줘야 한다.

1. 필요한 데이터 및 WA 선언 
2. 변경 데이터 유무 체크
3. BAPI Function 위한 데이터 구성
4. BAPI Function 수행
5. 성공/실패에 따른 결과를 ALV에 적용



### 1\) 필요한 데이터 및 WA 선언

![Form &amp;gt; SAVE\_DATA](../../.gitbook/assets/image%20%28298%29.png)



### 2\) 변경 데이터 유 체크

변경 데이터 유무를 체크하여, 없는 경우에는 메세지를 띄우게 한다. 변경된 데이터가 있는 경우는 이후 로직을 수행하여 변경 데이터를 저장하도록 한다. 

이 때, internal table GT\_DISP를 읽어서 

![Form &amp;gt; SAVE\_DATA](../../.gitbook/assets/image%20%28310%29.png)



### 3\) POP\_UP\_TO\_CONFIRM

POP\_UP\_TO\_CONFIRM Function을 활용해서 변경 내역에 대해 다시 한 번 는 창을 띄워본다. 

![Form &amp;lt; USER\_CONFIRM](../../.gitbook/assets/image%20%28294%29.png)



\*\*\*\*





