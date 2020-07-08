---
description: SAP에서 제공하는 교육 내용과 Easy ABAP 교재 참조
---

# Table

## 1. Table 

Table은 시스템에서 생성된 데이터를 저장하는 실제 물리적인 공간으로, T-code SE11에서 테이블을 생성하여 활성화하면 데이터베이스에 물리적인 테이블이 생성된다. 2차원 행렬로 이루어져 있으며, 행렬의 열은 field 또는 column이라 불다. 필드는 테이블 내에서 중복되지 않는 이름을 가지며, MANDT 필드는 필수적으로 존재해야 한다. ABAP 테이블은 3 종류로 존재하며, 테이블 기본 속성은 DD02L 테이블, 테이블 필드에 대한 정보는 DD03L 테이블에 저장된다.

![table &#xAD6C;&#xC131; &#xC815;&#xBCF4;](../../.gitbook/assets/image%20%2833%29.png)

### Table 종류

* Transparent table
* Pooled table
* Cluster table

### Table 속성

<table>
  <thead>
    <tr>
      <th style="text-align:left">Attribution</th>
      <th style="text-align:left">Explanation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Table field</td>
      <td style="text-align:left">
        <p>&#xD544;&#xB4DC; &#xC774;&#xB984;&#xACFC; &#xD544;&#xB4DC; &#xC18D;&#xC131;&#xC744;
          &#xAC00;&#xC9D0;</p>
        <p>key &#xD544;&#xB4DC; &#xC874;&#xC7AC;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Foreign key</td>
      <td style="text-align:left">&#xD14C;&#xC774;&#xBE14; &#xAC04;&#xC758; &#xAD00;&#xACC4;&#xB97C; &#xC815;&#xC758;</td>
    </tr>
    <tr>
      <td style="text-align:left">Technical setting</td>
      <td style="text-align:left">&#xD14C;&#xC774;&#xBE14; &#xB370;&#xC774;&#xD130; &#xCD1D; &#xC120;&#xC218;,
        &#xBC84;&#xD37C;&#xB9C1; &#xC124;&#xC815; &#xB4F1;&#xC758; &#xD14C;&#xC774;&#xBE14;
        &#xC18D;&#xC131;</td>
    </tr>
    <tr>
      <td style="text-align:left">Index</td>
      <td style="text-align:left">&#xD14C;&#xC774;&#xBE14; &#xB370;&#xC774;&#xD130;&#xC758; select &#xC18D;&#xB3C4;&#xC640;
        &#xC5F0;</td>
    </tr>
  </tbody>
</table>



## 2. Table Field

### Field 속성 정의

테이블 필드는 테이블 속성을 표현하는 개별 구성요소이다. 테이블 필드에는 데이터 타입, 필드 길이, 내역을 설정한다. \(Data type, Field Length, Short Text\) 필드 속성은 Data element와 Predefined type 두 방식을 통해 지정 가능하다.

* Data element : 기존 존재하는 data element 내역 불러옴
* Predefined type : 직접 입력

### Referenced Field & Referenced Table

수량을 표현하는 데이터 타입 QUAN은 Unit of measure, 화폐량을 표현하는 데이터 타입 CURR은 Currency key 단위 참조 필드를 지정해야 한다. QUAN 또는 CURR 타입을 사용할 때, 단위를 참조하지 않으면 에러가 발생하며, 그 경우 다음을 통해 설정 가능하다. 만약 다음 WRITE 옵션 사용이 불가능한 경우네는 비용 변환 로직을 프로그램으로 구현해야 한다. 추가적으로통화 단위의 소수 자릿수 정보는 TCURX 테이블에서 확인 가능하다.  

```sql
# QUAN 변환
WRITE 기존 단 TO 변환 단위 UNIT 'KG'.

# CUARR 변환
WRITE 기존 비용 TO 변환 비용 CURRENCY 'KRW'.
```



## 3. Table 생성

{% hint style="info" %}
T-code SE11 &gt; Database table 테이블 명 입력 &gt; Create
{% endhint %}

![T-code SE11](../../.gitbook/assets/image%20%2820%29.png)

![short description, delivery class, data browser/table view editing](../../.gitbook/assets/image%20%2831%29.png)

### Delivery and Maintenance - Delivery class 설정

<table>
  <thead>
    <tr>
      <th style="text-align:left">Delivery class</th>
      <th style="text-align:left">Explanation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">A</td>
      <td style="text-align:left">
        <p>&#xC77C;&#xBC18;&#xC801;&#xC73C;&#xB85C; &#xC0AC;&#xC6A9;&#xB428;</p>
        <p>Master &#xB610;&#xB294; Transaction data</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">C</td>
      <td style="text-align:left">&#xC0AC;&#xC6A9;&#xC790;&#xAC00; &#xC720;&#xC9C0; &#xAD00;&#xB9AC;</td>
    </tr>
    <tr>
      <td style="text-align:left">L</td>
      <td style="text-align:left">&#xC784;&#xC2DC;</td>
    </tr>
    <tr>
      <td style="text-align:left">G</td>
      <td style="text-align:left">&#xAE30;&#xC874; &#xB370;&#xC774;&#xD130;&#xB294; &#xC218;&#xC815;&#xC774;
        &#xC548;&#xB418;&#xACE0; &#xCD94;&#xAC00;&#xB9CC; &#xAC00;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">E</td>
      <td style="text-align:left">SAP&#xC640; &#xACE0;&#xAC1D;&#xC774; &#xAC01;&#xC790; key &#xC601;&#xC5ED;&#xC744;
        &#xAC00;&#xC9C0;&#xB294; &#xD14C;&#xC774;&#xBE14;</td>
    </tr>
    <tr>
      <td style="text-align:left">S</td>
      <td style="text-align:left">&#xC2DC;&#xC2A4;&#xD15C; &#xD14C;&#xC774;&#xBE14;, &#xC0C1;&#xD0DC; &#xC815;&#xBCF4;</td>
    </tr>
    <tr>
      <td style="text-align:left">W</td>
      <td style="text-align:left">&#xC2DC;&#xC2A4;&#xD15C; &#xD14C;&#xC774;&#xBE14;, &#xC804;&#xC1A1;&#xC2DC;
        &#xC790;&#xC2E0;&#xC758; &#xC804;&#xC1A1; &#xAC1D;&#xCCB4;&#xB97C; &#xAC00;&#xC9C0;&#xACE0;
        &#xC804;</td>
    </tr>
  </tbody>
</table>

### Delivery and Maintenance - Data browser/Table view maintenance 설정

테이블 유지보수에 대한 권한을 설정한다.  
T-code SE16 테이블 브라우저 권한이 있는 사용자라면 테이블 엔트리를 생성 및 변경할 수 있다.   
T-code SE30 에서 데이터 유지보수가 가능하다. 

![Fields](../../.gitbook/assets/image%20%2824%29.png)

### Fields 설정

Table의 Field, Column에 대한 설정을 입력한다.

### Technical setting

저장하고 활성화 하려고 하면, Technical setting을 하라고 뜨며 상단 메뉴에서 클릭하여 설정할 수도 있다.   
Technical setting 부분은 중요한 부분이기 떄문에 따로 다루도록 하겠다.

![Technical setting](../../.gitbook/assets/image%20%2828%29.png)

![Technical setting](../../.gitbook/assets/image%20%2815%29.png)



## 4. Table 변경

## 5. Table Field 속성

## 6. Table data 생성 방



