# 실습 - 인사 프로그램 생성

## 1. 인사 데이터 생성

### 1\) Database table 생성 

{% hint style="info" %}
T-code SE11 &gt; Database table &gt; Create
{% endhint %}

인사 테이블과 필요한 사원 마스터 정보 다음 양식에 맞춰 생성해보도록 한다. 

![&#xC0DD;&#xC131;&#xD560; &#xD14C;&#xC774;&#xBE14; &#xC815;&#xBCF4;](../.gitbook/assets/image%20%28165%29.png)

![T-CODE SE11 &amp;gt; DB Table &#xC0DD;&#xC131;](../.gitbook/assets/image%20%28172%29.png)

![DB Table &#xC0DD;&#xC131;](../.gitbook/assets/image%20%28174%29.png)

테이블 정보를 가지고 위와 같이 Database table을 생성해준다. 이왕이면 built-in type으로 직접 data type과 length를 입력하기보다 data element를 생성하여 이를 참조하도록 만들어준다. 즉, data element도 생성해줘야 한다. 이 때, 비고에 range가 존재하는 속성들은 domain을 필수적으로 만들어준다. 이를 통해 domain 값에 따른 range 값을 연결할 수 있기 때문이다. 예를 들어 직급이 A로 표시되었더라도 이것이 대표하는 값이 대표이사임을 알 수 있도록 정보가 필요하다.  



### 2\) Domain 생성

{% hint style="info" %}
T-code SE11 &gt; Domain &gt; Create 또는 Data element 더블 클릭
{% endhint %}

부서, 직급, 재직 구분 속성에 대해서 domain은 필수적이며, 자택 주소와 근무지주소, 퇴사일과 입사일 또한 동일한 데이터 타입, 속성을 가지기 때문에 도메인을 생성해 공동으로 사용 가능하다. 

대표로 직급에 대한 도메인을 생성하는 과정을 보이면 다음과 같다. 동일한 과정으로 나머지 속성에 대한 도메인 또한 생성해주도록 한다. 

![Domain &amp;gt; Definition](../.gitbook/assets/image%20%28176%29.png)

Definition 영역에서 데이터의 타입과, 길이에 대해 설정을 해준다. 

![Domain &amp;gt; Value range](../.gitbook/assets/image%20%28164%29.png)

Domain의 Value range 영역에서 각각 정해진 Fixed Value의 값과 그 값이 의미하는 것이 무엇인지에 대해 기술해준다. 



### 3\) Record structure 생성 및 추가 

해당 데이터에 대해 누가 언제 무엇을 어떻게 변경하였는지 등에 대한 정보를 담을 수 있는 structure를 생성해주도록 한다. 해당 record structure를 이루는 component는 이미 정의된 데이터를 사용하면 된다. 

![Record structure &#xC0DD;&#xC131;](../.gitbook/assets/image%20%28156%29.png)

![](../.gitbook/assets/image%20%28170%29.png)

생성한 structure를 이전에 만든 table에 include로 넣어준다. 

![](../.gitbook/assets/image%20%28155%29.png)

![](../.gitbook/assets/image%20%28162%29.png)

///

![](../.gitbook/assets/image%20%28169%29.png)

상단의 TEXT ELEMENT로 PARAMETER이름 설정 가



![](../.gitbook/assets/image%20%28177%29.png)

///

![](../.gitbook/assets/image%20%28175%29.png)

![](../.gitbook/assets/image%20%28166%29.png)

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

//

FULL SCREEN

![](../.gitbook/assets/image%20%28179%29.png)

![](../.gitbook/assets/image%20%28163%29.png)

EDITING 부분을 최대로 해두면 항상 FULL SCREEN이 된다. 

![](../.gitbook/assets/image%20%28181%29.png)

LAYOUT 부분도 최대로 해눈더, 

//

![](../.gitbook/assets/image%20%28178%29.png)

생성된 버튼에 대한 USER COMMAND 생성

//



![](../.gitbook/assets/image%20%28168%29.png)

통화키를 참조하도록 하여 기본급 SALARY를 설정: GS\_0200-WAERS

