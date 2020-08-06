---
description: >-
  조회된 화면에서 데이터를 수정하여 저장하고, 저장 과정에 대해 신호등 표시로 보이게끔 기능을 추가해본다. 이 때, 데이터 수정 및 저장하는
  구문은 BAPI Function을 사용한다.
---

# 수정 및 저장 기능 추가

## 1. Screen status 기능 추가

Screen 설정 중 SET PF-STATUS 에서 Function에 대한 아이콘과 Function code를 설정해준다. 

![Screen 0100 &amp;gt; PBO &amp;gt; SET PF-STATUS](../../.gitbook/assets/image%20%28316%29.png)

Function code에 따른 action을 module로 작성해서 PAI에 작성해준다. 

![Screen 0100 &amp;gt; PAI &amp;gt; USER\_COMMAND\_0100](../../.gitbook/assets/image%20%28293%29.png)



## 2. 수정 기능 추가

> ALV에 조회된 화면에서 수정이 발생한 경우 신호등 색상을 노란색, 오류가 발생한 경우 빨간색으로 변경하고자 한다. ALV 데이터에서 변화가 생겼다는 정보를 담은 EVENT를 활용한다.

{% hint style="info" %}
CL\_GUI\_ALV\_GRID 클래스의 DATA\_CHANGED 이벤트 활용 
{% endhint %}



### 1\) Class 생성

ALV GRID에서 데이터 변경이 발생하엿을 때, HANDLE\_DATA\_CHANGED method를 실행하도록 선언해준다. 

![Class &amp;gt; LCL\_EVENT\_RECEIVER](../../.gitbook/assets/image%20%28286%29.png)

### 2\) Method 정의

위에서 생성한 HANDLE\_DATA\_CHANGED 이름의 method가 발생했을 때, 실행 method를 다음과 같이 정의해준다. 

{% hint style="info" %}
CL\_GUI\_ALV\_GRID 클래스의 MODIFY\_CELL 메소드 활용 
{% endhint %}

CL\_GUI\_ALV\_GRID 클래스의 MODIFY\_CELL 메소드를 불러서 사용하는데, 변경 데이터에 대한 값이 클래스 형태여서 혼란을 줄 수 있다. 따라서 이를 아얘 다른 변수\(ex. LT\_CHANGED\)로 선언하고 사용해도 된다. 

변경된 데이터가 존재하는 ROW에 대해 상태\(STATUS\) 필드의 값을 ICON\_LED\_YELLOW, 즉 노란 신호등으로 변경하도록 설정한다. 

![Class &amp;gt; HANDLE\_DATA\_CHANGED](../../.gitbook/assets/image%20%28283%29.png)



### 3\) 참조 변수 선언

참조 변수는 이벤트를 참조해서 선언하고, TOP이 아닌 CLASS 선언 밑에 해준다. 

![Class &amp;gt; LCL\_EVENT\_RECEIVER](../../.gitbook/assets/image%20%28279%29.png)



### 4\) 객체 생성

선언한 참조 변수로 객체를 생성해준다. Display ALV 이전에 해주면 되고, 깔끔한 코드 정리를 위해 PERFORM으로 묶어 정의했다. 

![Screen 0100 &amp;gt; SET\_ALV\_0100](../../.gitbook/assets/image%20%28317%29.png)

![SET\_ALV\_0100 &amp;gt; SET\_EVENT](../../.gitbook/assets/image%20%28304%29.png)



### 5\) SET HANDLER 선언

Class를 사용하기 위한 마지막으로 SET HANDLER를 선언해준다. 

![SET\_ALV\_0100 &amp;gt; SET\_EVENT](../../.gitbook/assets/image%20%28282%29.png)



## 3. 저장 기능 추가

수정된 데이터를 저장하기 위해서는 다음 과정이 필요하다.  

1. 데이터 및 WA 선언
2. 변경 데이터 유무 체크
3. BAPI 실행 데이터 확보
4. BAPI 실행
5. 변경 데이터 반영

각각 과정을 분리해두었지만, SAVE\_DATA 하나의 PERFORM에 작성되며, SAVE\_DATA PERFORM은 Screen 0100의 PAI 중 USER\_COMMAND\_0100에서 SAVE 버튼이 클릭되었을 때 실행되도록 작성했다.

