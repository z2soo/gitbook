---
description: Relational database management system overall.
---

# RDBMS

## 1. 정의

Relational Database Management System 즉, 관계형 데이터 베이스 관리 시스템은 데이터 베이스의 한 종류로 가장 많이 사용된다. 이는 데이터 베이스에 데이터를 열\(Column\)과 행\(Row\)의 테이블 형태로 저장하고, 테이블 형태의 스키마를 지켜야 한다. 가장 대표적인 RDBMS는 Oracle사의 Oracle, Microsoft사의 MS-SQL Server, Oracle사의 MySQL, IBM의 DB2 등이 있다. 관계형 데이터 베이스를 다루기 위한 언어를 SQL 이라고 한다. 



## 2. 장점 및 단점

### 장점 

* 양한 용도로 사용이 가능 \(범용적\)
* 데이터의 분류, 정렬, 탐색 속도가 빠음 \(고성능\)
* 데이터의 일관성을 보증함
* 정규화에 따른 갱신 비용 최소화

### 단점 

* 반드시 스키마 규격에 맞춰야 함 즉, 갱신 발생 테이블은 인덱스 생성과 스키마 변경이 요구됨
* 작업 부하의 분산이 어려움
* 객체와 관계의 mapping layer 복잡 가능성
* 조인이 필요한 경우 확장성이 제약됨
* 테이블에 가변성이 있는 데이터 저장이 어려움

![https://codingcoding.tistory.com/200](../../.gitbook/assets/image%20%2876%29.png)



## 3. 용어 정리

### Schema\(스키마\)

* 데이터 베이스의 테이블 구조 및 형식, 관계 등의 정보를 형식 언어\(formal language\)로 기술한 것
* collection of metadata

관계형 데이터 베이스\(RDB\)를 사용하여 데이터를 저장할 때, 데이터의 공통 속성을 식별하여 열\(Col\)으로 정의하고 테이블을 생성하는 것이 가장 먼저 해야하는 과정이다. 이 때, 하나의 테이블이 아닌 여러 테이블을 만들고 각 테이블의 구조, 형식, 관계를 정의하는데 이를 스키마라고 한다. 즉, 데이터 베이스의 설계도로 이해하면 된다. 데이터 베이스마다 스키마를 만드는 언어가 각기 존재하며, 해당 스키마만 있으면 동일한 구조의 데이터 베이스를 만들 수 있다. \(데이터 백업은 아닌, 구조만 동일하다는 의미\)

![https://www.lifewire.com/definition-of-a-schema-in-a-database-1019262](../../.gitbook/assets/image%20%2873%29.png)



### Structured Query Language \(SQL\)

SQL은 데이터 베이스 스키마 생성 및 수정, 테이블 관리, 데이터 추가, 수정, 삭제, 조회 등 데이터 베이스와 관련된 거의 모든 작업을 위해 사용되는 언어다. 데이터 베이스마다 문법의 차이는 존재하지만, 표준 SQL을 기본으로 하기 때문에 SQL은 필수적으로 익히도록 한다. SQL 언어는 크게 세 가지 언어로 나뉘며 다음과 같이 구분된다. 

* RDBMS에서 관리하기 위해 사용되는 표준 프로그래밍 언어
* 세 종류로 나뉨
  * DDL \(Data Definition Language\) : 데이터 정의 언어
  * DML \(Data Manipulation Language\) : 데이터 조작 언어
  * DCL \(Data Contrl Language\) : 데이터 제어 언어

| 종류 | 설명 |
| :--- | :--- |
| DDL 데이터 정의 언어 | - 데이터 구조 정의 - 테이블\(table\), 인덱스\(index\) 등의 개체를 만들고 관리하는데 사용되는 명령어 - CREATE, ALTER, DROP |
| DML 데이터 조작 언어 | - 데이터 CRUD 수행 - Create, Read, Update, Delete 작업을 수행하기 위해 사용되는 명령어 - INSERT, UPDATE, DELETE, SELECT  |
| DCL 데이터 제어 언어 | - GRANT 데이터 베이스 개체 \(테이블, 인덱스 등\)에 대한 사용 권한 설정 - BEGIN, COMMIT, ROLLBACK |



### RDBMS 구성

관계형 데이터 베이스를 구성하는 데이터들은 다음의 요소로 이루어져 있다. 

다음의 경우, 학생 relation은 학번, 이름, 학과, 학년의 attribute로 이루어져 있으며, 학생 relation에서 학년 attribute가 가질 수 있는 값 즉, domain의 값은 1, 2, 3, 4 이며 이외의 값은 가질 수 없다고 해석된다. 

![](../../.gitbook/assets/image%20%2870%29.png)

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xC694;&#xC18C;</th>
      <th style="text-align:left">&#xC124;&#xBA85;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Relation</p>
        <p>(&#xD14C;&#xC774;&#xBE14;)</p>
      </td>
      <td style="text-align:left">&#xAC19;&#xC740; &#xC131;&#xACA9;&#xC758; &#xB370;&#xC774;&#xD130;&#xC758;
        &#xC9D1;&#xD569;&#xC73C;&#xB85C; Relation Schema &#xC640; Relation Instance
        &#xB85C; &#xAD6C;&#xC131;&#xB428;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Relation Schema</p>
        <p>(&#xC2A4;&#xD0A4;&#xB9C8;)</p>
      </td>
      <td style="text-align:left">Relation&#xC758; &#xC774;&#xB984;&#xACFC; &#xAC01; Attribute&#xC758; &#xC774;&#xB984;&#xC758;
        &#xC9D1;&#xD569;, Relation&#xC744; &#xB123;&#xAE30; &#xC704;&#xD55C; &#xD2C0;</td>
    </tr>
    <tr>
      <td style="text-align:left">Relation Instance</td>
      <td style="text-align:left">&#xC5B4;&#xB290; &#xC2DC;&#xC810;&#xC758; Relation&#xC5D0; &#xB4E4;&#xC5B4;&#xC788;&#xB294;
        Tuple&#xC758; &#xC9D1;&#xD569;, &#xC800;&#xC7A5;&#xB41C; &#xB370;&#xC774;&#xD130;
        &#xC804;&#xCCB4;&#xB97C; &#xC758;&#xBBF8;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Attribute</p>
        <p>(&#xC18D;&#xC131;)</p>
      </td>
      <td style="text-align:left">- Relation&#xC758; col (&#xC5F4;)
        <br />- Entity&#xC758; &#xC18D;&#xC131;</td>
    </tr>
    <tr>
      <td style="text-align:left">Entity Instance</td>
      <td style="text-align:left">&#xB2E8;&#xC218;&#xD615;&#xC758; &#xB370;&#xC774;&#xD130;</td>
    </tr>
    <tr>
      <td style="text-align:left">Entity, Tuple, Record</td>
      <td style="text-align:left">- Relation&#xC758; row (&#xD589;)
        <br />- Entity Instance&#xC758; &#xBCF5;&#xC218;&#xD615;</td>
    </tr>
    <tr>
      <td style="text-align:left">Domain</td>
      <td style="text-align:left">&#xD558;&#xB098;&#xC758; Attribute&#xAC00; &#xAC00;&#xC9C8; &#xC218; &#xC788;&#xB294;
        &#xAC12;&#xC758; &#xBC94;&#xC704;</td>
    </tr>
  </tbody>
</table>



### 기타

* Transaction : 분리되어 수행될 수 없는 논리적인 하나의 작업단위

