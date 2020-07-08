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

![Screen &#xC704;&#xCE58;](../.gitbook/assets/image%20%2845%29.png)

### Screen 구성요소

| Name | Explanation |
| :--- | :--- |
| Screen attributes | 스크린 번호, 타입, 이름, 내역, 창 크기, 다음 화면을 정의 SAP 시스템에 Screen object를 연결 |
| Screen element \(Layout\) | 사용자가 데이터를 조회하고 입력하는 GUI 화면을 디자인하는데 사용 텍스트 필드, Input/Output 필드, 체크박스 등과 같은 구성 요소 정의 |
| Field attributes | 메인 스크린 필드의 데이터 타입과 길이 등을 정의하는 부분 |
| Flow logic \(Module pool\) | User action에 따른 PAI, PBO 절차 수행 부분을 정의 |

![Screen &#xAD6C;&#xC131;&#xC694;&#xC18C;](../.gitbook/assets/image%20%2855%29.png)



## 2. Screen Attributes

* Screen number 1000~1010 : 표준 SELECTION SCREEN, ABAP Dictionary Maintenance Screen 

![Screen &amp;gt; Screen attributes](../.gitbook/assets/image%20%2853%29.png)

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

![Screen &amp;gt; Layout](../.gitbook/assets/image%20%2856%29.png)



## 4. Field Attributes

* 스크린의 작업 영역 메모리에 존재하는 필드
* PAI 발생 전 시점에 ABAP Program 동일 필드명 필드로 값 전달/복
* Screen field와 Program field는 동일한 필드명으로 선언되어야 함
* 이벤트 수행시 설정 값이 OK\_CODE에 저장됨

![Screen field &amp; Program field](../.gitbook/assets/image%20%2844%29.png)



## 5. Screen Flow Logic \(Module pool\)

* 스크린이 절차적을 실행되어야 하는 부분
* ABAP 언어와 유사하지만 다른 언어임에 유의!

### Screen flow logic & ABAP 차

| 구분 | Screen flow logic | ABAP |
| :--- | :--- | :--- |
| Data 선언 | 존재 X | 존재 O |
| Processing 블럭 |  |  |

## 6. User Action



