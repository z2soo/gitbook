---
description: ABAP List Viewer Overview
---

# 수정중\_15. Grid ALV

## 1. ALV

* ABAP List Viewer
* List 화면에 데이터 조회
* 조회된 데이터 수정, 변경 목적으로 사용 

Report program에서 조회된 데이터를 엑셀로 내려받는 기능을 추가하려면 STATUS를 생성하여 버튼을 화면에 추가하고, 사용자가 버튼을 클릭하면 반응하는 이벤트를 기술해야 했다. 

그러나 ALV는 이러한 기본적인 사무용 작업툴을 이미 포함된 패키지 프로그램으로 제공하기 때문에 이를 활용하면 스크립트를 구현하지 않고 ALV에서 제공되는 다음과 같은 작업툴의 기능을 활용할 수 있다. 

* 정렬기능
* 기본적인 계산 수행 기능
* 열의 크기 변경
* 레이아웃 변경
* 더블클릭 이벤트에 의한 추가정보 제공
* 엑셀 파일 및 워드파일 저장



## 2. ALV 화면 표시 방법

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xBC29;&#xBC95;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">ALV Grid</td>
      <td style="text-align:left">
        <p>Class &#xD65C;&#xC6A9;
          <br />CL_ &#xB85C; &#xC2DC;&#xC791;&#xD558;&#xB294; &#xD568;&#xC218;&#xBA85;</p>
        <p>&#xB370;&#xC774;&#xD130; &#xB0B4;&#xC6A9;&#xC744; &#xC0C1;&#xC138;&#xD558;&#xAC8C;
          &#xD45C;&#xD604; &#xAC00;&#xB2A5;</p>
        <p>&#xCF54;&#xB529;&#xB7C9;&#xC774; &#xB9E4;&#xC6B0; &#xB9CE;&#xC74C;
          <br
          />CL&#xB85C; &#xC2DC;&#xC791;&#xB418;&#xB294; &#xD568;&#xC218;&#xBA85;</p>
      </td>
      <td style="text-align:left">
        <ul>
          <li>CL_SALV_TABLE
            <br />CL_GUI_ALV_GRID&#xC758; &#xBCF5;&#xC7A1;&#xC131;&#xC744; &#xB2E8;&#xC21C;&#xD654;
            <br
            />EDIT &#xBD88;&#xAC00;</li>
          <li>CL_SALV_HIERSEQ_TABLE
            <br />&#xACC4;&#xCE35;&#xC801; &#xD45C;&#xD604;&#xBC29;&#xBC95;</li>
          <li>CL_SALV_TREE
            <br />Tree&#xD615;&#xD0DC;&#xB85C; &#xD45C;&#xD604;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Functions ALV</td>
      <td style="text-align:left">
        <p>REUSE_ALV &#xB85C; &#xC2DC;&#xC791;&#xD558;&#xB294; &#xD568;&#xC218;&#xB4E4;&#xC784;</p>
        <p>Screen &#xC0DD;&#xC131;&#xC5C6;&#xC774; &#xAC04;&#xB2E8; &#xC124;&#xC815;&#xC73C;&#xB85C;
          &#xD45C;&#xD604; &#xAC00;&#xB2A5;</p>
        <p>&#xB2E8;&#xC21C;&#xD654;&#xB418;&#xC5B4; Detail &#xD45C;&#xD604; &#xBD88;&#xAC00;&#xB2A5;</p>
      </td>
      <td style="text-align:left">
        <ul>
          <li>REUSE_ALV_GRID_DISPLAY
            <br />ALV LOAD&#xD574;&#xC11C; itab&#xC744; GRID&#xD615;&#xD0DC;&#xB85C; &#xBCF4;&#xC784;</li>
          <li>
            <p>REUSE_ALV_LIST_DISPLAY</p>
            <p>ALV LOAD&#xD574;&#xC11C; itab&#xC744; List&#xD615;&#xD0DC;&#xB85C; &#xBCF4;&#xC784;</p>
          </li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SALV</td>
      <td style="text-align:left">New ALV</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>



## 3. ALV GRID 컨트롤 인스턴스 

{% hint style="warning" %}
* 인스턴스화 : 클래스로부터 객체를 만드는 과정
* 인스턴스 : 어떤 클래스로부터 만들어진 객체
{% endhint %}

 ???????????????????

### ALV 사전 필요 작업

1. 프로그램 생성
2. 인터널 테이블 선언 - 화면에 표시될 인터널 테이블 선언 - 아웃풋 테이블 : ALV에서 데이터 정보를 저장하는 인터널 테이블 영역
3. 데이터의 구조 \(Field Catalog\) - ALV GRID  Control이 스크린에 조회되는 구조 정의 - ALV GRID Control에서 정의되는 데이터의 구조, 기술속성, 내역과 같은 정보 함유 - 일반적으로 ABAP Dictionary의 테이블, 구조체 이용 or 인터널 테이블의 구조 그대로 사 

![](../../.gitbook/assets/image%20%2872%29.png)











