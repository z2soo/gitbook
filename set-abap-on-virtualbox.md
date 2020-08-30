# Set ABAP on VirtualBox

{% embed url="https://www.virtualbox.org/wiki/Downloads" %}



![](.gitbook/assets/image%20%28651%29.png)

![](.gitbook/assets/image%20%28656%29.png)

platform 다운, 밑에 있는 extension box 다운 및 설치: 기본 window10이 아닌 가상머신에 설치하기 위함  
실행 및 경로 추가  

![](.gitbook/assets/image%20%28650%29.png)

![](.gitbook/assets/image%20%28653%29.png)

![](.gitbook/assets/image%20%28654%29.png)

![](.gitbook/assets/image%20%28655%29.png)

abap prgram 파일 경로로 들어가면 파란 아이콘 있음. 더블 클릭시 그린색 나옴,   
파일&gt;환경설정&gt;확장\(extension\)&gt;+버튼&gt;extension pack 클릭&gt;팝업뜨면 ok클릭

이제 시작 누름 



실행시 start sap server 메모장 &gt; 빈공간에 우클릭 &gt; 맨아래 open terminal &gt; 신규 terminal에 다음 입력

```text
su- l npladm 엔터 // npladm은 자동 ㅇ성되는 유저
비밀번호 입력 // 화면상에 안보임

npladm 프롬프트 생성
startsap all 엔터 //sap server ㅣㄹ행 
stopsap all 엔터 //sap server 중지
```

스타트 하고 나가서 sap 프로그램 실행, 새로운 entry 생

{% hint style="info" %}
Custom Application Server  
NPL \[127.0.0.1\]  
127.0.0.1
{% endhint %}

새 생성한 entry로 로그인: 다음 중 하나 

* DEVELOPER / Appl1ance
* SAP\* / Appl1ance
* BWDEVELOPER / Appl1ance

SAP\* 로그인 &gt; T-CODE: SU01에서 DEVELOPER 검색 &gt; CHANGE &gt; LOGON DATA &gt; NEWPASSWORD &gt; SAVE

다시 DEVEOPLER 계정으로 로그인시 다시 비밀번호 바꾸라고 뜨는데 바꾸고 로그인 





데이터 베이스 및 SAP 라이센스 존재

{% embed url="https://abapacademy.com/blog/sap-trial-license-expired-how-to-prolong-sap-trial-license/" %}

만약 라이센스 에러 뜬다면 위의 블로그 참조해서 아래 사이트로 들어감

{% embed url="https://go.support.sap.com/minisap/" %}



![](.gitbook/assets/image%20%28657%29.png)

![](.gitbook/assets/image%20%28652%29.png)

선택: 하드웨어 키가 필수임: U1515553033 &gt; GENERATE &gt; 텍스트 파 나

SAP GUI에서 SLICENSE &gt; EDIT &gt; DELETE LICENSE &gt; INSTALL ICENSE\(위 텍스트 파일 추가\)

* LICENSE작업 : SAP LICENSE
* SYBASE DATABASE: 만료 4/1 : 다시 다운받아야 함  

이제 이 DEVELOPER로 사용하면 





