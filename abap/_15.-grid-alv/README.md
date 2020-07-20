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



## 2. ALV 종류 

AVL의 종류, 즉 화면을 표현하는 방법으로는 두 가지가 존재한다.   
이번 chapter는 ALV Grid를 활용한 화면 표현 방법을 다룰 것이며, 다음 chapter는 Function에 대해 다룬다. 

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xBC29;&#xBC95;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
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
    </tr>
    <tr>
      <td style="text-align:left">Functions ALV</td>
      <td style="text-align:left">
        <p>REUSE_ALV &#xB85C; &#xC2DC;&#xC791;&#xD558;&#xB294; &#xD568;&#xC218;&#xB4E4;&#xC784;</p>
        <p>Screen &#xC0DD;&#xC131;&#xC5C6;&#xC774; &#xAC04;&#xB2E8; &#xC124;&#xC815;&#xC73C;&#xB85C;
          &#xD45C;&#xD604; &#xAC00;&#xB2A5;</p>
        <p>&#xB2E8;&#xC21C;&#xD654;&#xB418;&#xC5B4; Detail &#xD45C;&#xD604; &#xBD88;&#xAC00;&#xB2A5;</p>
      </td>
    </tr>
  </tbody>
</table>



## 3. ALV GRID 컨트롤 인스턴스 

 

```text
* CL_GUI_ALV_GRID 참조하는 GV_GRID 객체 참조 변수 
DATA: GV_GRID TYPE REF TO CL_GUI_ALV_GRID.

```



### ALV 사전 필요 작업

1. 프로그램 생성
2. 인터널 테이블 선언 - 화면에 표시될 인터널 테이블 선언 - 아웃풋 테이블 : ALV에서 데이터 정보를 저장하는 인터널 테이블 영역
3. 데이터의 구조 \(Field Catalog\) - ALV GRID  Control이 스크린에 조회되는 구조 정의 - ALV GRID Control에서 정의되는 데이터의 구조, 기술속성, 내역과 같은 정보 함유 - 일반적으로 ABAP Dictionary의 테이블, 구조체 이용 or 인터널 테이블의 구조 그대로 사 

![](../../.gitbook/assets/image%20%2872%29.png)











