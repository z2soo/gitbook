---
description: 추가 기능 없이 조건으로 조회하여 ALV에 결과를 뿌려주는 것까지 수행해본다.
---

# 조회 화면 생성

## 1. Data, structure, table 선언

이전에 생성해둔 ALV sample template을 복사하여 프로그램을 생성했기 때문에 ALV 생성 부분에 대한 설명은 생략한다. 

DB에서 구매 정보를 가지고 있는 EKKO 테이블을 참조하여 필요한 변수 및 테이블을 선언한다. 데이터 변경에 대한 오류 및 상태를 나타낼 필드를 추가하여 선언해준다.  

![TOP &amp;gt; ITAB &#xC120;&#xC5B8;](../../.gitbook/assets/image%20%28312%29.png)



## 2. Selection screen

특정 값을 기준 혹 조건으로 EKKO를 조회하기 위해 값을 입력받도록 작성해준다. 구매 문서 번호, 구매 문서 타입, 회사 코드 세 가지 값을 입력받도록 설정했으며, Multi 값을 입력받을 수 있도록 했다. 

![Selection screen](../../.gitbook/assets/image%20%28289%29.png)

PA\_1, PA\_2, PA\_3 대신에 보여지게 할 텍스트 또한 설정해준다. 

![Text element &amp;gt; Selection texts](../../.gitbook/assets/image%20%28286%29.png)



## 3. DB에서 데이터 받아오기

EKKO 테이블에서 데이터를 받아서 internal table에 넣어준다. 

![Form &amp;gt; GET\_DATA](../../.gitbook/assets/image%20%28274%29.png)

이 때, LOOP 이하 SQL에 작성에 대해서는 다음과 같은 3가지 방법이 존재한다.   
편한 방식으로 사용하되, 모두 이해하고 있어야 한다. 

```sql
* 방법 1
  LOOP AT GT_DISP INTO GS_DISP.
    GS_DISP-STATUS = ICON_LED_GREEN.
    MODIFY GT_DISP FROM GS_DISP.
  ENDLOOP.
  
* 방법 2
  GS_DISP-STATUS = ICON_LED_GREEN.
  MODIFY GT_DISP FROM GS_DISP TRANSPORTING STATUS
                              WHERE STATUS <> ICON_LED_GREEN.

* 방법 3: New SQL
  SELECT '@5B@' AS STATUS,
         EBELN, BUKRS, BSART, ERNAM, LIFNR,
         ZTERM, VERKF, TELF1
    INTO CORRESPONDING FIELDS OF TABLE @GT_DISP
    FROM EKKO
   WHERE EBELN IN @S_EBELN
     AND BUKRS IN @S_BUKRS
     AND BSART IN @S_BSART
     AND BSTYP EQ 'F'
     AND LOEKZ EQ ''.
```



## 4. Field catalog 생성

위에서 받아온 데이터를 ALV 화면에 뿌려주기 위한 Field catalog를 생성해준다. 이 때, 생성자와 전화번호는 수정이 가능하게 설정해준다. 

![](../../.gitbook/assets/image%20%28278%29.png)

![Screen 0100 &amp;gt; PBO &amp;gt; SET\_ALV &amp;gt; SET\_FIELDCAT ](../../.gitbook/assets/image%20%28302%29.png)



## 5. 결과

### Selection screen

![Selection screen](../../.gitbook/assets/image%20%28270%29.png)

### Screen 0100

![Screen 0100](../../.gitbook/assets/image%20%28290%29.png)



## 6. 코드

### Main Program 

```sql
*&---------------------------------------------------------------------*
*& Report ZS_0001
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT ZSL_24_012 MESSAGE-ID ZM00.

INCLUDE ZSL_24_012TOP.
INCLUDE ZSL_24_012SEL.
INCLUDE ZSL_24_012F01.
INCLUDE ZSL_24_012I01.
INCLUDE ZSL_24_012O01.

START-OF-SELECTION.

PERFORM GET_DATA.

CALL SCREEN '0100'.
```

### Selection-screen 

```sql
*&---------------------------------------------------------------------*
*& Include          ZS_0001SEL
*&---------------------------------------------------------------------*

SELECT-OPTIONS: PA_1 FOR EKKO-EBELN,
                PA_2 FOR EKKO-BUKRS,
                PA_3 FOR EKKO-BSART.
```

### Screen 0100

```sql
*&---------------------------------------------------------------------*
*& Screen 0100
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*

PROCESS BEFORE OUTPUT.
  MODULE STATUS_0100.
  MODULE SET_ALV_0100.

PROCESS AFTER INPUT.
  MODULE EXIT AT EXIT-COMMAND.
*  MODULE USER_COMMAND_0100.
```

### Top 

```sql
*&---------------------------------------------------------------------*
*& Include          ZS_0001TOP
*&---------------------------------------------------------------------*

* 화면 출력 및 데이터 처리를 위한 선언
TABLES: EKKO.
DATA: GV_OKCODE TYPE SY-UCOMM.
DATA : BEGIN OF GS_DISP,
         EBELN TYPE EKKO-EBELN,
         BUKRS TYPE EKKO-BUKRS,
         BSART TYPE EKKO-BSART,
         ERNAM TYPE EKKO-ERNAM,
         LIFNR TYPE EKKO-LIFNR,
         ZTERM TYPE EKKO-ZTERM,
         VERKF TYPE EKKO-VERKF,
         TELF1 TYPE EKKO-TELF1,
         RESULT TYPE CHAR20,
         STATUS TYPE ICON-ID,
       END OF GS_DISP.
DATA : GT_DISP LIKE TABLE OF GS_DISP.

************************************************************************
*---- ALV 관련 선언 ----
************************************************************************
DATA : GO_CONTAINER TYPE REF TO CL_GUI_CUSTOM_CONTAINER,
       GO_GRID      TYPE REF TO CL_GUI_ALV_GRID.

DATA : GT_FCAT  TYPE LVC_T_FCAT,
       GS_FCAT   TYPE LVC_S_FCAT,
       GS_LAYOUT TYPE LVC_S_LAYO.
```

### Process Before Output 

```sql
*&---------------------------------------------------------------------*
*& Include          ZS_0001O01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Module STATUS_0100 OUTPUT
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
MODULE STATUS_0100 OUTPUT.
  SET PF-STATUS '0100'.
  SET TITLEBAR '0100'.
ENDMODULE.

*&---------------------------------------------------------------------*
*& Module SET_ALV_0100 OUTPUT
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
MODULE SET_ALV_0100 OUTPUT.
  PERFORM SET_ALV_0100.
ENDMODULE.
```

### Process After Input 

```sql
*&---------------------------------------------------------------------*
*& Include          ZS_0001I01
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
*& Include          ZS_0001F01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Form SET_ALV_0100
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM SET_ALV_0100 .

  IF GO_CONTAINER IS INITIAL.
* OBJECT&INSTANCE 생성
    PERFORM CREATE_OBJECT_INSTANCE.

* FIELD CATALOG 셋팅
    PERFORM SET_FILDCAT.

* LAYOUT 셋팅
    PERFORM SET_LAYOUT.

* ALV 호출
    PERFORM DISPALY_ALV.

  ELSE.
    PERFORM REFRESH_DATA.
  ENDIF.

ENDFORM.

*&---------------------------------------------------------------------*
*& Form CREATE_OBJECT_INSTANCE
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM CREATE_OBJECT_INSTANCE .
  CREATE OBJECT GO_CONTAINER
    EXPORTING
      CONTAINER_NAME              = 'AREA_0100'.

CREATE OBJECT GO_GRID
  EXPORTING
    I_PARENT          = GO_CONTAINER.
ENDFORM.

*&---------------------------------------------------------------------*
*& Form SET_FILDCAT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM SET_FILDCAT .

  CLEAR GT_FCAT.
  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'STATUS'.
  GS_FCAT-COLTEXT   = '상태'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'EBELN'.
  GS_FCAT-COLTEXT   = '구매오더'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'BUKRS'.
  GS_FCAT-COLTEXT   = '회사코드'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'BSART'.
  GS_FCAT-COLTEXT   = '문서유형'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'ERNAM'.
  GS_FCAT-COLTEXT   = '생성자'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'LIFNR'.
  GS_FCAT-COLTEXT   = '공급업체'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'ZTERM'.
  GS_FCAT-COLTEXT   = '지급조건'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'VERKF'.
  GS_FCAT-COLTEXT   = '담당자'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'TELF1'.
  GS_FCAT-COLTEXT   = '연락처'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'RESULT'.
  GS_FCAT-COLTEXT   = '처리결과'.
  APPEND GS_FCAT TO GT_FCAT.
ENDFORM.

*&---------------------------------------------------------------------*
*& Form SET_LAYOUT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM SET_LAYOUT .

  CLEAR GS_LAYOUT.

  GS_LAYOUT-ZEBRA = 'X'.
  GS_LAYOUT-CWIDTH_OPT = 'A'.
  GS_LAYOUT-SEL_MODE   = 'D'.   "드래그 가능

ENDFORM.

*&---------------------------------------------------------------------*
*& Form DISPALY_ALV
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM DISPALY_ALV .

  CALL METHOD GO_GRID->SET_TABLE_FOR_FIRST_DISPLAY
    EXPORTING
*      I_BUFFER_ACTIVE               =
*      I_BYPASSING_BUFFER            =
*      I_CONSISTENCY_CHECK           =
*      I_STRUCTURE_NAME              =
*      IS_VARIANT                    =
*      I_SAVE                        =
*      I_DEFAULT                     = 'X'
      IS_LAYOUT                     = GS_LAYOUT
*      IS_PRINT                      =
*      IT_SPECIAL_GROUPS             =
*      IT_TOOLBAR_EXCLUDING          =
*      IT_HYPERLINK                  =
*      IT_ALV_GRAPHICS               =
*      IT_EXCEPT_QINFO               =
*      IR_SALV_ADAPTER               =
    CHANGING
      IT_OUTTAB                     = GT_DISP
      IT_FIELDCATALOG               = GT_FCAT
*      IT_SORT                       =
*      IT_FILTER                     =
*    EXCEPTIONS
*      INVALID_PARAMETER_COMBINATION = 1
*      PROGRAM_ERROR                 = 2
*      TOO_MANY_LINES                = 3
*      OTHERS                        = 4
          .
ENDFORM.

*&---------------------------------------------------------------------*
*& Form GET_DATA
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM GET_DATA .

  CLEAR GT_DISP.

  SELECT EBELN BUKRS BSART ERNAM LIFNR
         ZTERM VERKF TELF1
    INTO CORRESPONDING FIELDS OF TABLE GT_DISP
    FROM EKKO
   WHERE EBELN IN PA_1
     AND BUKRS IN PA_2
     AND BSART IN PA_3
     AND BSTYP EQ 'F'
     AND LOEKZ EQ ''.

  SORT GT_DISP BY EBELN.

* 방법 1
  LOOP AT GT_DISP INTO GS_DISP.
    GS_DISP-STATUS = ICON_LED_GREEN.
    MODIFY GT_DISP FROM GS_DISP.
  ENDLOOP.

* 방법 2
*  GS_DISP-STATUS = ICON_LED_GREEN.
*  MODIFY GT_DISP FROM GS_DISP TRANSPORTING STATUS
*                              WHERE STATUS <> ICON_LED_GREEN.

** 방법 3: New SQL
*  SELECT '@5B@' AS STATUS,
*         EBELN, BUKRS, BSART, ERNAM, LIFNR,
*         ZTERM, VERKF, TELF1
*    INTO CORRESPONDING FIELDS OF TABLE @GT_DISP
*    FROM EKKO
*   WHERE EBELN IN @S_EBELN
*     AND BUKRS IN @S_BUKRS
*     AND BSART IN @S_BSART
*     AND BSTYP EQ 'F'
*     AND LOEKZ EQ ''.

ENDFORM.

*&---------------------------------------------------------------------*
*& Form REFRESH_DATA
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM REFRESH_DATA .
  CALL METHOD GO_GRID->REFRESH_TABLE_DISPLAY.
ENDFORM.
```





