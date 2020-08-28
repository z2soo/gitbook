# HANA Database 생성

## 1. HANA Database 생성 

{% hint style="info" %}
SCP Cockpit &gt; SAP HANA/SAP ASE &gt; 데이터베이스 핫 스키마 &gt; 신규 
{% endhint %}

SCP Cockpit 카테고리 중  SAP HANA/SAP ASE &gt; 데이터베이스 핫 스키마  들어가서 신규를 눌러 새로운 database를 생성해준다. 현재 demo 계정이기 때문에 데이터베이스는 24시간만 유지된다. 

![SCP Cockpit &amp;gt; SAP HANA/SAP ASE &amp;gt; &#xB370;&#xC774;&#xD130;&#xBCA0;&#xC774;&#xC2A4; &#xD56B; &#xC2A4;&#xD0A4;&#xB9C8;](.gitbook/assets/image%20%28630%29.png)

신규 데이터베이스 및 스키마는 다음 정보로 생성한다. 이때, 비밀번호를 많이 틀리면 잠겨버리고, 까먹으면 찾을 수 없기 떄문에 유의한다. 

{% hint style="warning" %}
데이터베이스 ID : CP10024  
비밀번호 :  Group24cloudplatform
{% endhint %}

![ &#xB370;&#xC774;&#xD130;&#xBCA0;&#xC774;&#xC2A4; &#xD56B; &#xC2A4;&#xD0A4;&#xB9C8; &amp;gt; &#xC2E0;&#xADDC; ](.gitbook/assets/image%20%28623%29.png)

데이터 베이스 생성이 완료되면 다음 같은 화면이 뜬다. 

![SCP Cockpit &amp;gt; SAP HANA/SAP ASE &amp;gt; &#xB370;&#xC774;&#xD130;&#xBCA0;&#xC774;&#xC2A4; &#xD56B; &#xC2A4;&#xD0A4;&#xB9C8;](.gitbook/assets/image%20%28575%29.png)

생성한 데이터 베이스로 들어가서 확인한다. 

![&#xC0DD;&#xC131; &#xC644;&#xB8CC;&#xB41C; &#xB370;&#xC774;&#xD130; &#xBCA0;&#xC774;&#xC2A4; ](.gitbook/assets/image%20%28619%29.png)



## 2. Database 권한 설정

{% hint style="info" %}
초기 system 계정으로 로그인 후, Admin 권한을 받아야 DB 접근이 가능해진다.  
또한 유저 생성 및 권한 설정을 해야 DB 접근 및 작업이 가능해진다.
{% endhint %}



### 1\) system 계정 로그인 

데이터 베이스에 접근하기 위해서는 권한이 부여되어야 한다. 데이터 베이스 세부사항 중 우선 관 툴 부분을 눌러 들어간다. 

![&#xC0DD;&#xC131; &#xC644;&#xB8CC;&#xB41C; &#xB370;&#xC774;&#xD130; &#xBCA0;&#xC774;&#xC2A4; ](.gitbook/assets/image%20%28619%29.png)

![&#xAD00;&#xB9AC;&#xD234;:  SAP HANA &#xCF55;&#xD53C;&#xD2B8; &#xD074;&#xB9AD;](.gitbook/assets/image%20%28591%29.png)

초기 자동 생성되는 시스템 관리 계정인 system으로 로그인해서 Admin 권한을 부여받은 후, 유저를 생성하거나 권한을 부여해야 데이터 베이스에 정상적으로 접근 및 권한에 따른 작업이 가능해진다. 따라서, 로그인 화면이 나오면 system과 위에서 설정한 비밀번호를 입력해서 로그인한다.    

![SAP HANA &#xCF55;&#xD53C;&#xD2B8; &amp;gt; Login](.gitbook/assets/image%20%28603%29.png)

 system으로 로그인 완료하면 다음 information 창과 SAP HANA Databse Administraion 화면이 나온다. 

![system &#xCD08;&#xAE30; &#xB85C;&#xADF8;&#xC778; &#xC644;&#xB8CC;](.gitbook/assets/image%20%28589%29.png)

![SAP HANA Databse Administraion](.gitbook/assets/image%20%28568%29.png)



### 2\) User 권한 설정 - DEV/ADMIN

Cockpit 사이트로 돌아와서 개툴 SAP HANA 콕웹 기반 개발 워크벤치로 들어간다. 

![SCP Cockpit &amp;gt; SAP HANA/SAP ASE ](.gitbook/assets/image%20%28628%29.png)

![SCP Cockpit &amp;gt; SAP HANA/SAP ASE &amp;gt; SAP HANA &#xC6F9; &#xAE30;&#xBC18; &#xAC1C;&#xBC1C; &#xC6CC;&#xD06C;&#xBCA4;&#xCE58;](.gitbook/assets/image%20%28591%29.png)

다음 화면 중 Security로 들어가서 권한 및 유저 설정을 해준다.   
현재 권한 설정이 안되있기 때문에, 다른 부분으로 들어가도 페이지 오류가 뜬다.

![SAP HANA &#xC6F9; &#xAE30;&#xBC18; &#xAC1C;&#xBC1C; &#xC6CC;&#xD06C;&#xBCA4;&#xCE58;](.gitbook/assets/image%20%28618%29.png)

![SAP HANA &#xC6F9; &#xAE30;&#xBC18; &#xAC1C;&#xBC1C; &#xC6CC;&#xD06C;&#xBCA4;&#xCE58; &amp;gt; Security](.gitbook/assets/image%20%28560%29.png)

이제 User에 대해 작업을 위한 권한을 부여한다. 이를 위해 우선 system 유저에 대해 Developer 및 Admin 권한을 부여해주고, 권한이 부여된 system user를 복사해서 개발을 위한 새로운 user를 생성해줄 것이다.



#### Developer Role 추가

왼쪽 카테고리 중 User &gt; SYSTEM 클릭하면 Original Roles 부분에 Role 권한을 추가할 수 있는 버튼이 있다.   
이를 눌러 developer를 검색하고 나오는 role을 모두 선택해서 더해준다. 

![](.gitbook/assets/image%20%28551%29.png)



![](.gitbook/assets/image%20%28595%29.png)



![](.gitbook/assets/image%20%28540%29.png)

저장하고 성공하면 하단에 success 뜸

마찬가지로 admin도 모두 추가 

![](.gitbook/assets/image%20%28573%29.png)

저장 후 다시 돌아가서 editor 누르면 이제는 오류 안날 것

![](.gitbook/assets/image%20%28616%29.png)

![](.gitbook/assets/image%20%28593%29.png)



### 3\) 신규 User 생성  

![](.gitbook/assets/image%20%28565%29.png)

![](.gitbook/assets/image%20%28548%29.png)

![](.gitbook/assets/image%20%28609%29.png)

해당 비밀번호는 초기기 떄문에 로그인하ㅓ면 다시 재설정하라고 뜰 

![](.gitbook/assets/image%20%28578%29.png)



로그아웃해서 위에서 만든 것으로 로그인

![](.gitbook/assets/image%20%28602%29.png)

![](.gitbook/assets/image%20%28545%29.png)



새로운 비밀번호는 Group24cloudplatformdev으로 설정했음

{% hint style="warning" %}
DEV24 계정 비밀번호 : Group24cloudplatformdev
{% endhint %}



## 3. Schema 생성 

새로 생성한 DEV24 계정에서 앞으로 작업을 진행한다. 항상현재 작업 중인 user가 어느 계정인지 유의한다.  


![](.gitbook/assets/image%20%28621%29.png)

![](.gitbook/assets/image%20%28552%29.png)

![](.gitbook/assets/image%20%28546%29.png)

![](.gitbook/assets/image%20%28547%29.png)

![](.gitbook/assets/image%20%28611%29.png)

```text
create column table book(
bookId Int not NULL
,bookName varchar(100) not NULL
,isbn varchar(20) not NULL
,price int not NULL
,priceCurrency varchar(10) not NULL
,authorName varchar(100) not NULL
,primary key (bookID));
```

![](.gitbook/assets/image%20%28555%29.png)

![](.gitbook/assets/image%20%28598%29.png)

![](.gitbook/assets/image%20%28576%29.png)

Table 하위에 Book table이 생성되고, 빨간 오류가 뜨지 않으면 정상 작동되었다.



open definition



![](.gitbook/assets/image%20%28557%29.png)

open content

![](.gitbook/assets/image%20%28601%29.png)

```text
insert into store.book values ('110',' The Great Gatsby','743273567','11',' USD','Scott Fitzgerald');
insert into store.book values ('111',' Tender Is the Night','1853260975','9',' USD','Scott Fitzgerald');
insert into store.book values ('112',' This Side of Paradise','486289990','5',' USD','Scott Fitzgerald');
insert into store.book values ('120','1984','451524934','7',' USD','George Orwell');
insert into store.book values ('121',' Animal Farm',' 812911612X','14',' USD','George Orwell');
insert into store.book values ('130',' The Catcher in the Rye','316769487','5',' USD','Salinger');
insert into store.book values ('140',' Slaughterhouse-Five','385333846','10',' USD','Kurt Vonnegut');
insert into store.book values ('141',' Cats Cradle',' 038533348X','10',' USD','Kurt Vonnegut');
insert into store.book values ('142',' Breakfast of Champions','385334206','10',' USD','Kurt Vonnegut');
insert into store.book values ('143',' The Sirens of Titan','385333498','9',' USD','Kurt Vonnegut');
```

![](.gitbook/assets/image%20%28586%29.png)

![](.gitbook/assets/image%20%28617%29.png)





### Custom table 생성 

customer table도 생성

```text
create column table customer( custId Int not NULL
,custName varchar(100) not NULL ,gender varchar(100) not NULL ,age int not NULL
,primary key (custID));
```

![](.gitbook/assets/image%20%28549%29.png)

값 추

```text
insert into store.customer values ('101','Hong Gil Dong','M','24');
insert into store.customer values ('102','Choi Ji Woo','F','24');
```

![](.gitbook/assets/image%20%28542%29.png)

![](.gitbook/assets/image%20%28550%29.png)





## 4. Odata service로 만들기 

피오리 앱에서 Odata에 접근해서 가공하는 것처럼 위에서 생성한 테이블을 Odata service로 만든다. 



패키지 프로젝트를 구성할 것 

### 1\) package 생성 

![](.gitbook/assets/image%20%28553%29.png)

content &gt; 우클릭 &gt; new &gt; package

package name: mypackage  
description: ,ypackage ODATA Test  
Responsible: mypackagte  
original language: en

![](.gitbook/assets/image%20%28600%29.png)

![](.gitbook/assets/image%20%28543%29.png)



![](.gitbook/assets/image%20%28608%29.png)

![](.gitbook/assets/image%20%28567%29.png)

![](.gitbook/assets/image%20%28610%29.png)

![](.gitbook/assets/image%20%28579%29.png)



### 2\) 기능별  File 생성

Odata service를 위한 기능 파일을 두개 생성한다. 

#### 

###  

![](.gitbook/assets/image%20%28541%29.png)

![](.gitbook/assets/image%20%28584%29.png)

```text
{
"privileges": [
{"name": "Execute", "description": "Execute"}
]
}
```

![](.gitbook/assets/image%20%28566%29.png)









새로운 파일

만드는 파일들은 ODATA 서비스 위해 필요

![](.gitbook/assets/image%20%28554%29.png)

![](.gitbook/assets/image%20%28587%29.png)



![](.gitbook/assets/image%20%28592%29.png)

세번째 탭 &gt; + 버튼 누르면 뜨는 다음과 같은 창: runbtime 선택, store 검색해서 아까 만든 strore schema 선택

![](.gitbook/assets/image%20%28581%29.png)

옆에 나오는 privileges를 다음과 같이 체크 

![](.gitbook/assets/image%20%28596%29.png)

이번에는 다섯번째 탭에 가서 + 누르기

execute, 맨 처음꺼 클릭 

![](.gitbook/assets/image%20%28559%29.png)







지금까지 하고 role 파일 우클릭 해서 text로 open with하면 

다음과 같이 script 확인 가능 

![](.gitbook/assets/image%20%28604%29.png)



## 5. xs odata

![](.gitbook/assets/image%20%28607%29.png)



![](.gitbook/assets/image%20%28615%29.png)

```text
service {
"STORE"."BOOK" as "BOOK"
create forbidden
update forbidden
delete forbidden;
"STORE"."CUSTOMER" as "CUSTOMER"
create forbidden
update forbidden
delete forbidden;
}
```

![](.gitbook/assets/image%20%28574%29.png)

실행시

url이 xsodata로 끝나는 이 서버가 odata service를 호출하기 위한 full url 

[https://cp10024p2002339716trial.hanatrial.ondemand.com/mypackage/services.xsodata](https://cp10024p2002339716trial.hanatrial.ondemand.com/mypackage/services.xsodata)

![](.gitbook/assets/image%20%28572%29.png)

data service를 이용할 수 있도록 만들어진 url, 이를 활용해서 application에 사용











## 여기부터 8월 28일 수업!

## . Odata Service 등록 

HANA 데이터 베이스에서 생성한 데이터를 새로운 프로젝트의 OData Service로 연결해본다.   
이전에 URL로 새로운 데이터를 연결했던 방식과 동일하다.

우선 위에서 생성한 HANA DataBase의 OData URL을 복사해오고, 새로운 프로젝트를 WEB IDE에 생성한다.  
새로운 프로젝트 STUDYPROJECT06을 만드는 과정은 생략했다. STUDYPROJECT06에 새로운 OData Service를 등록한다. 

{% hint style="info" %}
manifest.json &gt; Data Source &gt; + &gt; URL Service &gt; Create new
{% endhint %}

새로 생성한 프로젝트의 manifest.json 파일의 Data Source 탭으로 가서 + 버튼을 눌러 새로 등록한다. 

![STUDYPROJECT06 &amp;gt; manifest.json](.gitbook/assets/image%20%28613%29.png)

Service URL을 클릭하고 create a new data source를 누른다. 

![manifest.json &amp;gt; Data Source &amp;gt; +](.gitbook/assets/image%20%28624%29.png)

입력 창에 다음 정보를 입력한다.   
본인의 경우 URL에 위에서 생성한 HANA OData URL로 다음 정보를 입력했다. [https://cp10024p2002339716trial.hanatrial.ondemand.com/mypackage/services.xsodata](https://cp10024p2002339716trial.hanatrial.ondemand.com/mypackage/services.xsodata)  
그리고 해당 HANA DB의 사용자이자 생성자인 USER는 DEV24로 권한을 받아왔다.  


<table>
  <thead>
    <tr>
      <th style="text-align:left">&#xC785;&#xB825; &#xCE78;</th>
      <th style="text-align:left">&#xC785;&#xB825; &#xC815;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">User ID / Password</td>
      <td style="text-align:left">SCP Cockpit &#xB85C;&#xADF8;&#xC778; &#xC815;&#xBCF4;</td>
    </tr>
    <tr>
      <td style="text-align:left">Name</td>
      <td style="text-align:left">OData Service &#xC774;&#xB984; (&#xBCF8;&#xC778;&#xC774; &#xC784;&#xC758;
        &#xC124;&#xC815;)</td>
    </tr>
    <tr>
      <td style="text-align:left">URL</td>
      <td style="text-align:left">
        <p>&#xB370;&#xC774;&#xD130; &#xAC00;&#xC838;&#xC62C; URL</p>
        <p>HANA DB&#xC5D0;&#xC11C; &#xC0DD;&#xC131;&#xD55C; OData URL &#xC785;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Username / Password</td>
      <td style="text-align:left">&#xC124;&#xC815;&#xD55C; URL &#xC989;, &#xC5F0;&#xACB0;&#xD558;&#xB294;
        DB&#xC758; &#xC720;&#xC800; &#xC815;&#xBCF4;</td>
    </tr>
  </tbody>
</table>

![manifest.json &amp;gt; Data Source &amp;gt; + &amp;gt; create a new data source](.gitbook/assets/image%20%28556%29.png)

입력된 URL 정보로 데이터가 연결됬는지 확인하기 위해 URI에는 /를 입력한다. 생성했던 BOOK, CUSTOMER entity가 확인되면 다음 버튼을 눌러 저장한다. 

![](.gitbook/assets/image%20%28588%29.png)



