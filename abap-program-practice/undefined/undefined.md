---
description: >-
  조회 스크린에서 조회되는 값 중 부서, 직급, 재직구분의 도메인 값에 따른 range value 즉, 실제 의미하는 도메인 텍스트 데이터를
  가져와 추가해준다.
---

# 도메인 텍스트 추가

## 1. Domain range value 가져오기 

### 1\) Structure 및 Table 선언

{% hint style="info" %}
Domain value, text 값은 DD07T 테이블에서 가져온다.
{% endhint %}

도메인 value에 따른 text 값을 담기 위한 structure와 table이 필요하다. Domain value와 domain text의 값을 가지는 table을 부서, 직급, 재직 구분 각각 만들어주도록 한다. 

![](../../.gitbook/assets/image%20%28225%29.png)



### 2\) Domain text 가져오기 

Main program의 기존 GET\_DATA 부분을 도메인 데이터와 인사 데이터를 각각 가져오고 이를 합쳐주는 세 개의 단계로 나누어 실행한다. 

![](../../.gitbook/assets/image%20%28234%29.png)

#### 

#### GET\_DOMAIN\_TEXT

DD07T 테이블에서 값을 읽어들이고, 위에서 선언한 부서, 직급, 재직구분 별 Domain table에 넣어주도록 한다. 

![GET\_DATA &amp;gt; GET\_DOMAIN\_TEXT](../../.gitbook/assets/image%20%28231%29.png)

Domain name에 하드 코딩을 해도 되지만, TOP에 Constants 값으로 선언해주었다. 

