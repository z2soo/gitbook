---
description: '상태 열을 추가하여 신호등을 넣어주고, 데이터 변경에 따라 신호등의 색상이 변경되게끔 설정해준다.'
---

# 신호등 아이콘 추가

TOP 부분에서 선언한 화면 출력용 GS\_DISP 구조에 STAT 이라는 열을 추가해주되, ICON-ID 타입으로 선언해준다. 

![TOP &amp;gt; GS\_DISP &#xC120;&#xC5B8; &amp;gt; STAT &#xCD94;&#xAC00;](../../.gitbook/assets/image%20%28277%29.png)

Field catalog에도 STAT 열에 대한 설정을 추가해준다. 

![Form &amp;gt; Field catalog STAT &#xCD94;&#xAC00;](../../.gitbook/assets/image%20%28269%29.png)

MERGE\_DATA에서 STAT열에 대한 데이터 값을 넣어준다. 데이터 값이 변경되지 않은 기본 값으로 ICON\_GREEN\_LIGHT를 설정한다. 

![GET\_DATA &amp;gt; MERGE\_DATA &amp;gt; Icon &#xC124;&#xC815; &#xCD94;&#xAC00;](../../.gitbook/assets/image%20%28268%29.png)

데이터가 변경될 때, 신호등 색상을 노란색으로 하고 싶다면?

HANDLE\_DATA\_CHANGED에서 PO\_DATA\_CHANGED-&gt;MODIFY\_CELL 사용

다음의 경우, STATUS의 값이 변경되는 경우 신호등 색상이 노란색으로 변경

![HANDLE\_DATA\_CHANGED](../../.gitbook/assets/image%20%28264%29.png)

![&#xBCC0;&#xACBD; &#xC804; &#xCD08;&#xB85D; &#xC2E0;&#xD638;&#xB4F1;](../../.gitbook/assets/image%20%28276%29.png)

![&#xC7AC;&#xC9C1; &#xAD6C;&#xBD84; &#xBCC0;&#xACBD; &#xD6C4; &#xB178;&#xB780; &#xC2E0;&#xD638;&#xB4F1;](../../.gitbook/assets/image%20%28273%29.png)

```text
*&---------------------------------------------------------------------*
*& Include          ZR00_0020CLS
*&---------------------------------------------------------------------*
CLASS LCL_EVENT_RECEIVER DEFINITION.
  PUBLIC SECTION.

    METHODS : HANDLE_DATA_CHANGED
                  FOR EVENT DATA_CHANGED OF CL_GUI_ALV_GRID
      IMPORTING ER_DATA_CHANGED.

    METHODS : HANDLE_DOUBLE_CLICK
                  FOR EVENT DOUBLE_CLICK OF CL_GUI_ALV_GRID
      IMPORTING E_ROW
                E_COLUMN
                ES_ROW_NO.


ENDCLASS.

CLASS LCL_EVENT_RECEIVER IMPLEMENTATION.

  METHOD : HANDLE_DATA_CHANGED.
    PERFORM HANDLE_DATA_CHANGED USING ER_DATA_CHANGED.
  ENDMETHOD.

  METHOD : HANDLE_DOUBLE_CLICK.
BREAK-POINT.
  ENDMETHOD.

ENDCLASS.

DATA : GO_EVENT_RECEIVER TYPE REF TO LCL_EVENT_RECEIVER.
```

```text
*&---------------------------------------------------------------------*
*& Report ZR00_0000
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT ZSL_24_99999 MESSAGE-ID ZM00.

INCLUDE ZL24_9999_TOP.
*INCLUDE ZR00_0020TOP.
INCLUDE ZL24_9999_CLS.
*INCLUDE ZR00_0020CLS.
INCLUDE ZL24_9999_SEL.
*INCLUDE ZR00_0020SEL.
INCLUDE ZL24_9999_F01.
*INCLUDE ZR00_0020F01.
INCLUDE ZL24_9999_I01.
*INCLUDE ZR00_0020I01.
INCLUDE ZL24_9999_O01.
*INCLUDE ZR00_0020O01.

START-OF-SELECTION.

  PERFORM GET_DATA.

  CALL SCREEN '0100'.
```

```text
PROCESS BEFORE OUTPUT.
  MODULE STATUS_0100.
  MODULE SET_ALV_0100.

PROCESS AFTER INPUT.
  MODULE EXIT_0100 AT EXIT-COMMAND.
  MODULE USER_COMMAND_0100.
```

```text
*&---------------------------------------------------------------------*
*& Include          ZR00_0000F01
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
* INSTANCE 생성
    PERFORM CREATE_OBJECT.

* 출력필드 셋팅
    PERFORM SET_FIELDCAT.

* 레이아웃 셋팅
    PERFORM SET_LAYOUT.

* EVENT 등록
    PERFORM SET_EVENT.

* ALV 호출
    PERFORM DISPLAY_ALV.

  ELSE.
    PERFORM REFRESH_DATA.
  ENDIF.

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

* CONTAINER 생성
  CREATE OBJECT GO_CONTAINER
    EXPORTING
      CONTAINER_NAME = 'GO_CONTAINER'.

* GRID 생성
  CREATE OBJECT GO_GRID
    EXPORTING
      I_PARENT = GO_CONTAINER.

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

  CLEAR GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'STAT'.
  GS_FCAT-COLTEXT   = '상태'.
  GS_FCAT-KEY       = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'EMPNO'.
  GS_FCAT-COLTEXT   = '사원번호'.
  GS_FCAT-KEY       = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'NAME'.
  GS_FCAT-COLTEXT   = '이름'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'DEPT'.
  GS_FCAT-COLTEXT   = '부서'.
  GS_FCAT-REF_TABLE = 'ZT00_0010'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'DEPT_T'.
  GS_FCAT-COLTEXT   = '부서내역'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'ENTDT'.
  GS_FCAT-COLTEXT   = '입사일'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'GRADE'.
  GS_FCAT-COLTEXT   = '직급'.
  GS_FCAT-REF_TABLE = 'ZT00_0010'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'GRADE_T'.
  GS_FCAT-COLTEXT   = '직급내역'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'RETDT'.
  GS_FCAT-COLTEXT   = '퇴사일'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'STATUS'.
  GS_FCAT-COLTEXT   = '재직구분'.
  GS_FCAT-REF_TABLE = 'ZT00_0010'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'STATUS_T'.
  GS_FCAT-COLTEXT   = '재직구분 내역'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'PHONE'.
  GS_FCAT-COLTEXT   = '전화번호'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'ADDR_H'.
  GS_FCAT-COLTEXT   = '자택주소'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'ADDR_W'.
  GS_FCAT-COLTEXT   = '근무지주소'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'SALARY'.
  GS_FCAT-COLTEXT   = '기본급'.
  GS_FCAT-CFIELDNAME = 'WAERS'.
  GS_FCAT-EDIT      = 'X'.
  APPEND GS_FCAT TO GT_FCAT.

  CLEAR GS_FCAT.
  GS_FCAT-FIELDNAME = 'WAERS'.
  GS_FCAT-COLTEXT   = '통화'.
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
  GS_LAYOUT-SEL_MODE   = 'D'.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form DISPLAY_ALV
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM DISPLAY_ALV .

  CALL METHOD GO_GRID->SET_TABLE_FOR_FIRST_DISPLAY
    EXPORTING
      IS_LAYOUT       = GS_LAYOUT
    CHANGING
      IT_OUTTAB       = GT_DISP
      IT_FIELDCATALOG = GT_FCAT.


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

* 도메인 텍스트 조회
  PERFORM GET_DOMAIN_TEXT.

* 인사마스터 조회
  PERFORM GET_EMPLOYEE_MASTER.

* 데이터취합
  PERFORM MERGE_DATA.

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
   WHERE DOMNAME = GC_DOM_DEPT.        "'ZD00_DEPT'.

  SELECT DOMVALUE_L
         DDTEXT
    INTO TABLE GT_DEPT
    FROM DD07T
   WHERE DOMNAME = GC_DOM_DEPT.        "'ZD00_DEPT'.

  SELECT DOMVALUE_L AS CODE
         DDTEXT     AS TEXT
    INTO CORRESPONDING FIELDS OF TABLE GT_GRADE
    FROM DD07T
   WHERE DOMNAME = GC_DOM_GRADE.       "'ZD00_GRADE'.

  SELECT DOMVALUE_L AS CODE
         DDTEXT     AS TEXT
    INTO CORRESPONDING FIELDS OF TABLE GT_STATUS
    FROM DD07T
   WHERE DOMNAME = GC_DOM_STATUS.      "'ZD00_STATUS'.

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

  LOOP AT GT_DISP ASSIGNING <FS_DISP>.           "INTO GS_DISP.

    PERFORM GET_TEXT_SINGLE_LINE CHANGING <FS_DISP>.

* icon 위한 추가 내용
    <FS_DISP>-STAT = ICON_GREEN_LIGHT.
  ENDLOOP.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form GET_TEXT_SINGLE_LINE
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*      <--P_<FS_DISP>  text
*&---------------------------------------------------------------------*
FORM GET_TEXT_SINGLE_LINE  CHANGING PS_DATA LIKE GS_DISP.

* 부서내역
  PERFORM GET_DEPT_TEXT USING     PS_DATA-DEPT
                        CHANGING  PS_DATA-DEPT_T.

* 직급 내역
  PERFORM GET_GRADE_TEXT USING     PS_DATA-GRADE
                         CHANGING  PS_DATA-GRADE_T.

* 재직구분 내역
  PERFORM GET_STATUS_TEXT USING     PS_DATA-STATUS
                          CHANGING  PS_DATA-STATUS_T.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form SET_EVENT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM SET_EVENT .

* EVENT RECEIVER INSTANCE 생성
  CREATE OBJECT GO_EVENT_RECEIVER.

* ALV에 EVENT 등록
  SET HANDLER GO_EVENT_RECEIVER->HANDLE_DOUBLE_CLICK
          FOR GO_GRID.

  SET HANDLER GO_EVENT_RECEIVER->HANDLE_DATA_CHANGED
          FOR GO_GRID.

** 이벤트 발생
  CALL METHOD GO_GRID->REGISTER_EDIT_EVENT
    EXPORTING
      I_EVENT_ID = CL_GUI_ALV_GRID=>MC_EVT_MODIFIED.




ENDFORM.
*&---------------------------------------------------------------------*
*& Form HANDLE_DATA_CHANGED
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*      -->P_ER_DATA_CHANGED  text
*&---------------------------------------------------------------------*
FORM HANDLE_DATA_CHANGED  USING    PO_DATA_CHANGED TYPE REF TO CL_ALV_CHANGED_DATA_PROTOCOL.

  DATA : LS_CHANGED TYPE LVC_S_MODI,
         LV_TEXT    TYPE DD07T-DDTEXT.

  LOOP AT PO_DATA_CHANGED->MT_GOOD_CELLS INTO LS_CHANGED.

    CASE LS_CHANGED-FIELDNAME.
      WHEN 'DEPT'.    "부서변경
        "부서명 조회
        PERFORM GET_DEPT_TEXT USING    LS_CHANGED-VALUE
                              CHANGING LV_TEXT.

        "ALV 및 INTERNAL TABLE 에 반영
        CALL METHOD PO_DATA_CHANGED->MODIFY_CELL
          EXPORTING
            I_ROW_ID    = LS_CHANGED-ROW_ID
            I_FIELDNAME = 'DEPT_T'
            I_VALUE     = LV_TEXT.

      WHEN 'GRADE'.
        "직급명 조회
        PERFORM GET_GRADE_TEXT USING     LS_CHANGED-VALUE
                               CHANGING  LV_TEXT.

        "ALV 및 INTERNAL TABLE 에 반영
        CALL METHOD PO_DATA_CHANGED->MODIFY_CELL
          EXPORTING
            I_ROW_ID    = LS_CHANGED-ROW_ID
            I_FIELDNAME = 'GRADE_T'
            I_VALUE     = LV_TEXT.

      WHEN 'STATUS'.
        "재직구분내역 조회
        PERFORM GET_STATUS_TEXT USING     LS_CHANGED-VALUE
                                CHANGING  LV_TEXT.

        "ALV 및 INTERNAL TABLE 에 반영
        CALL METHOD PO_DATA_CHANGED->MODIFY_CELL
          EXPORTING
            I_ROW_ID    = LS_CHANGED-ROW_ID
            I_FIELDNAME = 'STATUS_T'
            I_VALUE     = LV_TEXT.

        CALL METHOD PO_DATA_CHANGED->MODIFY_CELL
          EXPORTING
            I_ROW_ID    = LS_CHANGED-ROW_ID
            I_FIELDNAME = 'STAT'
            I_VALUE     = ICON_YELLOW_LIGHT.
    ENDCASE.

  ENDLOOP.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form GET_DEPT_TEXT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*      -->P_LS_CHANGED_VALUE  text
*      <--P_LV_TEXT  text
*&---------------------------------------------------------------------*
FORM GET_DEPT_TEXT  USING    P_CODE
                    CHANGING P_TEXT.

  CLEAR P_TEXT.
  READ TABLE GT_DEPT INTO GS_TEXT
                     WITH KEY CODE = P_CODE
                     BINARY SEARCH.
  IF SY-SUBRC = 0.
    P_TEXT = GS_TEXT-TEXT.
  ENDIF.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form GET_GRADE_TEXT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*      -->P_LS_CHANGED_VALUE  text
*      <--P_LV_TEXT  text
*&---------------------------------------------------------------------*
FORM GET_GRADE_TEXT  USING    P_CODE
                    CHANGING P_TEXT.

  CLEAR P_TEXT.
  READ TABLE GT_GRADE INTO GS_TEXT
                      WITH KEY CODE = P_CODE
                      BINARY SEARCH.
  IF SY-SUBRC = 0.
    P_TEXT = GS_TEXT-TEXT.
  ENDIF.

ENDFORM.
*&---------------------------------------------------------------------*
*& Form GET_STATUS_TEXT
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*      -->P_LS_CHANGED_VALUE  text
*      <--P_LV_TEXT  text
*&---------------------------------------------------------------------*
FORM GET_STATUS_TEXT  USING    P_CODE
                      CHANGING P_TEXT.

  CLEAR P_TEXT.
  READ TABLE GT_STATUS INTO GS_TEXT
                       WITH KEY CODE = P_CODE
                       BINARY SEARCH.
  IF SY-SUBRC = 0.
    P_TEXT = GS_TEXT-TEXT.
  ENDIF.

ENDFORM.
```

```text
*&---------------------------------------------------------------------*
*& Include          ZR00_0000I01
*&---------------------------------------------------------------------*
*&---------------------------------------------------------------------*
*&      Module  EXIT_0100  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
MODULE EXIT_0100 INPUT.

  LEAVE TO SCREEN 0.

ENDMODULE.
*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_0100  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
MODULE USER_COMMAND_0100 INPUT.

  CASE GV_OKCODE.
    WHEN 'SAVE'.
      CALL METHOD GO_GRID->CHECK_CHANGED_DATA.




  ENDCASE.

  CLEAR GV_OKCODE.

ENDMODULE.
```

```text
*&---------------------------------------------------------------------*
*& Include          ZR00_0000O01
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

```text
*&---------------------------------------------------------------------*
*& Include          ZR00_0020SEL
*&---------------------------------------------------------------------*
SELECTION-SCREEN BEGIN OF BLOCK BL1 WITH FRAME TITLE TEXT-T01.
  SELECT-OPTIONS : S_EMPNO  FOR ZT00_0010-EMPNO,
                   S_DEPT   FOR ZT00_0010-DEPT,
                   S_ENTDT  FOR ZT00_0010-ENTDT,
                   S_GRADE  FOR ZT00_0010-GRADE,
                   S_STATUS FOR ZT00_0010-STATUS.
SELECTION-SCREEN END OF BLOCK BL1.
```

```text
*&---------------------------------------------------------------------*
*& Include          ZR00_0000TOP
*&---------------------------------------------------------------------*

TABLES : ZT00_0010.

CONSTANTS : GC_DOM_DEPT       TYPE DOMNAME          VALUE 'ZD00_DEPT',
            GC_DOM_GRADE      TYPE DOMNAME          VALUE 'ZD00_GRADE',
            GC_DOM_STATUS     TYPE DOMNAME          VALUE 'ZD00_STATUS'.

* 화면출력 용(SCREEN 100)
DATA : BEGIN OF GS_DISP.
         INCLUDE STRUCTURE ZT00_0010.
DATA :   STAT     TYPE ICON-ID,
         DEPT_T   TYPE DD07T-DDTEXT,
         GRADE_T  TYPE DD07T-DDTEXT,
         STATUS_T TYPE DD07T-DDTEXT,
         RESULT   TYPE CHAR200,
       END OF GS_DISP.
DATA : GT_DISP LIKE TABLE OF GS_DISP.

* 도메인 텍스트 처리 용
DATA : BEGIN OF GS_TEXT,
         CODE TYPE DD07T-DOMVALUE_L,
         TEXT TYPE DD07T-DDTEXT,
       END OF GS_TEXT.
DATA : GT_DEPT   LIKE TABLE OF GS_TEXT,   "부서내역
       GT_GRADE  LIKE TABLE OF GS_TEXT,   "직급내역
       GT_STATUS LIKE TABLE OF GS_TEXT.   "재직구분 내역

DATA : GV_OKCODE TYPE SY-UCOMM.

************************************************************************
*---- ALV 관련 선언 ----
************************************************************************
DATA : GO_CONTAINER TYPE REF TO CL_GUI_CUSTOM_CONTAINER,
       GO_GRID      TYPE REF TO CL_GUI_ALV_GRID.

DATA : GT_FCAT  TYPE LVC_T_FCAT,
       GS_FCAT   TYPE LVC_S_FCAT,
       GS_LAYOUT TYPE LVC_S_LAYO.
```

