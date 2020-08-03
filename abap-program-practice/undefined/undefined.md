---
description: >-
  조회 스크린에서 조회되는 값 중 부서, 직급, 재직구분의 도메인 값에 따른 range value 즉, 실제 의미하는 도메인 텍스트 데이터를
  가져와 추가해준다.
---

# 도메인 값 추가

> 버튼 및 팝업 창 생성한 부분  
> ZR025\_0010\_EX03 파일이 버튼 및 정보 입력 팝업창 생성 완료 한 파일



## 1. Domain range value 가져오

### 1\) Structure 및 Table 선언

{% hint style="info" %}
Domain value, text 값은 DD07T 테이블에서 가져온다.
{% endhint %}

도메인 value에 따른 text 값을 담기 위한 structure와 table이 필요하다. Domain value와 domain text의 값을 가지는 table을 부서, 직급, 재직 구분 각각 만들어주도록 한다. 

![](../../.gitbook/assets/image%20%28235%29.png)



### 2\) Domain text 가져오기 

Main program의 기존 GET\_DATA 부분을 도메인 데이터와 인사 데이터를 각각 가져오고 이를 합쳐주는 세 개의 단계로 나누어 실행한다. 

![](../../.gitbook/assets/image%20%28226%29.png)

#### 

#### GET\_DOMAIN\_TEXT

DD07T 테이블에서 값을 읽어들이고, 위에서 선언한 부서, 직급, 재직구분 별 Domain table에 넣어주도록 한다. 

![GET\_DATA &amp;gt; GET\_DOMAIN\_TEXT](../../.gitbook/assets/image%20%28225%29.png)

#### 

#### GET\_EMPLOYEE\_MASTER

![GET\_DATA &amp;gt; GET\_EMPLOYEE\_MASTER](../../.gitbook/assets/image%20%28229%29.png)



#### MERGE\_DATA



#### 

## 2. Field catalog 설정 

### 1\) Field catalog 선언

{% hint style="info" %}
Field catalog는 LVC\_T\_FCAT, LVC\_S\_FCAT을 참조하여 선언한다. 
{% endhint %}

Domain text 값을 추가적으로 보여줄 것이기 때문에 ALV 출력 틀 또한 변경해줘야 한다. 즉, Domain text 값을 가지고 있는 형태의 Field catalog를 선언해준다.

![Field catalog &#xAD6C;&#xC870;&#xCCB4; &#xC120;&#xC5B8; &amp;gt; GT\_FCAT, GS\_FCAT](../../.gitbook/assets/image%20%28234%29.png)



### 2\) Field catalog 구조 설정

{% hint style="info" %}
Field catalog structure에 값을 넣고 table에 append하는 방식 활용
{% endhint %}

선언한 Field catalog 구조에 어떤 열을 어떤 이름으로 표현할 것인지 설정해준다. 그 외에 참조, KEY 설정, 숨김 등에 대한 설정도 가능하다. 해당 과정은 ALV 생성 중 ALV Display 이전에 진행한다. 

![Screen 0100 &amp;gt; SET\_ALV](../../.gitbook/assets/image%20%28232%29.png)

![Field catalog &#xC124;&#xC815; - 1](../../.gitbook/assets/image%20%28227%29.png)

![Field catalog &#xC124;&#xC815; - 2](../../.gitbook/assets/image%20%28224%29.png)

![Field catalog &#xC124;&#xC815; - 3](../../.gitbook/assets/image%20%28230%29.png)



### 3\) Field catalog 적용

생성한 Field catalog를 ALV Display 부분에 적용시켜준다. 이 때, I\_STRUCTURE\_NAME에 설정해 둔 부분은 주석처리함을 잊지 말자.

![Screen 0100 &amp;gt; SET\_ALV &amp;gt; SET\_DISPLAY](../../.gitbook/assets/image%20%28233%29.png)

















생성된 버튼에 대한 USER COMMAND 생성

//



![](../../.gitbook/assets/image%20%28178%29.png)

통화키를 참조하도록 하여 기본급 SALARY를 설정: GS\_0200-WAERS

