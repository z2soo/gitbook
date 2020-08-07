---
description: >-
  BAPI와 마찬가지로 standard transaction을 흘리는 기능을 한다. BAPI를 사용하려면 해당 BAPI Function이
  있어야 하고, BDC를 사용하기 위해서는 해당 record가 있어야 한다. BDC를 수행하기 위해서는 transaction record가
  있어야 하며, 이는 마우스 클릭으로 생성 or 코드로 프로그램 생성 두 방법이 있다.
---

# BDC

## 1. Transaction record 생성 - Cursor

{% hint style="info" %}
T-Code SHDB : 트랜젝션 레코딩 생성 및 조회 
{% endhint %}

![SHDB](../../.gitbook/assets/image%20%28364%29.png)

New recording을 눌러 새로운 record를 만들어본다. 이 때, 입력한 transaction code로 화면이 이동하며 transaction 녹화를 시작한다. 

![Create Recording](../../.gitbook/assets/image%20%28389%29.png)

자재 생성 T-Code를 입력했기 때문에 자재 생성 화면으로 이동했다. 다음과 같이 값을 입력해주고 다음 화면에서 description 등 필수 값을 입력해주고 저장하면 record는 끝난다. 

![MM01 &#xC790;&#xC7AC; &#xC0DD;&#xC131;](../../.gitbook/assets/image%20%28374%29.png)

저장과 동시에 Record가 끝나고, 다음과 같은 기록을 보여준다. 혹 SHDB로 들어가서 확인할 수도 있다.

![MM01\_24\_001 Record](../../.gitbook/assets/image%20%28384%29.png)

SUB라고 적힌 Subscreen은 불필요한 recording이기 때문에 지워주고, 이 때 모든 SUB를 지울 것이냐는 창이 뜬다. 확인을 눌러준다. 

![SUB &#xC804;&#xCCB4; &#xC0AD;&#xC81C; &#xD655;&#xC778;](../../.gitbook/assets/image%20%28380%29.png)

SUB를 지운 record는 다음과 같다. 이대로 활용해도 되지만, 변수명 혹 코드명의 경우 겹쳐 사용이 안되기 때문에 \(ex. clsap24\_f\_0001\) 이 값만 바꿔서 record 실행이 가능하다. 

![MM01\_24\_001](../../.gitbook/assets/image%20%28362%29.png)



## 2. Transaction record 생성 - ABAP

> 위에서는 직접 커서를 클릭하는 과정을 녹화하여 사용했다면 직접 코드를 짜서 실행해본다.



### 1\) TOP

{% hint style="info" %}
BDCDATA : BDC 사용시 필요한 데이터가 저장되는 DB Table
{% endhint %}

![TOP](../../.gitbook/assets/image%20%28385%29.png)



### 2\) Selection Screen

BDC를 사용하여 transaction을 흘릴 때, 설정할 변수 중 입력받을 값을 parameter로 설정한다. 그리고 보기 편하게 입력 수 text를 설정해준다. 

![Selection screen](../../.gitbook/assets/image%20%28370%29.png)

![Text element &amp;gt; Selection texts](../../.gitbook/assets/image%20%28392%29.png)



### 3\) BDC

#### 기본 틀 생성 및 WA 생성 

값을 입력받고 실행할 BDC에 대해 form으로 만들어준다. 

![Main program](../../.gitbook/assets/image%20%28354%29.png)

어떤 T-code를 사용하여 record를 실행할 것인지에 대한 설정이 필요하기 때문에 사용할 T-code를 불러온다.

{% hint style="info" %}
CALL TRANSACTION : 다른 T-Code 호출 
{% endhint %}

기본적인 틀은 다음과 같으며, 필요한 WA, 데이터를 선언해준다. 

![CREATE\_MATERIAL](../../.gitbook/assets/image%20%28388%29.png)

![TOP &#xB370;&#xC774;&#xD130; &#xCD94;&#xAC00; &#xC120;&#xC5B8;](../../.gitbook/assets/image%20%28347%29.png)



#### 옵션 및 설정 추가 \(1\) 

이제 필요한 옵션을 추가해주고, 원하는 설정을 넣어준다. 설정을 넣어준다는 것은 이전에 Cursor를 사용해 Transaction record를 생성했을때 보았던 다음과 같은 기록은 직접 코드로 넣어준다는 의미이다. 이 때, 첫 줄은 무시하고 다음 줄 부터 입력해주면 되고, 커서에 대한 값 또한 생략해도 된다.   

![MM01\_24\_001](../../.gitbook/assets/image%20%28362%29.png)

![CREATE\_MATERIAL \(1\)](../../.gitbook/assets/image%20%28379%29.png)

![CREATE\_MATERIAL \(2\)](../../.gitbook/assets/image%20%28378%29.png)

![CREATE\_MATERIAL \(3\)](../../.gitbook/assets/image%20%28351%29.png)



#### 옵션 및 설정 추가 \(2\)

이렇게 설정한 부분에 대해서, parameter로 값을 입력받아 설정할 부분들에 대해서 값을 parameter로 받은 변수명으로 변경해준다.  Description과 자재 이름이 이에 해당된다. 

![&#xC790;&#xC7AC; &#xC774;&#xB984; parameter &#xAC12;&#xC73C;&#xB85C; &#xBCC0;&#xACBD;](../../.gitbook/assets/image%20%28393%29.png)

![description&#xC744; parameter &#xAC12;&#xC73C;&#xB85C; &#xBCC0;&#xACBD;](../../.gitbook/assets/image%20%28350%29.png)



#### 옵션 및 설정 추가 \(3\) 

BDC 실행 시 다음과 같은 화면 설정을 할 수 있다. 

| 설정  | 내 |
| :--- | :--- |
| A | BDC 모든 화면을 띄 |
| N | BDC 화면을 하나도 안띄움 + 에러나도 안띄움  |
| E | BDC 화면을 하나도 안띄움 + 에러나면 띄움 |

![BDC &#xD654;&#xBA74; &#xC124;&#xC815;](../../.gitbook/assets/image%20%28358%29.png)



#### Message 추가 

![Message &#xCD94;&#xAC00;](../../.gitbook/assets/image%20%28391%29.png)

## 3. 결과 화면 

### Selection screen

만들고자 하는 자재의 이름과 description을 입력한다. 

![Selection screen](../../.gitbook/assets/image%20%28355%29.png)

### BDC 실행 

화면 옵션 설정을 A로 두어 모든 과정의 화면이 뜨게 했기 때문에 실행 창을 보면서 확인할 수 있다. 

![BDC &#xC2E4;&#xD589; \(1\)](../../.gitbook/assets/image%20%28368%29.png)

![BDC &#xC2E4;&#xD589; \(2\)](../../.gitbook/assets/image%20%28363%29.png)



### 생성 확인

T-Code SE11에서 MARA 테이블을 조회함으로써 위에서 프로그램 실행을 통해 만든 자재를 확인할 수 있다. 

![](../../.gitbook/assets/image%20%28367%29.png)



## 4. 코드

### Main Program

```sql
*&---------------------------------------------------------------------*
*& Report ZR00_0060
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT ZSL_24_013 MESSAGE-ID ZM00.

INCLUDE ZSL_24_013TOP.
INCLUDE ZSL_24_013SEL.
INCLUDE ZSL_24_013F01.

START-OF-SELECTION.
  PERFORM CREATE_MATERIAL.
```

### TOP

```sql
*&---------------------------------------------------------------------*
*& Include          ZR00_0060TOP
*&---------------------------------------------------------------------*

DATA: GT_BDC TYPE TABLE OF BDCDATA,
      GS_BDC TYPE          BDCDATA,
      GS_OPT TYPE          CTU_PARAMS,
      GT_MSG TYPE TABLE OF BDCMSGCOLL,
      GS_MSG TYPE          BDCMSGCOLL.
```

### Selection-Screen

```sql
*&---------------------------------------------------------------------*
*& Include          ZR00_0060SEL
*&---------------------------------------------------------------------*

PARAMETERS: P_MATNR TYPE MARA-MATNR,
            P_MAKTX TYPE MAKT-MAKTX.
```

### Perform - Form 방법 1

```sql
*&---------------------------------------------------------------------*
*& Include          ZR00_0060F01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Form CREATE_MATERIAL
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM CREATE_MATERIAL .
  CLEAR : GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-PROGRAM  = 'SAPLMGMM'.
  GS_BDC-DYNPRO   = '0060'.
  GS_BDC-DYNBEGIN = 'X'.
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-FNAM = 'BDC_OKCODE'.
  GS_BDC-FVAL = '=ENTR'.
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-FNAM = 'RMMG1-MATNR'.
  GS_BDC-FVAL = P_MATNR.        "자재 이름 입력 받음"
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-FNAM = 'RMMG1-MBRSH'.
  GS_BDC-FVAL = 'M'.
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-FNAM = 'RMMG1-MTART'.
  GS_BDC-FVAL = 'FERT'.
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-PROGRAM  = 'SAPLMGMM'.
  GS_BDC-DYNPRO   = '0070'.
  GS_BDC-DYNBEGIN = 'X'.
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-FNAM = 'BDC_OKCODE'.
  GS_BDC-FVAL = '=ENTR'.
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-FNAM = 'MSICHTAUSW-KZSEL(01)'.
  GS_BDC-FVAL = 'X'.
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-PROGRAM  = 'SAPLMGMM'.
  GS_BDC-DYNPRO   = '4004'.
  GS_BDC-DYNBEGIN = 'X'.
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-FNAM = 'BDC_OKCODE'.
  GS_BDC-FVAL = '=BU'.
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-FNAM = 'MAKT-MAKTX'.
  GS_BDC-FVAL = P_MAKTX.        "DESCRIPTION 부분 입력받음"
  APPEND GS_BDC TO GT_BDC.

  CLEAR GS_BDC.
  GS_BDC-FNAM = 'MARA-MEINS'.
  GS_BDC-FVAL = 'EA'.
  APPEND GS_BDC TO GT_BDC.


  CLEAR GS_OPT.
  GS_OPT-DISMODE = 'A'.    "A: BDC 모든 화면을 띄워줌"
                           "N: BDC 화면 하나도 안띄워줌 + 에라나도 안띄움"
                           "E: BDC 화면 하나도 안띄워줌 + 에러나면 띄움"
  GS_OPT-UPDMODE = 'S'.

  CALL TRANSACTION 'MM01' USING GT_BDC
                          OPTIONS FROM GS_OPT
                          MESSAGES INTO GT_MSG.
                          
  READ TABLE GT_MSG INTO GS_MSG WITH KEY MSGID = 'M3'
                                         MSGNR = '800'.
  IF SY-SUBRC = 0.
    "성공처리"
    MESSAGE S008 WITH P_MATNR.
  ELSE.
    "실패처리"
  ENDIF.
ENDFORM.
```

### Perform - Form 방법 2

혹은 CREATE\_BDC 부분에 대한 코드를 다음과 같이 정리할 수 있다. 

```sql
*&---------------------------------------------------------------------*
*& Include          ZR00_0060F01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Form CREATE_MATERIAL
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM CREATE_MATERIAL .

  CLEAR : GT_BDC.

  PERFORM SET_BDC_TAB USING : 'SAPLMGMM' '0060' 'X' '' '',
                              '' '' '' 'BDC_OKCODE' '=ENTR',
                              '' '' '' 'RMMG1-MATNR' P_MATNR,
                              '' '' '' 'RMMG1-MBRSH' 'M',
                              '' '' '' 'RMMG1-MTART' 'FERT'.

  PERFORM SET_BDC_TAB USING : 'SAPLMGMM' '0070' 'X' '' '',
                              '' '' '' 'BDC_OKCODE' '=ENTR',
                              '' '' '' 'MSICHTAUSW-KZSEL(01)' 'X'.

  PERFORM SET_BDC_TAB USING : 'SAPLMGMM' '4004' 'X' '' '',
                              '' '' '' 'BDC_OKCODE' '=BU',
                              '' '' '' 'MAKT-MAKTX' P_MAKTX,
                              '' '' '' 'MARA-MEINS' 'EA'.

  CLEAR GS_OPT.
  GS_OPT-DISMODE = 'N'.   
  GS_OPT-UPDMODE = 'S'.

  CALL TRANSACTION 'MM01' USING GT_BDC
                          OPTIONS FROM GS_OPT
                          MESSAGES INTO GT_MSG.
                          
  READ TABLE GT_MSG INTO GS_MSG WITH KEY MSGID = 'M3'
                                         MSGNR = '800'.
  IF SY-SUBRC = 0.
    "성공처리"
    MESSAGE S008 WITH P_MATNR.
  ELSE.
    "실패처리"
  ENDIF.
ENDFORM.

*&---------------------------------------------------------------------*
*& Form SET_BDC_TAB
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*      -->P_       text
*      -->P_       text
*      -->P_       text
*      -->P_       text
*      -->P_       text
*&---------------------------------------------------------------------*
FORM SET_BDC_TAB  USING    P_PROGRAM
                           P_DYNPRO
                           P_DYNBEGIN
                           P_FNAM
                           P_FVAL.
  CLEAR GS_BDC.
  GS_BDC-PROGRAM  = P_PROGRAM.
  GS_BDC-DYNPRO   = P_DYNPRO.
  GS_BDC-DYNBEGIN = P_DYNBEGIN.
  GS_BDC-FNAM     = P_FNAM.
  GS_BDC-FVAL     = P_FVAL.
  APPEND GS_BDC TO GT_BDC.

ENDFORM.
```

