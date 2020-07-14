# Oracle 설치 및 환경설정

## 1. 프로그램 설치

###  Oracle Database 11G 프로그램 다운

* [https://www.oracle.com/kr/index.html](https://www.oracle.com/kr/index.html)



### 프로그램 설치

해당 프로그램은 교육용으로 제공되어진다. 프로그램을 설치하기 이전에 우선 두 개의 파일로 다운받아진 폴더의 압축을 풀어 하나의 폴더로 합쳐줘야 한다. 그 후에 설치를 진행한다. 

![&#xB450; &#xAC1C;&#xB85C; &#xB2E4;&#xC6B4;&#xBC1B;&#xC544;&#xC9C4; &#xD504;&#xB85C;&#xADF8;&#xB7A8;](../../.gitbook/assets/image%20%2889%29.png)

![Oracle &#xC124;&#xCE58; &#xC2DC;&#xC791;](../../.gitbook/assets/image%20%2869%29.png)

![&#xBCF4;&#xC548;&#xAC31;&#xC2E0;&#xC218;&#xC2E0; &#xBBF8;&#xC124;&#xC815;](../../.gitbook/assets/image%20%2895%29.png)

교육용이기 때문에 보안갱신 수신에 대해 받지 않음으로 설정한다.

![&#xB370;&#xC774;&#xD130;&#xBCA0;&#xC774;&#xC2A4; &#xC0DD;&#xC131; &#xBC0F; &#xAD6C;&#xC131; &#xC124;&#xC815;](../../.gitbook/assets/image%20%2894%29.png)

설치 옵션으로 데이터 베이스를 생성하도록 설정한다.

![](../../.gitbook/assets/image%20%2882%29.png)

![&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC704;&#xCE58; &#xC124;&#xC815;](../../.gitbook/assets/image%20%2886%29.png)

Oracle의 기본 생성 계정은 **sys** 로써, 이는 **삭제 불가한 계정**이다.  관리 비밀번호를 설정해준다.   
이때, 아래와 같은 알람이 뜨는 이유는 비밀번호의 보완성이 낮기 때문이며 계속 진행 가능하다. 

![&#xC554;&#xD638; &#xC124;&#xC815;](../../.gitbook/assets/image%20%2890%29.png)

![](../../.gitbook/assets/image%20%2884%29.png)

![](../../.gitbook/assets/image%20%2888%29.png)

 다음 과정까지 모두 마치면 Oracle 프로그램 설치가 완료된다. 다음과 같이 뜨는 창에서 비밀번호관리를 눌러 게정에 대한 잠금, 해제, 비밀번호 등을 관리할 수 있다. 이 방법 외에는 다음 목차의 **프로그램 실행 과정을 통해서 계정 잠금 해제가 가능**하다. 

![&#xAC8C;&#xC815; &#xBC0F; &#xBE44;&#xBC00;&#xBC88;&#xD638; &#xAD00;&#xB9AC;](../../.gitbook/assets/image%20%2877%29.png)



## 2. 프로그램 실행 및 환경설정 

### **CMD PROMPT 접속**

![](../../.gitbook/assets/image%20%2893%29.png)



### Oracle 연결 및 계정 설정

* sql 연결: sqlplus /nolog 
* 관리자\(sys\)로 DB 접속: connect sys/oracle as sysdba
* 샘플 계정 전환 및 잠금풀기: alter user scott, alter user hr

![](../../.gitbook/assets/image%20%2878%29.png)



### Oracle 계정 확인  

샘플 계정 scott 으로 database를 연결한다. dual은 기본으로 제공되어지는 table 로써 user, emp 등 여러 자료가 들어가 있다. 이 table에 대한 정보를 sql plus에서 확인하는 작업을 진행해보도록 하겠다. 

* 계정 연결: conn 계정이름/비밀번호
* 연결 계정 확인: select user from dual;
* 연결 계정 테이블 목록 확인: select table\_name from user\_tables;
* 테이블 정보 확인: desc 또는 describe 테이블명

![scott &#xACC4;&#xC815; &amp;gt; user &#xD655;&#xC778;](../../.gitbook/assets/image%20%2879%29.png)

![user&#xC758; table &#xBAA9;&#xB85D; &#xD655;&#xC778;](../../.gitbook/assets/image%20%2892%29.png)

![table &#xC815;&#xBCF4; &#xD655;&#xC778;](../../.gitbook/assets/image%20%2883%29.png)



### **기타 Oracle SQL Query**

```sql
# Host IP 주소 확인
select utl_inaddr.ger_host_name from dual;

# DB 버전 확인 
v$version;

# DB 이름 확인
select * from global_name;

# DB 계정명 확인
select user from dual 또는 select name from sys.user$;

# DB 리스트 확인
select DISTINCT owner from all_tables;

# 권한 확인
select * from session_privs;

# DB 컬럼 리스트 확인
select * from cols;
```

