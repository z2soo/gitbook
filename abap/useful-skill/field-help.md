---
description: 'Field Help, 즉 F1을 생성하고 변경해본다.'
---

# Field Help

## 1. Field Help 생성하기 

사용자가 화면에서 F1을 누르거나 Help 아이콘을 클릭하면, 현재 커서가 존재하는 필드의 텍스트 도움말이 조회된다. ABAP Dictionary 필드의 Data element documentation이 생성되어 있다면 자동으로 첨부된다. 해당 문서를 변경 및 생성하는 경우에는 다음 과정을 거친다.

{% hint style="info" %}
Screen &gt; Layout &gt; Documentation &gt; Data Element Supplement Documentation
{% endhint %}

우선 생성된 Screen layout에서 도움말을 넣고자 하는 필드를 선택한다.  
그 다음 상단 Goto &gt; Documentation &gt; Data Element Supplement Documentation을 클릭한다.

이 때, Data Element Documentation\(D\)는 ABAP Dictionary 레벨에서 도움말을 생성하는 것이며, Data Element Supplement Documentation\(A\)는 해당 프로그램 스크린 한정으로 생성하는 것이다. 

![Goto &amp;gt; Documentation &amp;gt; A](../../.gitbook/assets/image%20%28146%29.png)

해당 데이터 element에 스크린 100번 정보를 추가하여 생성한다.   
스크린 100번에서 사용할 것이기 때문이다.

![Screen Supplement](../../.gitbook/assets/image%20%28150%29.png)

CBO가 아닌 표준 data element인 경우에는 아래와 같은 팝업창이 열린다. Modification name을 입력한다.

![Modification name](../../.gitbook/assets/image%20%28145%29.png)

아래와 같은 화면에서 도움말을 작성하고 활성화하면 화면 필드의 Documentation이 생성된다.

![Documentation](../../.gitbook/assets/image%20%28141%29.png)

스크린의 Flow logic 부분에 POH 이벤트를 추가한다.  
Module 부분은 선택 조건으로 도움말 수행 전 추가하고 싶은 로직을 구현할 수 있다. 

{% hint style="info" %}
FIELD &lt;필드명&gt; \[MODULE &lt;모듈명&gt;\] WITH &lt;번호&gt;.
{% endhint %}

![Screen flow logic](../../.gitbook/assets/image%20%28142%29.png)

저장 및 활성화 후, 해당 field에서 F1 키를 누르면 앞서 작성한 도움말 창이 열리게 된다. 

![](../../.gitbook/assets/image%20%28152%29.png)



## 2. Field Help 불러오기 

{% hint style="info" %}
HELP\_OBJECT\_SHOW\_FOR\_FIELD
{% endhint %}

새로운 도움말을 생성하지 않고 기존에 존재하는 ABAP Dictionary의 Data Element 도움말을 사용하고자 할 때, 다음과 같은 Module 을 사용한다.

![](../../.gitbook/assets/image%20%28151%29.png)

해당 Module에는 HELP\_OBJECT\_SHOW\_FOR\_FIELD 함수를 사용하여 참조할 테이블과 필드를 설정해준다.

![MODULE HELP\_REQ](../../.gitbook/assets/image%20%28138%29.png)

그 결과 다음과 같이 추가된 도움말을 확인할 수 있다.

![](../../.gitbook/assets/image%20%28140%29.png)

