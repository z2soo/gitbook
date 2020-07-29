---
description: SAP에서 제공하는 교육 내용과 Easy ABAP 교재 참조
---

# Program 구조 - 선언

## 1. Report program 구조

Report program은 3가지 구조로 이루어지며 여에서는 프로그램 및 데이터 선언에 대해 다룬다.

* 프로그램 및 데이터 선언 : 데이터 선언부와 조회 선택 화면 \(SELECTION SCREEN\)
* Event : 실행 시점까지의 Event
* List process event : 데이터를 뿌려주는 List Event

```sql
# 1. 프로그램 및 데이터 선언
REPORT pgm_id.
TABLES: SFLIGHT.
DATA: I_CARRID TYPE SFLIGHT-CARRID.

# SELECTION SCREEN
SELECT-OPTIONS: SEL_CARR FOR SFLIGHT-CARRID.
PARAMETERS: P_CARR LIKE SFLIGHT-CARRID.
```

```sql
# 2. 이벤트
INITIALIXATION.
AT SELECTION-SCREEN.
START-OF-SELECTION.
    <SQL 구문>
END-OF-SELECITON.
```

```sql
# 3. List process 이벤트
TOP-OF-PAGE.
END-OF-PAGE.
AT LINE-SELECTION.
AT PF<NN>.
AT USER-COMMAND.
```



## 2. Program 선언

프로그램 선언문은 REPORT &lt;프로그램 이름&gt; 기본 구조 외에 추가 옵션이 존재한다. 

{% hint style="info" %}
* REPORT &lt;프로그램 이름&gt; NO STANDARD PAGE HEADING.
* REPORT &lt;프로그램 이름&gt; LINE-SIZE 숫자.
* REPORT &lt;프로그램 이름&gt; MESSAGE-ID &lt;message-id&gt;
{% endhint %}



### List Heading 설정 

프로그램을 실행한 리스트 화면에 프로그램 이름을 기본 Heading으로 사용할지에 대해 설정한다. 

```sql
# List heading 미사
REPORT ZSTUDY_012_REPORT_PROGRAM_01 NO STANDARD PAGE HEADING.
WRITE 'LIST HEADING TEST'.
```

