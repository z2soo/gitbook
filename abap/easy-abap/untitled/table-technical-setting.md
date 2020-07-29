---
description: SAP에서 제공하는 교육 내용과 Easy ABAP 교재 참조
---

# Table - Technical setting

## 1. Technical setting

데이터 베이스에 테이블이 생성되기 위해서는 즉, T-code SE11에서 활성화 시키기 위해서는 기술적 속성이 정의되어야 한다. Table의 Size, Buffering, Log data 등에 대한 설정이 해당되며, ABAP Workbench 및 개별 트랜잭션 T-code SE13으로 실행 가능하다.

{% hint style="info" %}
T-code SE13 또는 ABAP Workbench
{% endhint %}

![T-code SE13](../../../.gitbook/assets/image%20%2813%29.png)

![Technical setting](../../../.gitbook/assets/image%20%2830%29.png)



## 2. Logical storage parameters

Technical setting에서 가장 중요한 부분이다.

![Technical setting &amp;gt; General properties &amp;gt; Logical storage parameters](../../../.gitbook/assets/image%20%284%29.png)

### Data class

Table이 존재하게되는 데이터 베이스의 물리적인 영역을 지정한다. Oracle에서는 Tablespace, Informix, DBspace라고 한다. 즉, Tablespace의 영역 지정 의미한다. 

