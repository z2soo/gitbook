---
description: BAPI Funtion을 어떻게 적용하여 활용하는지 기초적인 부분을 익혀본다.
---

# BAPI\_PO\_CHANGE

## 1. BAPI\_PO\_CHANGE 활용

> 프로그램을 실행하여 구매문서 번호와 판매자를 입력받고, 해당 구매문서의 판매자를 입력받은 이름으로 변경하는 프로그램을 짜보도록 한다. 참고로 판매오더에 대한 정보는 EKKO 테이블에 있다.



### 프로그램 생성 

우선적으로 기반이 되는 프로그램을 생성해준다. 이 부분에 대한 코드는 아래를 참조하도록 한다. 

![Main program](../../.gitbook/assets/image%20%28275%29.png)

구매문서 번호 및 바꿔서 넣고자 하는 생성자 이름에 대해 다음과 같이 Parameter로 받아준다. 

![Selection screen](../../.gitbook/assets/image%20%28287%29.png)

Text element 부분에서 다음과 같이 parameter 입력 변수 이름에 문자를 설정해준다. 

![Text element](../../.gitbook/assets/image%20%28294%29.png)



### BAPI\_PO\_CHANGE 입력 

Selection screen에서 입력받은 값을 가지고 특정 PO의 판매자 이름를 변경하고자 한다. 이를 위해 BAPI Function을 추가하고 필요한 값을 입력해준다. 

![](../../.gitbook/assets/image%20%28272%29.png)



## 2. 결과

### 실행 화면

프로그램을 실행하면 변경하고자 하는 구매오더 문서 번호와 sales person 이름을 입력하는 창이 나온다. 

![Selection screen](../../.gitbook/assets/image%20%28266%29.png)

변경하고자 하는 문서 번호는 4500003916이며, sales person 이름을 JISOO로 변경하고자 한다.   
기존에 저장되어 있는 정보는 구매오더 조회에서 확인 가능하다. 

{% hint style="info" %}
T-code ME23N : 구매오더 조회
{% endhint %}

![ME23N &amp;gt; PO&#xC870;&#xD68C;](../../.gitbook/assets/image%20%28277%29.png)

기존 정보를 확인한 후 프로그램 실행을 통해 정보를 입력해본다. 

![&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC2E4;&#xD589;](../../.gitbook/assets/image%20%28295%29.png)

실행 후, 다시 구매 오더 문서를 조회하니 Sales person의 정보가 바뀌었음을 확인할 수 있다.  

![](../../.gitbook/assets/image%20%28303%29.png)



## 3. 코드

### Main Program 

```sql
*&---------------------------------------------------------------------*
*& Report ZSL_24_010
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT ZSL_24_010 MESSAGE-ID ZM00.

INCLUDE ZSL_24_010TOP.
INCLUDE ZSL_24_010SEL.
INCLUDE ZSL_24_010F01.

START-OF-SELECTION.
  PERFORM CHANGE_SALES_PERSON.
END-OF-SELECTION.
```

### Selection-screen 

```sql
*&---------------------------------------------------------------------*
*& Include          ZSL_24_010SEL
*&---------------------------------------------------------------------*

PARAMETERS: P_EBELN TYPE EKKO-EBELN,
            P_VERKF TYPE EKKO-VERKF.
```

### Perform - Form

```sql
*&---------------------------------------------------------------------*
*& Include          ZSL_24_010F01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Form CHANGE_SALES_PERSON
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM CHANGE_SALES_PERSON .
  DATA: LT_RETURN  TYPE TABLE OF BAPIRET2,
        LS_HEADER  TYPE BAPIMEPOHEADER,
        LS_HEADERX TYPE BAPIMEPOHEADERX,
        LS_RETURN  TYPE          BAPIRET2.   "work area 생성

  LS_HEADER-SALES_PERS = P_VERKF.    "바꾸고자 하는 구매문서 번호 넣어줌
  LS_HEADERX-SALES_PERS = 'X'.       "x 값을 줘야지 바뀜, 바꾸고자 하는 필드에 x 표시

  CALL FUNCTION 'BAPI_PO_CHANGE'
    EXPORTING
      PURCHASEORDER = P_EBELN
      POHEADER      = LS_HEADER
      POHEADERX     = LS_HEADERX
    TABLES
      RETURN        = LT_RETURN.

  READ TABLE LT_RETURN INTO LS_RETURN WITH KEY TYPE = 'E'.
  IF SY-SUBRC NE 0.
    CALL FUNCTION 'BAPI_TRANSACTION_COMMIT'   "BAPI 실행 후 수행 필수!
      EXPORTING
        WAIT = 'X'.     "연계가 필요한 경우 WAIT 옵션 줘야 함
    .
  ENDIF.
ENDFORM.
```