![LIST heading &#xC124;&#xC815; &#xC804;](../../../.gitbook/assets/image%20%2862%29.png)

![LIST heading &#xC124;&#xC815; &#xD6C4;](../../../.gitbook/assets/image%20%2861%29.png)

### 

### Line-Size 설정 

Output List의 넒이를 지정한다. 0 또는 default 값은 표준 길이로 설정된다. 

```sql
# List 넓이 30 설
REPORT ZSTUDY_012_REPORT_PROGRAM_01 line-size 30.
WRITE 'LIST HEADING TEST'.
```

![Line size &#xC124;&#xC815; &#xC804;](../../../.gitbook/assets/image%20%2864%29.png)

![Line size &#xC124;&#xC815; &#xD6C4;](../../../.gitbook/assets/image%20%2865%29.png)



### Message ID 설정 

ABAP 프로그램에서 사용할 MESSAGE ID를 선언하며, 뒤에서 자세히 다뤄본다. 

```sql
REPORT ZSTUDY_012_REPORT_PROGRAM_01 MESSAGE-ID <message-id>.
```



## 3. Data 선언 

프로그램에서 사용할 테이블과 데이터를 선언한다. 복잡한 프로그램에서는 INCLUDE TOP을 사용한다.

```sql
# Data 선언
TABLES: SFLIGHT.                        #프로그램 내에서 사용하는 TABLE 형태의 WA
DATA: IV_CARRID TYPE SFLIGHT-CARRID.
```



## 4. SELECTION SCREEN 

프로그램의 조회 조건을 입력할 수 있는 SELECTION SCREEN을 생성한다. 이는 사용자와의 상호 작용을 위한 INPUT 필드와 같은 선택 조건 입력 화면을 제공하며, Report program 실행시 자동 생성된다.   
Report program에서 SELECTION SCREEN 구문은 INCLUDE TOP에 포함하는 것이 좋다.



### PARAMETERS

사용자가 값을 입력할 수 있는 Input field를 정의한다. 타입 미설정 시, CHAR 1자리 타입이 정의된다.  
Parameter에 대한 옵션은 다음이 존재한다. 

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Occur</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">DEFAULT &apos;&#xAE30;&#xBCF8;&#xAC12;&apos;</td>
      <td style="text-align:left">&#xAE30;&#xBCF8;&#xAC12; &#xC124;&#xC815;</td>
    </tr>
    <tr>
      <td style="text-align:left">TYPE &#xB370;&#xC774;&#xD130;&#xD0C0;&#xC785; (&#xC22B;&#xC790;)</td>
      <td
      style="text-align:left">&#xD0C0;&#xC785;&#xACFC; &#xAE38;&#xC774; &#xC124;&#xC815;</td>
    </tr>
    <tr>
      <td style="text-align:left">LENGTH &#xC22B;&#xC790;</td>
      <td style="text-align:left">Type C, N, X, P &#xAE38;&#xC774; &#xC124;&#xC815;</td>
    </tr>
    <tr>
      <td style="text-align:left">DECIMALS &#xC22B;&#xC790;</td>
      <td style="text-align:left">&#xC18C;&#xC218;&#xC810; &#xC790;&#xB9AC;&#xC218; &#xC124;</td>
    </tr>
    <tr>
      <td style="text-align:left">LIKE &#xC624;&#xBE0C;&#xC81D;&#xD2B8;</td>
      <td style="text-align:left">&#xC624;&#xBE0C;&#xC81D;&#xD2B8;&#xC640; &#xB3D9;&#xC77C;&#xD55C; &#xD0C0;&#xC785;
        &#xC120;&#xC5B8;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;MEMORY ID &#xBA54;&#xBAA8;&#xB9AC;&#xBA85;</td>
      <td style="text-align:left">&#xBA54;&#xBAA8;&#xB9AC; &#xD30C;&#xB77C;&#xBBF8;&#xD130; &#xD560;</td>
    </tr>
    <tr>
      <td style="text-align:left">SEARCH HELP &#xC11C;&#xCE58; &#xD5EC;&#xD504;&#xBA85;</td>
      <td style="text-align:left">Search help&#xBA85; &#xC785;&#xB825;&#xC2DC; possible entry &#xC0DD;</td>
    </tr>
    <tr>
      <td style="text-align:left">MODIF ID &#xC2A4;&#xD06C;&#xB9B0; &#xADF8;&#xB8F9;</td>
      <td style="text-align:left">Screen-group &#xC9C0;&#xC815;&#xD558;&#xC5EC; &#xADF8;&#xB8F9;&#xBCC4;&#xB85C;
        &#xD654;&#xBA74; &#xC18D;&#xC131; &#xC81C;&#xC5B4;</td>
    </tr>
    <tr>
      <td style="text-align:left">NO-DISPLAY</td>
      <td style="text-align:left">&#xD654;&#xBA74;&#xC5D0; &#xBCF4;&#xC774;&#xC9C0; &#xC54A;</td>
    </tr>
    <tr>
      <td style="text-align:left">LOWER CASE</td>
      <td style="text-align:left">&#xB300;&#xC18C;&#xBB38;&#xC790; &#xAD6C;&#xBCC4; &#xC124;&#xC815;</td>
    </tr>
    <tr>
      <td style="text-align:left">OBLIGATORY</td>
      <td style="text-align:left">&#xD544;&#xC218;&#xAC12; &#xC124;&#xC815;</td>
    </tr>
    <tr>
      <td style="text-align:left">AS CHECKBOX</td>
      <td style="text-align:left">&#xCCB4;&#xD06C; &#xBC15;&#xC2A4;&#xB85C; &#xD45C;&#xD604;</td>
    </tr>
    <tr>
      <td style="text-align:left">RADIOBUTTON GROUP &#xBC84;&#xD2BC; &#xADF8;&#xB8F9;&#xBA85;</td>
      <td style="text-align:left">&#xB77C;&#xB514;&#xC624; &#xBC84;&#xD2BC; &#xADF8;&#xB8F9; &#xC124;&#xC815;</td>
    </tr>
    <tr>
      <td style="text-align:left">VISIBLE LENGTH &#xC22B;&#xC790;</td>
      <td style="text-align:left">&#xD544;&#xB4DC;&#xC758; &#xC77C;&#xBD80; &#xAE38;&#xC774;&#xAE4C;&#xC9C0;&#xB9CC;
        &#xD654;&#xBA74;&#xC5D0; &#xBCF4;&#xC774;&#xAC8C; &#xC124;&#xC815;</td>
    </tr>
    <tr>
      <td style="text-align:left">LIKE (&#xC624;&#xBE0C;&#xC81D;&#xD2B8;)</td>
      <td style="text-align:left">&#xD30C;&#xB77C;&#xBBF8;&#xD130; &#xB3D9;&#xC801; &#xC120;&#xC5B8;</td>
    </tr>
    <tr>
      <td style="text-align:left">AS LISTBOX</td>
      <td style="text-align:left">ABAP dictionary &#xD544;&#xB4DC;&#xC758; input help&#xC640; &#xC5F0;&#xACB0;&#xC2DC;
        list box&#xB85C; &#xBCF4;&#xC784;</td>
    </tr>
    <tr>
      <td style="text-align:left">USER-COMMAND ucom</td>
      <td style="text-align:left">
        <p>&#xCCB4;&#xD06C; &#xBC15;&#xC2A4;&#xC640; &#xB77C;&#xB514;&#xB3C4; &#xBC84;&#xD2BC;&#xC5D0;&#xB9CC;
          &#xC791;&#xC6A9;</p>
        <p>&#xD574;&#xB2F9; &#xBC84;&#xD2BC; &#xD074;&#xB9AD;&#xC2DC; user command
          &#xC218;&#xD589;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">AS SEARCH PATTERN</td>
      <td style="text-align:left">LDB&#xC5D0;&#xC11C; &#xC0AC;&#xC6A9;, search help key&#xAC12;&#xC73C;&#xB85C;
        itab &#xAD6C;&#xC131;</td>
    </tr>
    <tr>
      <td style="text-align:left">VALUE-REQUEST</td>
      <td style="text-align:left">LDB&#xC5D0;&#xC11C; &#xC0AC;&#xC6A9;, F4 VALUE HELP &#xCD94;&#xAC00;&#xD558;&#xAC8C;
        &#xD568;</td>
    </tr>
    <tr>
      <td style="text-align:left">HELP-REQUEST</td>
      <td style="text-align:left">
        <p>VALUE-REQUEST&#xC640; &#xC720;&#xC0AC;</p>
        <p>&#xD544;&#xB4DC; HELP &#xC0DD;&#xC131;</p>
      </td>
    </tr>
  </tbody>
</table>

```sql
REPORT Z_012_REPORT_PROGRAM_02.

DATA: L_FNAME(20) TYPE C.
PARAMETERS: P_1 DEFAULT 'A',
            P_2 TYPE char10,
            P_3 type c length 3 DEFAULT '123',
            P_4 DEFAULT '123.4567',
            P_5 like sflight-carrid,
            P_6 memory id scl,
            P_7 MATCHCODE OBJECT zcarrid,
            P_8 modif id mid,
            P_9 NO-DISPLAY,
            P_10 DEFAULT 'a' LOWER CASE,
            P_11 OBLIGATORY,
            P_12 as CHECKBOX,
            P_13 RADIOBUTTON GROUP radio,
            P_13_2 RADIOBUTTON GROUP radio,
            P_14(10) VISIBLE LENGTH 3 DEFAULT '12345678',
            P_15 like sflight-carrid Value CHECK,
            P_16 like (l_fname),
            p_17 like sflight-carrid as LISTBOX VISIBLE LENGTH 3,
            p_18 as CHECKBOX USER-COMMAND abc.
```

![&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC2E4;&#xD589; &#xD654;&#xBA74;](../../../.gitbook/assets/image%20%2867%29.png)



### SELECT-OPTIONS

하나의 값만 입력받을 수 있는 Input 필드인 PARAMETER와 달리, SELECT-OPTIONS은 2개의 필드를 통해서 조건 값\(Selection criteria\)을 입력받는다. 다음 옵션들이 존재한다. 

{% hint style="warning" %}
SELECT-OPTIONS는 항상 FOR 구문화 병행하며,   
FOR 이후 값은 TABLES로 선언된 테이블 필드나 DATA로 선언된 변수여야만 한다.
{% endhint %}



### SELECTION-SCREEN



## 5. Message ID

