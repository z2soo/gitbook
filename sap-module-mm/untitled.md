# 실습 - 인사 프로그램 생성

![structure &#xC0DD;&#xC131;](../.gitbook/assets/image%20%28156%29.png)

![](../.gitbook/assets/image%20%28157%29.png)

생성한 structure를 이전에 만든 table에 include로 넣어준다. 

![](../.gitbook/assets/image%20%28155%29.png)

![](../.gitbook/assets/image%20%28162%29.png)

///

![](../.gitbook/assets/image%20%28164%29.png)

상단의 TEXT ELEMENT로 PARAMETER이름 설정 가



![](../.gitbook/assets/image%20%28166%29.png)

///

![](../.gitbook/assets/image%20%28165%29.png)

![](../.gitbook/assets/image%20%28163%29.png)

위와 같은 프로그램 생성을 위한 프로그래밍은 다음과 같다. 

```sql
*&---------------------------------------------------------------------*
*& Report ZR24_0010
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT ZR24_0010.

INCLUDE ZR24_0010TOP.
INCLUDE ZR24_0010F01.
INCLUDE ZR24_0010O01.
INCLUDE ZR24_0010I01.

INITIALIZATION.
AT SELECTION-SCREEN.
START-OF-SELECTION.
  PERFORM GET_DATA.
END-OF-SELECTION.
CALL SCREEN 0100.



*&---------------------------------------------------------------------*
*& Screen 100
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
PROCESS BEFORE OUTPUT.
  MODULE STATUS_0100.
  MODULE SET_ALV.

PROCESS AFTER INPUT.
  MODULE EXIT AT EXIT-COMMAND.
  
  
  
*&---------------------------------------------------------------------*
*& Include          ZR24_0010TOP
*&---------------------------------------------------------------------*
TABLES: ZT24_0010.
DATA: GT_ITAB TYPE TABLE OF ZT24_0010,
      GS_ITAB TYPE ZT24_0010.

DATA: GO_CON TYPE REF TO CL_GUI_CUSTOM_CONTAINER,
      GO_ALV TYPE REF TO CL_GUI_ALV_GRID.
DATA: GT_FCAT TYPE LVC_T_FCAT,
      GS_FCAT TYPE LVC_S_FCAT,
      GS_LAYOUT TYPE LVC_S_LAYO.

SELECTION-SCREEN BEGIN OF BLOCK BL1 WITH FRAME TITLE TEXT-100.
  SELECT-OPTIONS: PA_1 FOR ZT24_0010-EMPNO,
                  PA_2 FOR ZT24_0010-DEPT,
                  PA_3 FOR ZT24_0010-ENTDT,
                  PA_4 FOR ZT24_0010-GRADE,
                  PA_5 FOR ZT24_0010-STATUS.
SELECTION-SCREEN END OF BLOCK BL1.



*&---------------------------------------------------------------------*
*& Include          ZR24_0010F01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*& Form SET_CAT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM SET_CAT .

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'EMPNO'.
    GS_FCAT-COLTEXT = '사원번호'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'NAME'.
    GS_FCAT-COLTEXT = '이름'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'DEPT'.
    GS_FCAT-COLTEXT = '부서'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'ENTDT'.
    GS_FCAT-COLTEXT = '입사일'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'GRADE'.
    GS_FCAT-COLTEXT = '직급'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'RETDT'.
    GS_FCAT-COLTEXT = '퇴사일'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'STATUS'.
    GS_FCAT-COLTEXT = '재직구분'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'PHONE'.
    GS_FCAT-COLTEXT = '전화번호'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'ADDR_H'.
    GS_FCAT-COLTEXT = '자택주소'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'ADDR_W'.
    GS_FCAT-COLTEXT = '근무지주소'.
    APPEND GS_FCAT TO GT_FCAT.

    CLEAR GS_FCAT.
    GS_FCAT-FIELDNAME = 'SALARY'.
    GS_FCAT-COLTEXT = '기본급'.
    APPEND GS_FCAT TO GT_FCAT.

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
  CLEAR GT_ITAB.
  SELECT *
    FROM ZT24_0010
    INTO CORRESPONDING FIELDS OF TABLE GT_ITAB
    WHERE EMPNO IN PA_1
    AND DEPT IN PA_2.

ENDFORM.



*&---------------------------------------------------------------------*
*& Form CREATE_OBJECT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM CREATE_OBJECT .
    CREATE OBJECT GO_CON
      EXPORTING
        CONTAINER_NAME    = 'AREA_0100'.
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
     " EXPORTING
        "I_STRUCTURE_NAME              = 'ZT24_0010'
      CHANGING
        IT_OUTTAB                     = GT_ITAB
        IT_FIELDCATALOG               = GT_FCAT
        .
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
  GS_LAYOUT-CWIDTH_OPT = 'X'.
ENDFORM.



*&---------------------------------------------------------------------*
*& Include          ZR24_0010O01
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
*& Module SET_ALV OUTPUT
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
MODULE SET_ALV OUTPUT.

  PERFORM CREATE_OBJECT.

  PERFORM SET_CAT.

  PERFORM SET_LAYOUT.

  PERFORM SET_DISPLAY.

ENDMODULE.



*&---------------------------------------------------------------------*
*& Include          ZR24_0010I01
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

//

도메인 텍스트 가져오???



