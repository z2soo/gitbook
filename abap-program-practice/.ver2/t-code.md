---
description: '조회 및 관리 두 가지의 T-code를 생성하여, 조회인 경우에는 데이터를 변경하지 못하게 설정한다.'
---

# T-code 생성

> 하나의 프로그램에 대해 여러 개의 T-code를 생성하고, Exclude를 통해 서로 다른 권한\(조회, 생성 등\)을 부여할 수 있다.

## 1. T-code 생성

T-code 생성시 프로그램명과 스크린 번호를 맞춰 작성해준다. 

### 조회용 T-code 생성 

![](../../.gitbook/assets/image%20%28280%29.png)

![](../../.gitbook/assets/image%20%28285%29.png)



### 관리용 T-code 생성 

![](../../.gitbook/assets/image%20%28267%29.png)

![](../../.gitbook/assets/image%20%28281%29.png)

### 

## 2. Exclude 설정

{% hint style="info" %}
SET PF-STATUS 구문에 EXCLUDE 사용하여 T-code별 설정 가능
{% endhint %}

Screen의 STATUS 설정에서 T-code에 따라 다른 설정이 가능하며, EXCLUDE를 사용한다. 

![TOP &amp;gt; GT\_EXCLUDE &#xC120;&#xC5B8;](../../.gitbook/assets/image%20%28287%29.png)

![Screen 0100 &amp;gt; STATUS\_0100](../../.gitbook/assets/image%20%28284%29.png)





