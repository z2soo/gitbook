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

![LIST heading &#xC124;&#xC815; &#xC804;](../.gitbook/assets/image%20%2862%29.png)

![LIST heading &#xC124;&#xC815; &#xD6C4;](../.gitbook/assets/image%20%2861%29.png)

### 

### Line-Size 설정 

Output List의 넒이를 지정한다. 0 또는 default 값은 표준 길이로 설정된다. 

```sql
# List 넓이 30 설
REPORT ZSTUDY_012_REPORT_PROGRAM_01 line-size 30.
WRITE 'LIST HEADING TEST'.
```

![Line size &#xC124;&#xC815; &#xC804;](../.gitbook/assets/image%20%2864%29.png)

![Line size &#xC124;&#xC815; &#xD6C4;](../.gitbook/assets/image%20%2865%29.png)



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

| Option | Occur |
| :--- | :--- |
| DEFAULT '기본값' | 기본값 설정 |
| TYPE 데이터타입\(길이\) | 타입과 길이 설정REPO |

 

### SELECT-OPTIONS

### SELECTION-SCREEN



## 5. Message ID

