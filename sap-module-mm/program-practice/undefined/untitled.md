---
description: >-
  인사 프로그램 실행을 위한 데이터, 테이블을 ABAP Database에 생성하고, Selection screen에 입력한 조회 조건에 맞는
  데이터를 확인할 수 있는 조회 스크린을 ALV를 활용하여 생성해본다.
---

# 데이터 및 조회 스크린 생성

## 1. 사원 데이터 생성

> 인사 프로그램에서 사용할 데이터 베이스 테이블을 생성하고 필요한 설정과 더불어 데이터를 입력해보도록 한다.

### 1\) Database table 생성 

{% hint style="info" %}
T-code SE11 &gt; Database table &gt; Create
{% endhint %}

사원 테이블과 필요한 사원 마스터 정보 다음 양식에 맞춰 생성해보도록 한다. 

![&#xC0DD;&#xC131;&#xD560; &#xD14C;&#xC774;&#xBE14; &#xC815;&#xBCF4;](../../../.gitbook/assets/image%20%28168%29.png)

![T-CODE SE11 &amp;gt; DB Table &#xC0DD;&#xC131;](../../../.gitbook/assets/image%20%28186%29.png)

![DB Table &#xC0DD;&#xC131;](../../../.gitbook/assets/image%20%28189%29.png)

![Currency &#xCC38;&#xC870; &#xD544;&#xB4DC; &#xC124;&#xC815;](../../../.gitbook/assets/image%20%28173%29.png)

![Delivery and Maintenance &#xC124;&#xC815;](../../../.gitbook/assets/image%20%28155%29.png)

테이블 정보를 가지고 위와 같이 Database table을 생성하고 Currency 참조 필드 및 Display/Maintenance를 설정해준다. 테이블 속성 설정 시, 이왕이면 built-in type으로 직접 data type과 length를 입력하기보다 data element를 생성하여 이를 참조하도록 만들어준다. 즉, data element도 생성해줘야 한다. 이 때, 비고에 range가 존재하는 속성들은 domain을 필수적으로 만들어준다. 이를 통해 domain 값에 따른 range 값을 연결할 수 있기 때문이다. 예를 들어 직급이 A로 표시되었더라도 이것이 대표하는 값이 대표이사임을 알 수 있도록 정보가 필요하다.  



### 2\) Domain 생성

{% hint style="info" %}
T-code SE11 &gt; Domain &gt; Create 또는 Data element 더블 클릭
{% endhint %}

부서, 직급, 재직 구분 속성에 대해서 domain은 필수적이며, 자택 주소와 근무지주소, 퇴사일과 입사일 또한 동일한 데이터 타입, 속성을 가지기 때문에 도메인을 생성해 공동으로 사용 가능하다. 

대표로 직급에 대한 도메인을 생성하는 과정을 보이면 다음과 같다. 동일한 과정으로 나머지 속성에 대한 도메인 또한 생성해주도록 한다. 

![Domain &amp;gt; Definition](../../../.gitbook/assets/image%20%28191%29.png)

Definition 영역에서 데이터의 타입과, 길이에 대해 설정을 해준다. 

![Domain &amp;gt; Value range](../../../.gitbook/assets/image%20%28167%29.png)

Domain의 Value range 영역에서 각각 정해진 Fixed Value의 값과 그 값이 의미하는 것이 무엇인지에 대해 기술해준다. 



### 3\) Record structure 생성 및 추가 

해당 데이터에 대해 누가 언제 무엇을 어떻게 변경하였는지 등에 대한 정보를 담을 수 있는 structure를 생성해주도록 한다. 해당 record structure를 이루는 component는 이미 정의된 데이터를 사용하면 된다. 

생성한 record structure를 이전에 만든 table에 include로 넣어줌으로써 해당 테이블을 수정한 기록에 대한 정보를 담을 수 있도록 한다. 

{% hint style="info" %}
ERDAT, ERZET, ERNAM, AEDAT, AEZET, ZENAM
{% endhint %}

![Record structure &#xC0DD;&#xC131;](../../../.gitbook/assets/image%20%28156%29.png)

![Record structure &amp;gt; Include](../../../.gitbook/assets/image%20%28182%29.png)



### 4\) Database table 데이터 추가

{% hint style="info" %}
T-code SE16N 
{% endhint %}

![T-code SE16 ](../../../.gitbook/assets/image%20%28162%29.png)

Table 이름으로 검색하여 row를 추가해 데이터를 추가해준다. 만약, 데이터 추가가 안된다면 테이블 설정에서 Delivery and Maintenance 부분의 editing이 allow로 되어있는지 확인해본다. 



## 2. 사원 데이터 조회 스크린 생성

> 사원번호, 부서, 입사일, 직급, 재직구분 값을 selection screen을 통해 입력받고, 이를 기준으로 Database에 생성한 인사 테이블에서 해당되는 사원 정보를 읽어서 ALV를 통해 결과화면을 보이도록 한다.   
> 조회화면과 결과화면에 대한 내용은 구현할 스크린 정보를 참조하자.

![&#xAD6C;&#xD604;&#xD560; &#xC0AC;&#xC6D0; &#xB370;&#xC774;&#xD130; &#xC870;&#xD68C; &#xC2A4;&#xD06C;&#xB9B0;](../../../.gitbook/assets/image%20%28195%29.png)



### 1\) 조회화면 생성 \(Selection Screen\)

![Main program](../../../.gitbook/assets/image%20%28165%29.png)

![TOP](../../../.gitbook/assets/image%20%28192%29.png)

![Selection-options](../../../.gitbook/assets/image%20%28201%29.png)

#### Text symbol & Selection texts 설정

{% hint style="info" %}
상단 메뉴 &gt; Text elements &gt; Selection Texts & Text symbols
{% endhint %}

Selection-options에서 값을 받는 변수명은 PA\_1, PA\_2, PA\_3, PA\_4, PA\_5으로 되어있지만, 화면상으로는 사원번호, 부서, 입사일, 직급, 재직구분으로 보이기를 원한다. 이를 위해 상단 메뉴의 Text elements 혹 Text-100으로 작성한 text symbol을 더블 클릭하여 들어가서 다음과 같이 설정하도록 한다. 

![Text symbol](../../../.gitbook/assets/image%20%28196%29.png)

![Selection texts](../../../.gitbook/assets/image%20%28188%29.png)

모든 변경 사항을 저장 및 실행하면 다음과 같은 조회용 사원 정보 입력창을 확인할 수 있다. 

![&#xC870;&#xD68C;&#xC6A9; &#xC0AC;&#xC6D0; &#xC815;&#xBCF4; &#xC785;&#xB825;&#xCC3D;](../../../.gitbook/assets/image%20%28184%29.png)



### 2\) 결과화면 생성 \(ALV\) 

#### Screen 생성

Screen 100번을 생성하고, layout에서 control area를 생성해준다. 

![Screen 100](../../../.gitbook/assets/image%20%28169%29.png)

![Screen 100 Layout](../../../.gitbook/assets/image%20%28202%29.png)



#### Status 및 Exit 설정 

Screen 100에 대한 status와 exit을 설정해준다. 이 부분에 대한 상세 설명은 넘어가도록 한다. 

![Screen 100](../../../.gitbook/assets/image%20%28170%29.png)

![Screen 100 Status](../../../.gitbook/assets/image%20%28164%29.png)

![Screen 100 Exit](../../../.gitbook/assets/image%20%28180%29.png)



#### ALV container & grid 인스턴스 선언 

![](../../../.gitbook/assets/image%20%28177%29.png)

#### 

#### ALV container & grid 오브젝트 선언 

![](../../../.gitbook/assets/image%20%28176%29.png)



#### ALV display 설정

![](../../../.gitbook/assets/image%20%28171%29.png)



#### Internal table 선언 및 Select 

GT\_ITAB은 조회 조건으로 사원 데이터를 조회한 결과를 담는 테이블로써 결론적으로 ALV 화면으로 보여주고 싶은 데이터이다.  

![GT\_ITAB &#xC120;&#xC5B8;](../../../.gitbook/assets/image%20%28179%29.png)

GT\_ITAB에 넣어서 보여주고자 하는 데이터를 가져오는 구문을 작성해주고, select가 끝난 후에 100번 화면을 호출하는 구문 또한 작성해준다.

![Select &amp; Call screen](../../../.gitbook/assets/image%20%28163%29.png)



### 3\) 화면 확인 및 사이즈 조정

지금까지 작성한 코드로 다음과 같은 결과를 확인할 수 있다. 

![&#xC870;&#xD68C;&#xD654;&#xBA74;](../../../.gitbook/assets/image%20%28185%29.png)



![](../../../.gitbook/assets/image%20%28203%29.png)













도메인 텍스트 가져오???

//

FULL SCREEN

![](../../../.gitbook/assets/image%20%28197%29.png)

![](../../../.gitbook/assets/image%20%28166%29.png)

EDITING 부분을 최대로 해두면 항상 FULL SCREEN이 된다. 

![](../../../.gitbook/assets/image%20%28200%29.png)

LAYOUT 부분도 최대로 해눈더, 

//

![](../../../.gitbook/assets/image%20%28194%29.png)

생성된 버튼에 대한 USER COMMAND 생성

//



![](../../../.gitbook/assets/image%20%28178%29.png)

통화키를 참조하도록 하여 기본급 SALARY를 설정: GS\_0200-WAERS

