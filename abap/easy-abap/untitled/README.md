---
description: ABAP dictionary Overview
---

# 07. ABAP Dictionary

## ABAP Dictionary?

* T-code: SE11
* ABAP Program 에서 사용되는 object 지칭
* 중앙집중식으로 object 관리
* 3 Type 

ABAP dictionary는 ABAP 프로그램에서 사용되는 object를 지칭함과 동시에 이를 중앙집중식으로 관리한다. 중앙집중식 관리를 통해 무결성, 일관성, 안정성을 유지할 수 있으며, ABAP dictionary는 동적으로 ABAP Workbench와 연관되어 있기 때문에 오브젝트 변경 및 신규 생성은 ABAP Program, Screen 등 모든 사용처에 영향을 미친다. 이러한 ABAP dictionary는 3 종류로 분류된다.

## ABAP Dictionary Type

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">object</th>
      <th style="text-align:left">Explanation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Database object</td>
      <td style="text-align:left">Table</td>
      <td style="text-align:left">&#xC2DC;&#xC2A4;&#xD15C;&#xC5D0;&#xC11C; &#xC0DD;&#xC131;&#xB41C; &#xB370;&#xC774;&#xD130;&#xB97C;
        &#xC800;&#xC7A5;&#xD558;&#xB294; &#xC2E4;&#xC81C; &#xBB3C;&#xB9AC;&#xC801;&#xC778;
        &#xACF5;&#xAC04;</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">View</td>
      <td style="text-align:left">
        <p>&#xD558;&#xB098; &#xC774;&#xC0C1;&#xC758; table&#xC774; &#xB17C;&#xB9AC;&#xC801;&#xC73C;&#xB85C;
          &#xACB0;&#xD568;&#xD55C; &#xAD6C;&#xC870;</p>
        <p>&#xC2E4;&#xC81C; &#xB370;&#xC774;&#xD130;&#xB97C; &#xAC00;&#xC9C0;&#xB294;
          &#xAC83;&#xC774; &#xC544;&#xB2CC; &#xC870;&#xAC74;&#xC5D0; &#xB9DE;&#xCDB0;
          &#xC5EC;&#xB7EC; table &#xC870;&#xD569;&#xD558;&#xC5EC; &#xC870;&#xD68C;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Type definition</p>
        <p>(Data type)</p>
      </td>
      <td style="text-align:left">Data element</td>
      <td style="text-align:left">
        <p>Elementary type, Referenced type &#xD544;&#xB4DC;&#xC758; &#xAE30;&#xC220;&#xC801;
          &#xC18D;&#xC131;&#xC744; &#xC815;&#xC758;</p>
        <p>ABAP &#xD504;&#xB85C;&#xADF8;&#xB7A8;&#xC5D0;&#xC11C; &#xCC38;&#xACE0;&#xD558;&#xC5EC;
          &#xBCC0;&#xC218; &#xC120;&#xC5B8; &#xBD88;&#xAC00;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Structure</td>
      <td style="text-align:left">
        <p>Type&#xC744; &#xAC00;&#xC9C0;&#xB294; component&#xB85C; &#xAD6C;&#xC131;</p>
        <p>Domain, Data element,</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Table type</td>
      <td style="text-align:left">Internal table&#xC758; &#xAE30;&#xB2A5;&#xC801; &#xC18D;&#xC131;&#xC744;
        &#xC815;&#xC758;</td>
    </tr>
    <tr>
      <td style="text-align:left">Tool</td>
      <td style="text-align:left">Search help</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">Lock object</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

## View - Table - Data element - Domain 관계



![](../../../.gitbook/assets/image-20200623104243285%20%281%29.png)

### Domain

* 필드의 기술적인 속성을 정의
* Data element에 할당되어 사용
* ABAP 프로그램 내에서 Domain을 참조하여 변수 선언 불가

### Data element

* 테이블 필드의 정보를 가진 ABAP dictionary object
* 테이블 필드의 속성으로 사용 가능
* ABAP 프로그램 내에서 참조하 변수 선언 가능

### Table

* 시스템에서 생성된 데이터를 저장하는 실제 물리적인 공간

### View

* 하나 이상의 table이 논리적으로 결합한 구조로 실제 데이터를 가지지는 않음
* table의 데이터를 조건에 맞게 조합하여 조회하는 기능으로 주로 사용 

