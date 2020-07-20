---
description: SAP에서 제공하는 교육 내용과 Easy ABAP 교재 참조
---

# Screen

## 1. Screen

### Screen 생성

{% hint style="info" %}
T-code SE80 또는 T-code SE51
{% endhint %}

### Screen 위치 

스크린은 SAP GUI에서 조회되는 모든 화면을 의미하며, 사용자와 상호작용을 통해 데이터를 생성하고 조회하는 작업 영역이다. 다음 이미지는 GUI Status와 ABAP Program 사이에서의 Screen 위치를 보여준다. 

스크린이 조회되거나 사용자의 액션이 끝난 후, 자동으로 같은 이름을 가진 스크린 필드들과 ABAP Program의 Data object 사이에 데이터 복사가 일어난다. 이는 PAI 호출시 프로그램 내부적으로 수행되는 과정이다. 

![Screen &#xC704;&#xCE58;](../../.gitbook/assets/image%20%2845%29.png)

### Screen 구성요소

| Name | Explanation |
| :--- | :--- |
| Screen attributes | 스크린 번호, 타입, 이름, 내역, 창 크기, 다음 화면을 정의 SAP 시스템에 Screen object를 연결 |
| Screen element \(Layout\) | 사용자가 데이터를 조회하고 입력하는 GUI 화면을 디자인하는데 사용 텍스트 필드, Input/Output 필드, 체크박스 등과 같은 구성 요소 정의 |
| Field attributes | 메인 스크린 필드의 데이터 타입과 길이 등을 정의하는 부분 |
| Flow logic \(Module pool\) | User action에 따른 PAI, PBO 절차 수행 부분을 정의 |

![Screen &#xAD6C;&#xC131;&#xC694;&#xC18C;](../../.gitbook/assets/image%20%2855%29.png)



## 2. Screen Attributes

* Screen number 1000~1010 : 표준 SELECTION SCREEN, ABAP Dictionary Maintenance Screen 

![Screen &amp;gt; Screen attributes](../../.gitbook/assets/image%20%2853%29.png)

### Screen attributes 세부사항

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key field</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Screen number</td>
      <td style="text-align:left">&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xB0B4;&#xBD80;&#xC5D0;&#xC11C; &#xC2A4;&#xD06C;&#xB9B0;&#xC744;
        &#xAD6C;&#xBCC4;&#xD558;&#xB294; 4&#xC790;&#xB9AC; &#xC22B;&#xC790;</td>
    </tr>
    <tr>
      <td style="text-align:left">Screen type</td>
      <td style="text-align:left">
        <p>Normal : &#xC2A4;&#xD06C;&#xB9B0;&#xC774; &#xC804;&#xCCB4; GUI &#xCC3D;&#xC744;
          &#xC810;&#xC720;
          <br />Subscreen : Subscreen &#xC601;&#xC5ED; &#xC548;&#xC5D0;&#xC11C; &#xC0AC;&#xC6A9;&#xD558;&#xB294;
          &#xC2A4;&#xD06C;&#xB9B0;</p>
        <p>Modal dialog box : &#xD31D;&#xC5C5; &#xCC3D; &#xD615;&#xD0DC;&#xB85C;
          &#xC885;&#xB8CC;&#xC548;&#xD558;&#xBA74; &#xB2E4;&#xB978; &#xC2A4;&#xD06C;&#xB9B0;
          &#xC120;&#xD0DD; &#xBD88;&#xAC00;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Next screen</td>
      <td style="text-align:left">&#xD638;&#xCD9C;&#xD55C; &#xC2A4;&#xD06C;&#xB9B0;&#xC758; PAI &#xC2E4;&#xD589;
        &#xD6C4; &#xC2E4;&#xD589; &#xD560; &#xC2A4;&#xD06C;&#xB9B0; &#xC124;&#xC815;</td>
    </tr>
    <tr>
      <td style="text-align:left">Cursor position</td>
      <td style="text-align:left">
        <p>&#xC2A4;&#xD06C;&#xB9B0;&#xC774; display &#xB420; &#xB54C;&#xC758; &#xCEE4;&#xC11C;
          &#xC704;&#xCE58; &#xC124;&#xC815;</p>
        <p>Default &#xAC12;&#xC740; &#xCCAB; &#xD544;&#xB4DC;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Screen group</td>
      <td style="text-align:left">
        <p>&#xC2A4;&#xD06C;&#xB9B0; &#xC2E4;&#xD589; &#xB3D9;&#xC548; SY-DYNGR&#xC5D0;
          &#xC800;&#xC7A5;</p>
        <p>ABAP Dictionary table TFAWT&#xC5D0; &#xC800;&#xC7A5;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Hold data</td>
      <td style="text-align:left">
        <p>&#xC0AC;&#xC6A9;&#xC790; &#xD504;&#xB85C;&#xD30C;&#xC77C;&#xC5D0; &#xC800;&#xC7A5;&#xB41C;
          &#xB370;&#xC774;&#xD130;&#xB97C; &#xC2A4;&#xD06C;&#xB9B0;&#xC758; &#xAE30;&#xBCF8;
          &#xAC12;&#xC73C;&#xB85C; &#xC124;&#xC815;&#xD558;&#xAE30; &#xC704;&#xD568;</p>
        <p>ABAP Memory &#xC601;&#xC5ED; &#xB370;&#xC774;&#xD130; &#xC0AC;&#xC6A9;
          &#xC548;&#xD568;</p>
        <p>&#xC124;&#xC815;&#xC2DC;, System &gt; User profile &gt; Hold data &#xC124;&#xC815;&#xC5D0;&#xC11C;
          &#xAE30;&#xB2A5; &#xC774;&#xC6A9; &#xAC00;</p>
      </td>
    </tr>
  </tbody>
</table>



## 3. Screen Element \(Layout\)

데이터를 보여주거나 사용자들과 대화, User dialog 하는 기능을 한다.   
필드에 값을 입력하거나 버튼을 클릭하는 행위가 이에 속한다.   
이미 만들어진 tool을 사용하여 쉽게 생성할 수 있다. 

![Screen &amp;gt; Layout](../../.gitbook/assets/image%20%2856%29.png)



## 4. Field Attributes

* 스크린의 작업 영역 메모리에 존재하는 필드
* PAI 발생 전 시점에 ABAP Program 동일 필드명 필드로 값 전달/복
* Screen field와 Program field는 동일한 필드명으로 선언되어야 함
* 이벤트 수행시 설정 값이 OK\_CODE에 저장됨

![Screen field &amp; Program field](../../.gitbook/assets/image%20%2844%29.png)



## 5. Screen Flow Logic \(Module pool\)

* 스크린이 절차적을 실행되어야 하는 부분
* ABAP 언어와 유사하지만 다른 언어임에 유의



### Processing block

Processing block은 Module 기능으로 이루어지며, 이러한 측면에서 Type-M 프로그램을 Module pool program 이라고 한다. 

| Processing block | Meaning |
| :--- | :--- |
| \(PBO\) PROCESS BEFORE OUTPUT  | 화면 초기 설정 |
| \(PAI\) PROCESS AFTER INPUT | 사용자 액션 수행시 발생하는 이벤트 블록 |
| \(POH\) PROCESS ON HELP-REQUEST | F1 눌렀을 때 발생하는 이벤트 블록 |
| \(POV\) PROCSEE ON VALUE-REQUEST | F4 눌렀을 때 발생하는 이벤트 블 |



### Flow logic keyword

<table>
  <thead>
    <tr>
      <th style="text-align:left">Keyword</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">CALL</td>
      <td style="text-align:left">Subscreen &#xD638;&#xCD9C;</td>
    </tr>
    <tr>
      <td style="text-align:left">MODULE</td>
      <td style="text-align:left">Processing Module &#xC815;&#xC758; &#xBC0F; Dialog Module &#xD638;&#xCD9C;</td>
    </tr>
    <tr>
      <td style="text-align:left">FIELD ~ ON</td>
      <td style="text-align:left">
        <p>Screen &#xD544;&#xC5D0;&#xC11C; ABAP &#xD544;&#xB4DC;&#xB85C; &#xB370;&#xC774;&#xD130;
          &#xBCF5;&#xC0AC;</p>
        <p>Screen &#xD544;&#xB4DC;&#xB294; PAI &#xC218;&#xD589; &#xC804; ABAP &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC5D0;&#xC11C;
          &#xC81C;&#xC5B4; &#xBD88;&#xAC00;&#xB2A5; &#xD558;&#xC9C0;&#xB9CC;,</p>
        <p>FIELD &#xC120;&#xC5B8;&#xC2DC; PAI &#xC218;&#xD589;&#xD558;&#xC9C0; &#xC54A;&#xC544;&#xB3C4;
          ABAP &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC5D0;&#xC11C; &#xB370;&#xC774;&#xD130;
          &#xCCB4;&#xD06C; &#xAC00;&#xB2A5;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">VALUES</td>
      <td style="text-align:left">
        <p>Input &#xAC12; &#xC815;&#xC758; (&#xB2E4;&#xB978; &#xAC12;&#xC774; &#xC815;&#xC758;&#xB418;&#xBA74;</p>
        <p>Field keyword&#xC640; &#xAC19;&#xC774; &#xC0AC;&#xC6A9;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">CHAIN / ENDCHAIN</td>
      <td style="text-align:left">&#xC5EC;&#xB7EC; &#xD544;&#xB4DC;&#xB97C; &#xADF8;&#xB8F9;&#xC73C;&#xB85C;
        &#xCC98;&#xB9AC;</td>
    </tr>
    <tr>
      <td style="text-align:left">LOOP / ENDLOOP</td>
      <td style="text-align:left">Screen&#xC5D0; &#xB300;&#xD574; &#xBC18;&#xBCF5; process &#xCC98;&#xB9AC;</td>
    </tr>
    <tr>
      <td style="text-align:left">MODIFY</td>
      <td style="text-align:left">Screen table &#xBCC0;&#xACBD;</td>
    </tr>
    <tr>
      <td style="text-align:left">PROCESS</td>
      <td style="text-align:left">Process &#xC774;&#xBCA4;&#xD2B8; &#xC815;&#xC758;</td>
    </tr>
    <tr>
      <td style="text-align:left">SELECT</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>



## 6. User Action

User action이란 말 그대로 사용자의 행위를 의미한다. 다음과 같은 다양한 방식으로 사용자는 action을 취할 수 있다.

* Input Field Data 입력
* PAI 이벤트 실행 
* Processing Input/Output Field
* F1 \(Field Help\)
* F4 \(Search Help\)

### Field Help

사용자가 F1을 누르거나 Help 아이콘을 클릭하면 현재 커서가 존재하는 필드의 텍스트 도움말이 조회된다. 만약, ABAP Dictionary에 생성된 Data Element Document가 존재하면 자동 첨부되며, 추가 내용은 Useful Skill 부분을 참조하자. 

### Input Help

Category 9에서 상세하게 다뤘으니 참조하도록 한다. Input help는 3가지 방법으로 스크린에 추가 가능하다.

<table>
  <thead>
    <tr>
      <th style="text-align:left">How</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ABAP Dictionary</td>
      <td style="text-align:left">Search help&#xB97C; &#xC0DD;&#xC131;&#xD558;&#xC5EC; Table field&#xC5D0;
        &#xD560;&#xB2F9;&#xD558;&#xACE0;,
        <br />&#xC774;&#xB97C; &#xC0C1;&#xC18D;&#xBC1B;&#xB294; Screen field&#xB97C;
        &#xC120;&#xC5B8;&#xD55C;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">Screen</td>
      <td style="text-align:left">
        <p>Screen painter&#xC5D0;&#xC11C; &#xAC1C;&#xBCC4; Screen field&#xC5D0; &#xC9C1;&#xC811;
          &#xD560;&#xB2F9;&#xD558;&#xAC70;&#xB098;,</p>
        <p>PAI &#xC774;&#xBCA4;&#xD2B8;&#xC5D0;&#xC11C; &#xC785;&#xB825; &#xAC12;&#xC744;
          &#xC81C;&#xD55C;&#xD55C;&#xB2E4;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Dialog Module</td>
      <td style="text-align:left">F4 &#xBC84;&#xD2BC;&#xC744; &#xB204;&#xB97C; &#xB54C;,
        <br />PROCESS ON VALUE-REQUEST &#xC5D0;&#xC11C; Dialog module&#xC744; &#xD638;&#xCD9C;&#xD558;&#xB3C4;&#xB85D;
        &#xD55C;&#xB2E4;.</td>
    </tr>
  </tbody>
</table>

