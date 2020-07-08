---
description: SAP에서 제공하는 교육 내용과 Easy ABAP 교재 참조
---

# Data element

## 1. Data element

Data element는 테이블 필드의 모든 정보를 가진 ABAP Dictionary 오브젝트이다. 즉, 테이블 필드의 기술적인 속성을 정의하며, Domain을 참조할 수 있으며 필드에 의해 참조 또한 될 수 있다. 다음은 Domain, Data element, Field의 관계를 명시적으로 보여준다. 

![&#xCD9C;&#xCC98; Easy ABAP](../../.gitbook/assets/image%20%2822%29.png)



## 2. Data element 생성

{% hint style="info" %}
T-code SE11 &gt; Data type &gt; Data element 명 입력 &gt; Create &gt; Data element 
{% endhint %}

![T-code SE11](../../.gitbook/assets/image%20%2826%29.png)

![Check Data element](../../.gitbook/assets/image%20%2817%29.png)

![Data element &amp;gt; Data type](../../.gitbook/assets/image%20%286%29.png)

### Data type 설정

상세 내용은 아래에 기술

### Field label 설정

![Data element &amp;gt; Field label](../../.gitbook/assets/image%20%2840%29.png)

Short, Medium, Long 필드 라벨은 스크린 필드의 텍스트를 지정할 때 사용된다.  
Heading 필드 라벨은 List 프로그램의 Header row에 조회된다. 

### Search Help & Parameter ID

해당 내용은 이후에 학습



## 3. Data element & Elementary type

ABAP Dictionary의 필드 속성을 정의하기 위한 Data element의 기술적 속성 Elementary Type는 두 가지 방법으로 정의될 수 있다.

* Domain : Domain을 입력하여 설정된 속성을 정의
* Built-in type : 직접 Data type/Elementary type 정의

Domain은 ABAP Dictionary에 독립적으로 존재하는 Repository object로써 하나의 Domain을 가지고 여러 Data element 정의가 가능하다.

기본 데이터 타입인 ABAP Type 중 자주 사용되는 것을 ABAP Dictionary에서 미리 선언한 것이 Data type\(ABAP Dictionary Type, Elementary Type\)이며, 이를 가지고 직접 선언할 수도 있다.   
이 경우 사용 가능한 종류는 다음과 같다. 

| Dict.Type | Meaning | Max length n | ABAP Type |
| :--- | :--- | :--- | :--- |
| DEC | Calculation/amount field | 1-17 | P\(\(n+1\)/2\) |
| INT1 | Single-bite integer | 3 | Internal only |
| INT2 | Two-bite integer | 5 | Internal only |
| INT4 | Four-bite integer | 10 | l |
| CURR | Currency field | 1-17 | P\(\(n+1\)/2\) |
| CUKY | Currency key | 5 | C\(5\) |
| QUAN | Quantity | 1-17 | P\(\(n+1\)/2\) |
| UNIT | Unit | 2-3 | C\(n\) |
| PREC | Accuracy | 16 | Internal only |
| FLTP | Floating point number | 16 | F\(8\) |
| NUMC | Numeric text | 1-255 | N\(n\) |
| CHAR | Character | 1-255 | C\(n\) |
| LCHAR | Long character | 256-max | C\(n\) |
| STRING | String of Variable length | 1-max | String |
| RAWSTRING | Byte sequence of Variable length | 1-max | Xstring |
| DATS | Date | 8 | D |
| ACCP | Accounting period YYYYMM | 6 | N\(6\) |
| TIMS | Time HHMMSS | 6 | T |
| RAW | Byte sequence | 1-255 | X\(n\) |
| LRAW | Long byte sequence | 256-max | X\(n\) |
| CLNT | Client | 3 | C\(3\) |
| LANG | Language | internal 1, external 2 | C\(1\) |

