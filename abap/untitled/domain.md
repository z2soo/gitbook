---
description: SAP에서 제공하는 교육 내용과 Easy ABAP 교재 참조
---

# Domain

## 1. Domain

Domain은 필드의 기술적인 속성을 정의한다. 이는 ABAP Dictionary 상에서 참조하는 것이 없는 최소의 단위이다. Domain은 Data element에 할당되어 사용되며, Data element는 테이블 필드의 속성을 정의하기 위해 사용된다. 이러한 관계를 표현한 것이 아래 그림이며 이를 Two-level Domain Concept라고 한다. Table과 Structure는 Domain이 할당된 Data element 사용이 가능하다.  단, 같은 Domain을 참조하는 테이블 필드는 Domain이 변경되면 변경 사항을 자동을 반영한다.

![&#xCD9C;&#xCC98; Easy ABAP](../../.gitbook/assets/image%20%2843%29.png)



## 2. Domain 생성

{% hint style="info" %}
T-code SE11 &gt; Domain &gt; Domain명 입력 &gt; Create
{% endhint %}

![T-code SE11](../../.gitbook/assets/image%20%285%29.png)

![Domain &amp;gt; Definition](../../.gitbook/assets/image%20%2818%29.png)

### Definition 설정

| Option | Explanation |
| :--- | :--- |
| Data type | 입력 값의 데이터 타입 설정 |
| No. Characters | 입력 값의 데이터 길이 설정 |
| Decimal Places | 숫자 타입인 DEC, FLTP, QUAN, CURR 경우 소수 자릿수 설정 |
| Lowercase | 문자 타입일 경우 활성화되며, 체크시 대소문자 구별 설정 |
| \(Conversion\) Routine | 데이터가 테이블에 저장되는 값, 조회되는 값 변경 설 |

![Domain &amp;gt; Value Range &amp;gt; Single Vals](../../.gitbook/assets/image%20%2834%29.png)

![Domain &amp;gt; Value Range &amp;gt; Intervals, Value Table](../../.gitbook/assets/image%20%2842%29.png)

### Value Range 설정 

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Explanation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Single Value</td>
      <td style="text-align:left">
        <p>&#xC0AC;&#xC6A9;&#xC790;&#xAC00; &#xC785;&#xB825; &#xAC00;&#xB2A5;&#xD55C;
          &#xAC12;&#xC744; &#xACE0;&#xC815;&#xD558;&#xC5EC; Input Check &#xC2E4;&#xD589;</p>
        <p>GET_DOMAIN_VALUES &#xD568;&#xC218;&#xB97C; &#xD1B5;&#xD574; Fixed value&#xB97C;
          Range &#xBCC0;&#xC218;&#xC5D0; &#xC800;&#xC7A5; &#xAC00;&#xB2A5;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Intervals</td>
      <td style="text-align:left">
        <p>&#xC815;&#xD574;&#xC9C4; &#xBC94;&#xC704; &#xAC12; &#xB0B4;&#xC5D0; &#xC874;&#xC7AC;&#xD558;&#xB294;
          &#xAC12;&#xB9CC; &#xC785;&#xB825; &#xAC00;&#xB2A5;&#xD558;&#xB3C4;&#xB85D;
          &#xC124;&#xC815;</p>
        <p>CHAR, NUM, DEC, INT &#xAC19;&#xC740; &#xC720;&#xD615;&#xB9CC; &#xC0AC;&#xC6A9;
          &#xAC00;&#xB2A5;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Value Table</td>
      <td style="text-align:left">Value Table &#xC874;&#xC7AC;&#xD558;&#xB294; Domain&#xC744; &#xCC38;&#xC870;&#xD558;&#xB294;
        &#xD544;&#xB4DC;&#xB294;
        <br />Foreign key &#xC815;&#xC758; &#xC2DC;, Value Table&#xC744; &#xC790;&#xB3D9;&#xC73C;&#xB85C;
        Check Table&#xB85C;&#xC11C; &#xC81C;&#xC548;</td>
    </tr>
  </tbody>
</table>

Value Table과 Check Table은 다른 것으로 구분해야 한다.   
다음은 Check Table과 차이점을 보이는 Value Table의 특징이다.

* Domain level에서 정의됨
* Possible entry 기능 및 Input check 기능 없음
* Value Table이 설정된 필드는 Foreign Key가 설정되야 테이블에서 Check Table 역할 가능
* Domain에 Value Table이 존재하면, 표준 테이블 데이터가 어느 테이블에 저장되는지 쉽게 알 수 있음
* 표준 테이블의 key 필드는 대부분 Value Table 설정 있



## 3. Domain & Conversion Routine

Domain 생성 중 Definition 설정에서 언급된 부분이다. Conversion Routine 설정을 통해 입력 값, 입력 값을 가지고 테이블에 저장되는 값, 저장된 값을 가지고 조회하는 값에 대한 형태를 변경할 수 있다. 즉, 실제 화면에서 보이는 데이터와 테이블에 저장된 데이터의 포맷이 다를 경우 사용한다. 아래의 그림은 이 내용을 명시적으로 보여준다. 

![&#xCD9C;&#xCC98; Easy ABAP](../../.gitbook/assets/image%20%2811%29.png)

예를 들어, Database에 저장되는 사번의 형태는 다섯 자리지만, 입력 값과 조회 값은 세 자리만을 보이는 경우 이에 대한 입출력 변환을 수행해준다. 

### Conversion Routine 설정 및 정의

![Domain &amp;gt; Definition](../../.gitbook/assets/image%20%289%29.png)

Conversion Routine 설정은 Domain &gt; Definition 설정에서 가능하며, 이것이 설정된 Domain을 참조하는 필드는 해당 Routine을 수행한다. 

Conversion Routine은 다음 같은 구문의 두 개의 Function Module과 5자리 이름으로 정의된다.   
0 값을 처리하기 위한 Conversion Routine은 ALPHA 함수를 사용하면 된다.

```sql
# CONVERSION 정의
CONVERSION_EXIT_5자리이름_INPUT
CONVERSION_EXIT_5자리이름_OUTPUT

# CONVERSION 사용
CONVERSION_EXIT_ALPHA_INPUT
CONVERSION_EXIT_ALPHA_INPUT
```

입력값에 대한 data type과 길이를 정한다. 숫자 타입\(DEC, FLTP, QUAN, CURR\) 경우 소수 자릿수\(Decimal places\)를 지정하고, Sign 옵션을 통