![Data class type](../../../.gitbook/assets/image%20%2816%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Explanation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Master data</td>
      <td style="text-align:left">
        <p>&#xBCC0;&#xACBD;&#xC774; &#xC790;&#xC8FC; &#xC77C;&#xC5B4;&#xB098;&#xC9C0;
          &#xC54A;&#xB294; &#xB370;&#xC774;&#xD130;</p>
        <p>ex. &#xC870;&#xC9C1; &#xCF54;&#xB4DC;&#xC640; &#xAC19;&#xC740; &#xAE30;&#xC900;
          &#xC815;&#xBCF4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Transaction data</td>
      <td style="text-align:left">
        <p>&#xBCC0;&#xACBD;&#xC774; &#xC790;&#xC8FC; &#xC77C;&#xC5B4;&#xB098;&#xB294;
          &#xB370;&#xC774;&#xD130;</p>
        <p>ex. &#xC804;&#xD45C; &#xBC1C;&#xC0DD;&#xACFC; &#xAC19;&#xC774; transaction
          &#xBC1C;&#xC0DD; &#xB9C8;&#xB2E4; &#xC0DD;&#xC131;&#xB418;&#xB294; &#xB370;&#xC774;&#xD130;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Organizational data</td>
      <td style="text-align:left">
        <p>&#xC2DC;&#xC2A4;&#xD15C;&#xC774; &#xC124;&#xCE58;&#xB420; &#xB54C; &#xC124;&#xC815;&#xB418;&#xACE0;
          &#xAC70;&#xC758; &#xBCC0;&#xACBD;&#xB418;&#xC9C0; &#xC54A;&#xB294; &#xB370;&#xC774;&#xD130;</p>
        <p>ex. &#xAD6D;&#xAC00; key&#xC640; &#xAC19;&#xC740; &#xD14C;&#xC774;&#xBE14;
          &#xC815;&#xBCF4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">System data</td>
      <td style="text-align:left">
        <p>&#xC2DC;&#xC2A4;&#xD15C; &#xC790;&#xCCB4;&#xAC00; &#xC694;&#xAD6C;&#xD558;&#xB294;
          &#xB370;&#xC774;&#xD130;</p>
        <p>ex. &#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC18C;&#xC2A4;&#xB97C; &#xB2F4;&#xB294;
          &#xD14C;&#xC774;&#xBE14; &#xC815;&#xBCF4;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Customer data</td>
      <td style="text-align:left">&#xACE0;&#xAC1D;&#xC0AC;&#xC5D0;&#xC11C; &#xD544;&#xC694;&#xD55C; &#xACBD;&#xC6B0;
        &#xCD94;&#xAC00;&#xB85C; &#xC0DD;&#xC131;&#xD558;&#xB294; &#xB370;&#xC774;</td>
    </tr>
  </tbody>
</table>

### Size category

![Data size category](../../../.gitbook/assets/image%20%288%29.png)

Table에 생성될 수 있는 레코드 수를 정의하며, 고객마다 다르게 설정 가능하다.



## 3. Buffering

Buffer 설정을 하면 DB에서 직접 데이터를 조회하는 것이 아닌, Application server 영역의 Buffer에서 조회한다. Buffer 설정은 특히 Client/Server 모델에서 효과를 가지며 Access 시간을 효과적으로 절감할 수 있다.

하지만, Buffer에 원하는 데이터가 존재하지 않으면 DB Access &gt; Buffer에 데이터 저장 &gt; Buffer 데이터 조회 과정을 거치기 떄문에 DB에 직접 Access하는 것보다 시간이 더 걸리게 된다. 따라서 Buffer 설정은 Master data 성격의 Table에만 하고, Transaction이 자주 발생하는 테이블은 Buffer를 설정하지 않는다.

![&#xCD9C;&#xCC98; Easy ABAP](../../../.gitbook/assets/image%20%283%29.png)

### Buffering Option

![](../../../.gitbook/assets/image%20%281%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">For</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Buffering not permitted</td>
      <td style="text-align:left">
        <p>Transaction&#xC774; &#xC790;&#xC8FC; &#xBC1C;&#xC0DD;&#xD558;&#xB294;
          Table</p>
        <p>Application server&#xC640; DBserver &#xB3D9;&#xAE30;&#xD654;&#xB97C; &#xAE30;&#xB2E4;&#xB9B4;
          &#xC218; &#xC5C6;&#xB294; Table</p>
        <p>&#xCD5C;&#xC2E0; &#xB370;&#xC774;&#xD130;&#xAC00; &#xD544;&#xC694;&#xD55C;
          Table</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Buffering allowed but switched off</td>
      <td style="text-align:left">
        <p>Buffering &#xC120;&#xD0DD; &#xAC00;&#xB2A5;</p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Buffering activated</td>
      <td style="text-align:left">&#xB370;&#xC774;&#xD130; &#xBCC0;&#xACBD;&#xC774; &#xC7A6;&#xC9C0; &#xC54A;&#xACE0;
        Read &#xC811;&#xADFC;&#xC774; &#xB9CE;&#xC740; Table</td>
    </tr>
  </tbody>
</table>

### Buffering Type

![](../../../.gitbook/assets/image%20%2812%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Explanation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Single record</td>
      <td style="text-align:left">
        <p>Table record&#xC5D0; &#xC811;&#xADFC;&#xD55C; &#xC815;&#xBCF4;&#xB9CC;
          Buffer&#xC5D0; &#xC800;&#xC7A5;</p>
        <p>Buffer storage &#xACF5;&#xAC04; &#xC801;&#xAC8C; &#xD544;&#xC694;&#xD558;&#xB2E4;&#xB294;
          &#xC7A5;&#xC810;</p>
        <p>DB &#xC811;&#xADFC; &#xD69F;&#xC218;&#xAC00; &#xC99D;&#xAC00;&#xD55C;&#xB2E4;&#xB294;
          &#xB2E8;&#xC810;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Generic area buffered</td>
      <td style="text-align:left">
        <p>&#xC120;&#xD0DD; key &#xAC12;&#xC5D0; &#xD574;&#xB2F9;&#xD558;&#xB294;
          Table &#xBAA8;&#xB4E0; Entry&#xB97C; Buffer&#xC5D0; &#xC800;&#xC7A5;</p>
        <p>Generic key&#xB294; Primary key &#xC77C;&#xBD80;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Fully buffered</td>
      <td style="text-align:left">
        <p>&#xBAA8;&#xB4E0; Table row&#xAC00; Buffer&#xC5D0; &#xC800;&#xC7A5;</p>
        <p>&#xB370;&#xC774;&#xD130;&#xAC00; &#xC801;&#xACE0; &#xC790;&#xC8FC; &#xC77D;&#xD788;&#xBA70;
          &#xB370;&#xC774;&#xD130;&#xAC00; &#xCD94;&#xAC00;&#xB418;&#xB294; &#xD69F;&#xC218;&#xAC00;
          &#xC801;&#xC740; &#xD14C;&#xC774;&#xBE14;&#xC5D0; &#xC0AC;</p>
      </td>
    </tr>
  </tbody>
</table>

### Buffering Synchronize

대부분의 SAP 운영 환경은 여러 대의 Application server가 동작하고 있으며, 각 Application은 각자의 SAP Table Buffer, Local Buffer를 가진다. 즉, 우리가 운영 서버로 로그인 할 때마다 같은 서버가 아닌 여러 서버 중 하나로 접속하게 된다. 

Synchronized Table은 Local Buffer에서 데이터 변경이 발생하면 해당 정보를 저장하는 테이블이다. 매 1~2분 마다 Server의 Local Buffer는 Synchronization Table의 데이터를 참조하여 동기화를 수행한다. 만약 동기화 이전에 데이터가 변경되면 Server 간 다른 데이터가 존재하는 문제가 발생한다. 따라서 Transaction이 자주 발생하는 Table에 Buffer를 설정하면 데이터 왜곡이 발생할 수 있음을 유의해야 한다. 

버퍼링이 설정된 Table에서 Local Buffer를 사용하지 않고 DB Table에서 데이터를 읽어오려면 다음 옵션을 사용한다.

```sql
# BYPASSING BUFFER
SELECT * FROM 테이블명 INTO 스트럭쳐명 BYPASSING BUFFER
         WHERE 조건.
```

