---
description: SAP GUI ABAP 프로그램과 Github울 연결해본다.
---

# ABAP Git 연동

## 1. Github 생성

SAP GUI ABAP 프로그램과 Github repository를 연결하기 앞서 Githhub 계정을 생성한다. 

{% embed url="https://github.com/" %}

\*\*\*\*

## 2. ABAP Git Report 생성

{% hint style="info" %}
T-Code SE80/SE28 &gt; new Reoport 생성 &gt; 코드 입력
{% endhint %}

새로운 프로그램 즉, report를 생성하고 abapGit에서 제공하든 다음 코드를 입력한다. 

{% embed url="https://raw.githubusercontent.com/abapGit/build/master/zabapgit.abap" %}

ZABAP\_Z2SOO 이름으로 새로운 Program울 생성해 위의 코드를 붙여넣은 후에 activate 해주었다. 

![](../../.gitbook/assets/image%20%28700%29.png)

//

se38 

![](../../.gitbook/assets/image%20%28712%29.png)

![](../../.gitbook/assets/image%20%28678%29.png)

![](../../.gitbook/assets/image%20%28681%29.png)

## 3. SSL 설정

Secure Socket Layer 라는 보안 인증서 활성화 작업이 있으나, 회사 서버를 사용함으로써 이 부분에 대한 설정이 따로 필요하지는 않았다. 만약 필요하다면, abapGit에서 제공하는 다음의 documentation과 자세하게 설명된 아래의 블로그 글을 참조하도록 한다. 

{% embed url="https://docs.abapgit.org/guide-install.html" %}

{% embed url="https://blog.naver.com/howwithus/221738403324" %}

{% embed url="https://www.digicert.com/kb/digicert-root-certificates.htm" %}

![](../../.gitbook/assets/image%20%28706%29.png)

![](../../.gitbook/assets/image%20%28692%29.png)

![](../../.gitbook/assets/image%20%28718%29.png)

![](../../.gitbook/assets/image%20%28674%29.png)

t-code strust



![](../../.gitbook/assets/image%20%28682%29.png)

SSL\_client\_SSL\_Client\(Anonymous\)를 클릭하고 들어오면 최초에는 Certification List가 없습니다.

위에서 다운로드 받은 인증서를 import하고 적용합니다.**\[출처\]** [\[SAP ABAP\] abapGit 으로 ABAP Open Source 프로그램 생성하기](https://blog.naver.com/howwithus/221738403324)\|**작성자** [곰선비](https://blog.naver.com/howwithus)



![](../../.gitbook/assets/image%20%28710%29.png)

![](../../.gitbook/assets/image%20%28672%29.png)

![](../../.gitbook/assets/image%20%28698%29.png)







![](../../.gitbook/assets/image%20%28699%29.png)

## 4. Git Repository 생성

![](../../.gitbook/assets/image%20%28717%29.png)

![](../../.gitbook/assets/image%20%28685%29.png)