![Screen 0100 &amp;gt; USER\_COMMAND\_0100](../../.gitbook/assets/image%20%28325%29.png)



### 1\) 데이터 및 WA 선언

{% hint style="info" %}
BAPI\_PO\_CHANGE : 변경 데이터 저을 위한 BAPI 함수 
{% endhint %}

변경된 데이터를 저장을 위해 직접 SQL을 작성하지 말고, BAPI 함수를 사용한다. 현재 우리가 저장하고자 하는 변경 데이터는 EKKO, 즉 구매오더에 대한 내용이기 때문에 BAPI\_PO\_CHANGE 함수를 활용한다. 

BAPI\_PO\_CHANGE 함수를 사용하기 위해서는 변경되어 저장할 필드 명이 무엇인지, 변경 내용을 저장할 것인지에 대한 값을 넣어줘야 한다. 따라서 다음과 같은 데이터와 WA를 선언해준다.

* BAPIRET2 : BAPI 함수 실행 후 반한되는 값
* BAPIMEPOHEADER : BAPI 함수를 실행할 필드명
* BAPIMEPOHEADERX : X 체크를 통해 변경 허용

![SET\_DATA &amp;gt; &#xD544;&#xC694;&#xD55C; &#xB370;&#xC774;&#xD130; &#xBC0F; WA &#xC120;&#xC5B8;](../../.gitbook/assets/image%20%28334%29.png)



### 2\)  변경 데이터 유무 체크 

ITAB을 읽어들이되, STATUS 신호등의 값이 노란색이거나 빨간색인 경우의 조건을 주어 변경된 데이터만 읽어들인다. 만약 STATUS = ICON\_LED\_YELLOW 라는 하나의 조건 만을 사용한다면 ITAB을 읽을 때 사용하는 READ ~ WITH KEY 구문을 사용할 수 있지만, 두 개 이상의 조건을 적용할 대는 LOOP를 사용해야 한다. 

{% hint style="info" %}
READ 인터널 테이블 WITH KEY 필드명 : 하나의 KEY만 가
{% endhint %}

#### 

#### 변경 데이터 없는 경우

데이터가 없어 읽어들이지 못했을 경우, SY-SUBRC&lt;&gt;0 에는 S006의 메세지를 띄운다.

![SET\_DATA &amp;gt; &#xBCC0;&#xACBD; &#xB370;&#xC774;&#xD130; &#xC720;&#xBB34; &#xCCB4;&#xD06C;](../../.gitbook/assets/image%20%28324%29.png)

해당 메세지는 MAIN PROGRAM 상단의 MESSAGE ID에 정의된 메세지 클래스로 메세지를 저장해서 쓸 수 있다. 

![MAIN PROGRAM &#xC0C1;&#xB2E8;&#xC5D0; &#xC815;&#xC758;&#xD55C; MESSAGE ID ](../../.gitbook/assets/image%20%28330%29.png)

![MESSAGE ID SM00](../../.gitbook/assets/image%20%28326%29.png)

#### 

#### 변경 데이터 있는 경우 

아무 문제없이 위의 코드가 실행되었을 때, 사용자에게 다시 한 번 데이터 변경 확인을 받기 위한 부가적 기능을 설정해준다. 팝업 창을 띄워 계속 진행할지 의사를 묻는 것으로 POP\_UP\_TO\_CONFIRM 함수를 활용한다. 

{% hint style="info" %}
POP\_UP\_TO\_CONFIRM 함수 활용 
{% endhint %}

팝업 창이 뜨고 사용자가 클릭한 버튼이 YES 즉 1인지 확인 후 다음 과정을 실행하게 한다. 

![Screen 0100 &amp;gt; USER\_COMMAND\_0100 &amp;gt; SAVE\_DATA](../../.gitbook/assets/image%20%28337%29.png)

![SAVE\_DATA &amp;gt; USER\_CONFRIM](../../.gitbook/assets/image%20%28328%29.png)



### 3\) BAPI 실행 데이터 확보

변경 데이터인 경우, STATUS = ICON\_LED\_YELLOW 조건으로 읽어들이고, 위에서 선언한 데이터 및 WA에 다음과 같은 값을 넣어준다. 

해석하자면,  기존 구매오더 SALES\_PER 필드 값을 GS\_DISP-VERKF 값으로 변경할 것이며 'X' 값을 줌으로써 변경을 허락한다는 의미다. 전화번호 또한 마찬가지의 의미다.

이렇게 변경하고자 하는 부분과 변경할 데이터를 확보해 연결해주었다. 

![SAVE\_DATA &amp;gt; BAPI &#xC2E4;&#xD589; &#xB370;&#xC774;&#xD130; &#xD655;&#xBCF4;](../../.gitbook/assets/image%20%28339%29.png)



### 4\) BAPI 실행

BAPI\_PO\_CHANGE 함수를 호출하고, 다음 값을 설정해준다. RETURN은 필수값이다.

* PURCHASEORDER : 변경할 구매오더 문서 번호 
* POHEADER : 변경할 필드명
* POHEADERX : 변경 여
* RETUN : 실행 후 받을 값

![SAVE\_DATA &amp;gt; BAPI &#xC2E4;&#xD589; \(1\)](../../.gitbook/assets/image%20%28335%29.png)

위의 코드만으로도 가능하지만, 만일에 변경 사항이 제대로 반영되지 못할 경우에 대한 ERROR HANDLING 구문을 다음과 같이 작성해준다. 



#### BAPI 실행 오류 

{% hint style="info" %}
BAPI\_TRANSACTION\_ROLLBACK
{% endhint %}

LT\_RETURN 값은 문자열인데, 이 값이 ERROR인 경우가 바로 실패인 경우다. 따라서 LT\_RETURN에 TYPE = 'E'를 조건으로 데이터를 읽어들이고, 읽는데 성공한 경우 그 ERROR 값이 있는 것이기 때문에 실패 처리로 ROLLBACK 함수를 호출한다.

오류가 있는 경우, STATUS 값을 빨간 신호등으로 바꿔준다. 그리고 RESULT 필드에 오류 내역을 넣어서 확인할 수 있게 해준다. 이 또한, 오류가 둘 이상일 경우가 있기 때문에 INITIAL인 경우는 단순하게 추가하고, IS NOT INITIAL인 경우에는 이전 오류 내역과 문자열 합침, CONCATENATE 하여 값을 넣어주도록 한다.  

![SAVE\_DATA &amp;gt; BAPI &#xC2E4;&#xD589; \(2\)](../../.gitbook/assets/image%20%28327%29.png)



#### BAPI 실행 완료 

{% hint style="info" %}
BAPI\_TRANSACTION\_COMMIT
{% endhint %}

LT\_RETURN에서 오류 내역을 읽어드리지 못하는 경우는 오류가 없이 온전히 실행되었기 때문이다. 이 경우에는 BAPI\_TRANSACTION\_COMMIT 함수를 호출한다. BAPI 실행 후 무조건! 필수적으로 해줘야 한다. WAIT 값에 'X'를 주면 이전 transaction이 실행된 후 충돌없이 commit을 수행하라는 의미이기 때문에 주는 것이 좋다. 

추가적으로 변경 데이터를 반영한 후에는 신호등 색을 다시 녹색으로 바꾸어주도록 했다. 

![SAVE\_DATA &amp;gt; BAPI &#xC2E4;&#xD589; \(2\)](../../.gitbook/assets/image%20%28327%29.png)

BAPI 실행에 대한 전체 코드는 다음과 같다.

![SAVE\_DATA &amp;gt; BAPI &#xC2E4;&#xD589; \(&#xC804;&#xCCB4;\)](../../.gitbook/assets/image%20%28321%29.png)



### 5\) 변경 데이터 반영

마지막으로 변경된 데이터를 반영해준다. 3번부터 여기까지의 과정이 하나의 LOOP 안에 실행되고 있음에 유의한다. 

![SAVE\_DATA &amp;gt; &#xBCC0;&#xACBD; &#xB370;&#xC774;&#xD130; &#xBC18;&#xC601;](../../.gitbook/assets/image%20%28332%29.png)



## 4. 결과 화면

### Selection screen

![Selection screen](../../.gitbook/assets/image%20%28333%29.png)

### Screen 0100 - 데이터 변경 전

![Screen 0100](../../.gitbook/assets/image%20%28331%29.png)

### Screen 0100 - 데이터 변경 후

![Screen 0100 - &#xC800;&#xC7A5; &#xBC84;&#xD2BC; &#xD074;&#xB9AD; &#xC804;](../../.gitbook/assets/image%20%28323%29.png)

![Screen 0100 - &#xC800;&#xC7A5; &#xBC84;&#xD2BC; &#xD074;&#xB9AD; &#xD6C4;](../../.gitbook/assets/image%20%28329%29.png)



## 5. 코드 

### Main Program

```sql
*&---------------------------------------------------------------------*
*& Report ZS_0001
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT ZSL_24_012 MESSAGE-ID ZM00.

INCLUDE ZSL_24_012TOP.
INCLUDE ZSL_24_012CLS.
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
*& Report ZS_0001
*&---------------------------------------------------------------------*
*&
*&---------------------------------------------------------------------*
REPORT ZSL_24_012 MESSAGE-ID ZM00.

INCLUDE ZSL_24_012TOP.
INCLUDE ZSL_24_012CLS.
INCLUDE ZSL_24_012SEL.
INCLUDE ZSL_24_012F01.
INCLUDE ZSL_24_012I01.
INCLUDE ZSL_24_012O01.

START-OF-SELECTION.

PERFORM GET_DATA.
a
CALL SCREEN '0100'.
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
  MODULE USER_COMMAND_0100.
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

###  Class

```sql
*&---------------------------------------------------------------------*
*& Include          ZSL_24_012CLS
*&---------------------------------------------------------------------*

CLASS LCL_EVENT_RECEIVER DEFINITION.
  PUBLIC SECTION.

    METHODS: HANDLE_DATA_CHANGED
               FOR EVENT DATA_CHANGED OF CL_GUI_ALV_GRID
               IMPORTING ER_DATA_CHANGED.
ENDCLASS.


CLASS LCL_EVENT_RECEIVER IMPLEMENTATION.
  METHOD: HANDLE_DATA_CHANGED.
    PERFORM HANDLE_DATA_CHANGED USING ER_DATA_CHANGED.
  ENDMETHOD.
ENDCLASS.


DATA : GO_EVENT_RECEIVER TYPE REF TO LCL_EVENT_RECEIVER.
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

*&---------------------------------------------------------------------*
*&      Module  USER_COMMAND_0100  INPUT
*&---------------------------------------------------------------------*
*       text
*----------------------------------------------------------------------*
MODULE USER_COMMAND_0100 INPUT.
  CASE GV_OKCODE.
    WHEN 'SAVE'.
      PERFORM SAVE_DATA.
    WHEN 'EXIT' OR 'CANC'.
      LEAVE TO SCREEN 0.
  ENDCASE.
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

* EVENT 세팅
    PERFORM SET_EVENT.

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
  GS_LAYOUT-SEL_MODE   = 'D'.  

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

* layout no-row-insert 하면 조회하면에서 insert row 불가
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
*& Form SAVE_DATA
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*& -->  p1        text
*& <--  p2        text
*&---------------------------------------------------------------------*
FORM SAVE_DATA .

* 1. 필요한 데이터 및 WA 선언
  DATA: LT_RETURN  TYPE TABLE OF BAPIRET2,
        LS_HEADER  TYPE BAPIMEPOHEADER,
        LS_HEADERX TYPE BAPIMEPOHEADERX,
        LS_RETURN  TYPE          BAPIRET2.
  DATA LV_ANSWER TYPE C.


* 2. 변경 데이터 유무 체크
*  READ TABLE GT_DISP INTO GS_DISP WITH KEY STATUS = ICON_LED_YELLOW.
*  조건을 하나만 줄 수 있음: 두개 이상의 조건을 주려면?
  LOOP AT GT_DISP INTO GS_DISP WHERE STATUS = ICON_LED_YELLOW
                                  OR STATUS = ICON_LED_RED.
  ENDLOOP.

  IF SY-SUBRC <> 0.
    MESSAGE S006.
    EXIT.
  ENDIF.

* USER CONFIRM
  PERFORM USER_CONFIRM USING    TEXT-Q01
                                TEXT-Q02 "구매오더가 변경됩니다. 계속 진행하시겠습니까?"
                       CHANGING LV_ANSWER.
  CHECK LV_ANSWER EQ '1'.






* 3. BAPI 실행 데이터 확보
  LOOP AT GT_DISP INTO GS_DISP WHERE STATUS = ICON_LED_YELLOW.

    CLEAR: LS_HEADER, LS_HEADERX.
    LS_HEADER-SALES_PERS = GS_DISP-VERKF.
    LS_HEADERX-SALES_PERS = 'X'.
    LS_HEADER-TELEPHONE = GS_DISP-TELF1.
    LS_HEADERX-TELEPHONE = 'X'.


* 4. BAPI 실행
    CALL FUNCTION 'BAPI_PO_CHANGE'
      EXPORTING
        PURCHASEORDER = GS_DISP-EBELN
        POHEADER      = LS_HEADER
        POHEADERX     = LS_HEADERX
      TABLES
        RETURN        = LT_RETURN.

     READ TABLE LT_RETURN INTO LS_RETURN WITH KEY TYPE = 'E'.
     IF SY-SUBRC = 0.
       "실패처리"
       CALL FUNCTION 'BAPI_TRANSACTION_ROLLBACK'.
         GS_DISP-STATUS = ICON_LED_RED.
         CLEAR GS_DISP-RESULT.
         LOOP AT LT_RETURN INTO LS_RETURN WHERE TYPE = 'E'.
           IF GS_DISP-RESULT IS INITIAL.
             GS_DISP-RESULT = LS_RETURN-MESSAGE.
           ELSE.
             CONCATENATE GS_DISP-RESULT LS_RETURN-MESSAGE
             INTO GS_DISP-RESULT
             SEPARATED BY '&'.
           ENDIF.
         ENDLOOP.
     ELSE.
       CALL FUNCTION 'BAPI_TRANSACTION_COMMIT'   "BAPI 실행 후 수행 필수!
         EXPORTING
           WAIT = 'X'.
           GS_DISP-STATUS = ICON_LED_GREEN.
     ENDIF.


* 5. 변경 데이터 반영
     MODIFY GT_DISP FROM GS_DISP.

  ENDLOOP.
ENDFORM.
*&---------------------------------------------------------------------*
*& Form USER_CONFIRM
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*      -->P_TEXT_Q01  text
*      -->P_TEXT_Q02  text
*      <--P_LV_ANSWER  text
*&---------------------------------------------------------------------*
FORM USER_CONFIRM  USING    P_TITLE
                            P_QUEST
                   CHANGING P_ANSWER.

  CLEAR : P_ANSWER.

  CALL FUNCTION 'POPUP_TO_CONFIRM'
    EXPORTING
      TITLEBAR      = P_TITLE
      TEXT_QUESTION = P_QUEST
      TEXT_BUTTON_1 = 'YES'
      TEXT_BUTTON_2 = 'NO'
    IMPORTING
      ANSWER        = P_ANSWER.
ENDFORM.

*&---------------------------------------------------------------------*
*& Form HANDLE_DATA_CHANGED
*&---------------------------------------------------------------------*
*& text
*&---------------------------------------------------------------------*
*      -->P_ER_DATA_CHANGED  text
*&---------------------------------------------------------------------*
FORM HANDLE_DATA_CHANGED  USING PO_DATA_CHANGED 
                          TYPE REF TO CL_ALV_CHANGED_DATA_PROTOCOL.

  DATA : LS_CHANGED TYPE LVC_S_MODI.

* LT_CHANGED = PO_DATA_CHANGED->MT_GOOD_CELLS로 선언하고,
* 아래 구문에서 LOOP AT LT_CHANGED INTO LS_CHANGED로 사용해도 가능
  LOOP AT PO_DATA_CHANGED->MT_GOOD_CELLS INTO LS_CHANGED.

        CALL METHOD PO_DATA_CHANGED->MODIFY_CELL
          EXPORTING
            I_ROW_ID    = LS_CHANGED-ROW_ID
            I_FIELDNAME = 'STATUS'
            I_VALUE     = ICON_LED_YELLOW.

  ENDLOOP.
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
  CREATE OBJECT GO_EVENT_RECEIVER.
  SET HANDLER GO_EVENT_RECEIVER->HANDLE_DATA_CHANGED FOR GO_GRID.

* 변경 발생시 이벤트 발생
  CALL METHOD GO_GRID->REGISTER_EDIT_EVENT
    EXPORTING
      I_EVENT_ID = CL_GUI_ALV_GRID=>MC_EVT_MODIFIED.
ENDFORM.
```











