# HANA Database 연결

## 1. Database 생성

{% hint style="info" %}
SCP Cockpit &gt; SAP HANA/SAP ASE &gt; 데이터베이스 핫 스키마 &gt; 신규
{% endhint %}

데이터 이관을 위한 데이터베이스를 생성해준다. 이때 중요한 것은 마지막 DP 서버 항목을 켬으로 체크해준다.

![](../.gitbook/assets/image%20%28761%29.png)

![](../.gitbook/assets/image%20%28721%29.png)



## 2. User 생성

![](../.gitbook/assets/image%20%28718%29.png)

system으로 로그인해서 새로운 SDI\_USER 생성 및 권한 부여

![](../.gitbook/assets/image%20%28739%29.png)

다시 로그인해서 비밀번호 변경

SDI\_AGENT 유저도 새로 생성, 권한부여, 비밀번호 재설정, 오류나지만 ㅇㅋㅇㅋ

![](../.gitbook/assets/image%20%28717%29.png)



## JAVA / Ecplipse 설치 

해당 파일 디운로드

ecli\[se oxygen을 쓰는 이유는 하나 데이터 이관이 그 버전만 가능하기 떼문

oxyen eclipse를 다운

{% embed url="https://www.oracle.com/java/technologies/javase-jdk14-downloads.html" %}

{% embed url="https://www.java.com/ko/download/" %}

{% embed url="https://www.eclipse.org/downloads/packages/release/oxygen/3a/eclipse-ide-java-ee-developers" %}

이클립스 설치

![](../.gitbook/assets/image%20%28550%29.png)

![](../.gitbook/assets/image%20%28647%29.png)

![](../.gitbook/assets/image%20%28552%29.png)

## 2. SAP 프로그램 설치 

![](../.gitbook/assets/image%20%28618%29.png)

[ https://tools.hana.ondemand.com/oxygen](%20https://tools.hana.ondemand.com/oxygen)

![](../.gitbook/assets/image%20%28578%29.png)

![](../.gitbook/assets/image%20%28576%29.png)

![](../.gitbook/assets/image%20%28642%29.png)

![](../.gitbook/assets/image%20%28545%29.png)

## 3. Database 연동 

![](../.gitbook/assets/image%20%28666%29.png)

![](../.gitbook/assets/image%20%28661%29.png)

password \(컴퓨처 로그인\) 설정해줌 다시 아래 설



![](../.gitbook/assets/image%20%28752%29.png)

윈도우키 + cmd 입력 &gt; cmd 까창 띄움 &gt;  services.msc 입

![](../.gitbook/assets/image%20%28660%29.png)

다음 아래 창 뜨면 SAP\_HANA\_SDI\_Agent\_Service\_Daemon\_AHJ 파일 찾아서 우클릭 &gt; 속

![](../.gitbook/assets/image%20%28662%29.png)

속성에서 설정 로컬로 변경 &gt; 저장 &gt; Agent db 재실행 및 start agent  
만약 microsoft 계정으로 로그인되어 있으면 계정지정에다가 해당 뎨ㅓㅇ 및 비밀번호 입력해주면 된다.

![](../.gitbook/assets/image%20%28659%29.png)

![](../.gitbook/assets/image%20%28663%29.png)



db

/////////////////////////////////////?

![](../.gitbook/assets/image%20%28747%29.png)

![](../.gitbook/assets/image%20%28673%29.png)

컴터 비

![](../.gitbook/assets/image%20%28713%29.png)

![](../.gitbook/assets/image%20%28733%29.png)

관리툴 콕피트로 들어가서 그 주소를 의미 

`cp10024p2002339716trial.hanatrial.ondemand.com`

![](../.gitbook/assets/image%20%28746%29.png)

![](../.gitbook/assets/image%20%28669%29.png)

![](../.gitbook/assets/image%20%28745%29.png)

![](../.gitbook/assets/image%20%28737%29.png)

ABAP Adapter를 register adapter

## hana workbench 작업

system 계정으로 로그인

![](../.gitbook/assets/image%20%28697%29.png)

![](../.gitbook/assets/image%20%28684%29.png)

![](../.gitbook/assets/image%20%28706%29.png)

![](../.gitbook/assets/image%20%28750%29.png)

```text
GRANT CREATE VIRTUAL TABLE ON REMOTE SOURCE "S4HANA" TO _SYS_REPO;
```

DATA REPLICATION TASK 생성

![](../.gitbook/assets/image%20%28688%29.png)

![](../.gitbook/assets/image%20%28755%29.png)

![](../.gitbook/assets/image%20%28756%29.png)

![](../.gitbook/assets/image%20%28707%29.png)

![](../.gitbook/assets/image%20%28714%29.png)

![](../.gitbook/assets/image%20%28731%29.png)

![](../.gitbook/assets/image%20%28722%29.png)

![](../.gitbook/assets/image%20%28759%29.png)

catalog로 딧; ㅇ;동

![](../.gitbook/assets/image%20%28744%29.png)

![](../.gitbook/assets/image%20%28676%29.png)

![](../.gitbook/assets/image%20%28743%29.png)

![](../.gitbook/assets/image%20%28709%29.png)