![TOP &amp;gt; Constants &#xC120;&#xC5B8;](../../.gitbook/assets/image%20%28239%29.png)

#### 

#### GET\_EMPLOYEE\_MASTER

이전까지 GT\_ITAB으로 사용하던 변수명을 GT\_DISP로, P\_1~5는 S\_EMPNO, S\_DEPT, S\_ENTDT, S\_GRADE, S\_STATUS로 변경하였으나 기본 코드는 동일하다. 

![GET\_DATA &amp;gt; GET\_EMPLOYEE\_MASTER](../../.gitbook/assets/image%20%28232%29.png)



#### MERGE\_DATA

![GET\_DATA &amp;gt; MERGE\_DATA-1](../../.gitbook/assets/image%20%28249%29.png)

![GET\_DATA &amp;gt; MERGE\_DATA-2](../../.gitbook/assets/image%20%28242%29.png)

#### 

## 2. Field catalog 설정 

### 1\) Field catalog 선언

{% hint style="info" %}
Field catalog는 LVC\_T\_FCAT, LVC\_S\_FCAT을 참조하여 선언한다. 
{% endhint %}

Domain text 값을 추가적으로 보여줄 것이기 때문에 ALV 출력 틀 또한 변경해줘야 한다. 즉, Domain text 값을 가지고 있는 형태의 Field catalog를 선언해준다.

![Field catalog &#xAD6C;&#xC870;&#xCCB4; &#xC120;&#xC5B8; &amp;gt; GT\_FCAT, GS\_FCAT](../../.gitbook/assets/image%20%28261%29.png)



### 2\) Field catalog 구조 설정

{% hint style="info" %}
Field catalog structure에 값을 넣고 table에 append하는 방식 활용
{% endhint %}

선언한 Field catalog 구조에 어떤 열을 어떤 이름으로 표현할 것인지 설정해준다. 그 외에 참조, KEY 설정, 숨김 등에 대한 설정도 가능하다. 해당 과정은 ALV 생성 중 ALV Display 이전에 진행한다. 

![Screen 0100 &amp;gt; SET\_ALV](../../.gitbook/assets/image%20%28255%29.png)

![Field catalog &#xC124;&#xC815; - 1](../../.gitbook/assets/image%20%28238%29.png)

![Field catalog &#xC124;&#xC815; - 2](../../.gitbook/assets/image%20%28230%29.png)

![Field catalog &#xC124;&#xC815; - 3](../../.gitbook/assets/image%20%28252%29.png)



### 3\) Field catalog 적용

생성한 Field catalog를 ALV Display 부분에 적용시켜준다. 이 때, I\_STRUCTURE\_NAME에 설정해 둔 부분은 주석처리함을 잊지 말자.

![Screen 0100 &amp;gt; SET\_ALV &amp;gt; SET\_DISPLAY](../../.gitbook/assets/image%20%28233%29.png)



## 3. 결과 및 코드

### 결과 화면 

![Selection-screen](../../.gitbook/assets/image%20%28251%29.png)

![Screen 0100](../../.gitbook/assets/image%20%28247%29.png)

### Main Program

```sql
*&---------------------------------------------------------------------*
*& Report ZSL_24_005
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT ZSL_24_005.

INCLUDE ZSL005_TOP.
INCLUDE ZSL005_SEL.
INCLUDE ZSL005_F01.
INCLUDE ZSL005_O01.
INCLUDE ZSL005_I01.

INITIALIZATION.
AT SELECTION-SCREEN.
START-OF-SELECTION.
  PERFORM GET_DATA.
END-OF-SELECTION.
CALL SCREEN 100.
```

### Selection-screen

```sql
*&---------------------------------------------------------------------*
*& Include          ZSL005_SEL
*&---------------------------------------------------------------------*
SELECTION-SCREEN BEGIN OF BLOCK BL1 WITH FRAME TITLE TEXT-100.
  SELECT-OPTIONS: S_EMPNO FOR ZT24_0010-EMPNO,
                  S_DEPT FOR ZT24_0010-DEPT,
                  S_ENTDT FOR ZT24_0010-ENTDT,
                  S_GRADE FOR ZT24_0010-GRADE,
                  S_STATUS FOR ZT24_0010-STATUS.
SELECTION-SCREEN END OF BLOCK BL1.
```

### Screen 0100

```sql
*&---------------------------------------------------------------------*
*& Screen 0100
*&---------------------------------------------------------------------*

PROCESS BEFORE OUTPUT.
  MODULE STATUS_0100.
  MODULE SET_ALV.

PROCESS AFTER INPUT.
  MODULE EXIT AT EXIT-COMMAND.
*  MODULE USER_COMMAND_0100.
```

### Top

```sql
*&---------------------------------------------------------------------*
*& Include          ZSL005_TOP
*&---------------------------------------------------------------------*
TABLES: ZT24_0010.
DATA: GT_ITAB TYPE TABLE OF ZT24_0010,
      GS_ITAB TYPE ZT24_0010.

* 도메인 이름에 대한 constants 설정
CONSTANTS: GC_DOM_DEPT TYPE DOMNAME VALUE 'ZD00_DEPT',
           GC_DOM_GRADE TYPE DOMNAME VALUE 'ZD00_GRADE',
           GC_DOM_STATUS TYPE DOMNAME VALUE 'ZD00_STATUS'.

* 화면 출력용
DATA : BEGIN OF GS_DISP.
         INCLUDE STRUCTURE ZT24_0010.
DATA :   DEPT_T   TYPE DD07T-DDTEXT,
         GRADE_T  TYPE DD07T-DDTEXT,
         STATUS_T TYPE DD07T-DDTEXT,
       END OF GS_DISP.
DATA : GT_DISP LIKE TABLE OF GS_DISP.

* 도메인 텍스트 처리용
DATA: BEGIN OF GS_TEXT,
        CODE TYPE DD07T-DOMVALUE_L,
        TEXT TYPE DD07T-DDTEXT,
      END OF GS_TEXT.
DATA: GT_DEPT   LIKE TABLE OF GS_TEXT,
      GT_GRADE  LIKE TABLE OF GS_TEXT,
      GT_STATUS LIKE TABLE OF GS_TEXT.



************************************************************************
*---- ALV 관련 선언 ----
************************************************************************
DATA: GO_CON type REF TO CL_GUI_CUSTOM_CONTAINER,
      GO_ALV TYPE REF TO CL_GUI_CUSTOM_ALV_GRID.

DATA : GT_FCAT  TYPE LVC_T_FCAT,
       GS_FCAT   TYPE LVC_S_FCAT,
       GS_LAYOUT TYPE LVC_S_LAYO.
```

### Process Before Output

```sql
*&---------------------------------------------------------------------*
*& Include          ZSL005_O01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Module STATUS_0100 OUTPUT
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
MODULE STATUS_0100 OUTPUT.
  SET PF-STATUS '100'.
  SET TITLEBAR '100'.
ENDMODULE.

*&---------------------------------------------------------------------*
*& Module SET_ALV OUTPUT
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
MODULE SET_ALV OUTPUT.
* ALV Object 생성
  PERFORM CREATE_ALV_OBJECT.

* FIELD CATALOG 세팅
  PERFORM SET_FIELDCAT.

* LAYOUT 세팅

* ALV 출력
  PERFORM SET_DISPLAY.
ENDMODULE.
```

### Process After Input

```sql
*&---------------------------------------------------------------------*
*& Include          ZSL005_I01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  EXIT  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
MODULE EXIT INPUT.
  LEAVE TO SCREEN 0.
ENDMODULE.
```

### Perform - Form

```sql
*&---------------------------------------------------------------------*
*& Include          ZSL005_F01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Form GET_DATA
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM GET_DATA .
* 도메인 데이터 가져오기
  PERFORM GET_DOMAIN_TEXT.
* 안사 데이터 가져오기
  PERFORM GET_EMPLOYEE_MASTER.
* 데이터 취합하기
  PERFORM MERGE_DATA.
ENDFORM.

*&---------------------------------------------------------------------*
*& Form CREATE_ALV_OBJECT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM CREATE_ALV_OBJECT .
  CREATE OBJECT GO_CON
    EXPORTING
      CONTAINER_NAME    = 'AREA_100'.

  CREATE OBJECT GO_ALV
    EXPORTING
      I_PARENT          = GO_CON.
ENDFORM.

*&---------------------------------------------------------------------*
*& Form SET_DISPLAY
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM SET_DISPLAY .
  CALL METHOD GO_ALV->SET_TABLE_FOR_FIRST_DISPLAY
*    EXPORTING
*      I_STRUCTURE_NAME              = 'ZT24_0010'
    CHANGING
      IT_OUTTAB                     = GT_DISP
      IT_FIELDCATALOG               = GT_FCAT.
ENDFORM.

*&---------------------------------------------------------------------*
*& Form SET_FIELDCAT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM SET_FIELDCAT .

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'EMPNO'.
  GS_FCAT-COLTEXT   = '사원번호'.
  GS_FCAT-KEY       = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'NAME'.
  GS_FCAT-COLTEXT   = '이름'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'DEPT'.
  GS_FCAT-COLTEXT   = '부서'.
  GS_FCAT-REF_TABLE = 'ZT00_0010'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'DEPT_T'.
  GS_FCAT-COLTEXT   = '부서내역'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'ENTDT'.
  GS_FCAT-COLTEXT   = '입사일'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'GRADE'.
  GS_FCAT-COLTEXT   = '직급'.
  GS_FCAT-REF_TABLE = 'ZT00_0010'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'GRADE_T'.
  GS_FCAT-COLTEXT   = '직급내역'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'RETDT'.
  GS_FCAT-COLTEXT   = '퇴사일'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'STATUS'.
  GS_FCAT-COLTEXT   = '재직구분'.
  GS_FCAT-REF_TABLE = 'ZT00_0010'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'STATUS_T'.
  GS_FCAT-COLTEXT   = '재직구분 내역'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'PHONE'.
  GS_FCAT-COLTEXT   = '전화번호'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'ADDR_H'.
  GS_FCAT-COLTEXT   = '자택주소'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'ADDR_W'.
  GS_FCAT-COLTEXT   = '근무지주소'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'SALARY'.
  GS_FCAT-COLTEXT   = '기본급'.
  GS_FCAT-CFIELDNAME = 'WAERS'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'WAERS'.
  GS_FCAT-NO_OUT    = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

ENDFORM.

*&---------------------------------------------------------------------*
*& Form GET_DOMAIN_TEXT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM GET_DOMAIN_TEXT .

  CLEAR : GT_GRADE, GT_DEPT, GT_STATUS.
  SELECT DOMVALUE_L AS CODE
         DDTEXT     AS TEXT
    INTO CORRESPONDING FIELDS OF TABLE GT_DEPT
    FROM DD07T
   WHERE DOMNAME = GC_DOM_DEPT. "'ZD00_DEPT'.

  SELECT DOMVALUE_L AS CODE
         DDTEXT     AS TEXT
    INTO CORRESPONDING FIELDS OF TABLE GT_GRADE
    FROM DD07T
   WHERE DOMNAME = GC_DOM_GRADE. "'ZD00_GRADE'.

  SELECT DOMVALUE_L AS CODE
         DDTEXT     AS TEXT
    INTO CORRESPONDING FIELDS OF TABLE GT_STATUS
    FROM DD07T
   WHERE DOMNAME = GC_DOM_STATUS. " 'ZD00_STATUS'.

ENDFORM.

*&---------------------------------------------------------------------*
*& Form GET_EMPLOYEE_MASTER
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM GET_EMPLOYEE_MASTER .

  CLEAR GT_DISP.

  SELECT *
    INTO CORRESPONDING FIELDS OF TABLE GT_DISP
    FROM ZT24_0010
   WHERE EMPNO  IN S_EMPNO
     AND DEPT   IN S_DEPT
     AND ENTDT  IN S_ENTDT
     AND GRADE  IN S_GRADE
     AND STATUS IN S_STATUS.

ENDFORM.

*&---------------------------------------------------------------------*
*& Form MERGE_DATA
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM MERGE_DATA .
  FIELD-SYMBOLS : <FS_DISP> LIKE GS_DISP.

  SORT : GT_DEPT   BY CODE,
         GT_GRADE  BY CODE,
         GT_STATUS BY CODE.

  LOOP AT GT_DISP ASSIGNING <FS_DISP>. "INTO GS_DISP.

* 부서내역
    READ TABLE GT_DEPT INTO GS_TEXT
                       WITH KEY CODE = <FS_DISP>-DEPT
                       BINARY SEARCH.
    IF SY-SUBRC = 0.
      <FS_DISP>-DEPT_T = GS_TEXT-TEXT.
    ENDIF.

* 직급 내역
    READ TABLE GT_GRADE INTO GS_TEXT
                        WITH KEY CODE = <FS_DISP>-GRADE
                        BINARY SEARCH.
    IF SY-SUBRC = 0.
      <FS_DISP>-GRADE_T = GS_TEXT-TEXT.
    ENDIF.

* 재직구분 내역
    READ TABLE GT_STATUS INTO GS_TEXT
                         WITH KEY CODE = <FS_DISP>-STATUS
                         BINARY SEARCH.
    IF SY-SUBRC = 0.
      <FS_DISP>-STATUS_T = GS_TEXT-TEXT.
    ENDIF.
  ENDLOOP.
ENDFORM.
```

### 

