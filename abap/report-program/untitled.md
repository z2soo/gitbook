---
description: SAP에서 제공하는 교육 내용과 Easy ABAP 교재 참조
---

# Program 생성

## 1. Program 생성 

{% hint style="info" %}
T-code SE80 &gt; Create &gt; Program &gt; TOP INCL 설정 
{% endhint %}



## 2. Program Attributes

![&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC18D;&#xC131;](../../.gitbook/assets/image%20%2863%29.png)

### Type

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Describe</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">(1) Executable program</td>
      <td style="text-align:left">
        <p>T-code &#xC5C6;&#xC774; SE38&#xC5D0;&#xC11C; &#xC9C1;&#xC811; &#xC2E4;&#xD589;
          &#xAC00;&#xB2A5;</p>
        <p>SELECTION-SCREEN &amp; Output List&#xB85C; &#xAD6C;&#xC131;</p>
        <p>Local DB &#xC0AC;&#xC6A9; &#xAC00;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">(M) Module pool</td>
      <td style="text-align:left">
        <p>Screen painter screen</p>
        <p>Screen module processing</p>
        <p>T-code &#xB610;&#xB294; Menu function&#xC73C;&#xB85C; &#xC2E4;&#xD589;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">(I) Include</td>
      <td style="text-align:left">Program&#xC5D0;&#xC11C; Include&#xB85C; &#xD638;&#xCD9C;&#xB418;&#xB294;
        &#xB0B4;&#xC7A5;&#xD615; &#xD504;&#xB85C;&#xADF8;&#xB7A8;</td>
    </tr>
    <tr>
      <td style="text-align:left">(S) Subroutine</td>
      <td style="text-align:left">External PERFORM &#xAD6C;&#xBB38;&#xC5D0;&#xC11C; &#xC0AC;&#xC6A9; &#xAC00;&#xB2A5;&#xD55C;
        FORM</td>
    </tr>
    <tr>
      <td style="text-align:left">Etc</td>
      <td style="text-align:left">
        <p>F~K &#xC720;&#xD615;&#xC740; Program attribute&#xC5D0;&#xC11C; &#xBCC0;&#xACBD;
          &#xBD88;&#xAC00;</p>
        <p>Builder&#xC5D0;&#xC11C; &#xAD00;</p>
      </td>
    </tr>
  </tbody>
</table>

### Status

프로그램에 따라 특정 기능 수행이 불가해진다.

### Authorization Group

프로그램 수정 및 실행과 관련된 권한 그룹 할당으로 보완과 연관된다.

### Logical database 

Type-1 경우에만 선택한다. LDB를 사용하여 프로그램을 구현할 수 있다.   
사용 빈도가 높은 테이블의 데이터 조회를 위해 JOIN이 자주 사용되고, 조회 조건이 유사한 경우 하나의 package로 생성하여 재사용할 수 있게 해주는 기능이다. 

