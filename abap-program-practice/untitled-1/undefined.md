---
description: >-
  해당 프로그램을 생성하기 전에 BDC에 대해 먼저 학습하도록 한다. 원래 PARAMETER로 값을 입력해서 조회하거나 저장했다면, EXCEL
  파일을 올려 내부 프로그램에 해당 데이터를 저장하고, 이를 DB에 다시 저장하는 프로그램을 생성해본다. 이 때, EXCEL로 올려 내부에
  저장한 데이터를 DB에 저장할 때에는 BDC를 활용한다.
---

# 엑셀 데이터 업로드 및 변환

## 1. 프로그램 및 엑셀 파일 생성

생성해 ALV template을 복사하여 프로그램을 생성하고, 아래를 참조하 조회 및 결과 화면을 만들어준다.   
마찬가지로 ABAP에 업로드할 자재 마스터 생성 정보를 다음과 같은 구조로 작성해 엑셀 파일을 생성한다.



### 조회화면 및 결과화면 예시 

![&#xC6B0;&#xC120;&#xC801;&#xC73C;&#xB85C; &#xAD6C;&#xD604;&#xD560; Selection screen / ALV &#xD654;&#xBA74;](../../.gitbook/assets/image%20%28372%29.png)



### 자재 마스터 엑셀 파일 예시 

![&#xC62C;&#xB9AC;&#xACE0;&#xC790; &#xD558;&#xB294; EXCEL &#xD30C;&#xC77C; &#xB0B4;&#xC5ED;](../../.gitbook/assets/image%20%28383%29.png)



## 2. Excel file 정보 입력

### 1\) Excel file 경로 입력창 설정 

엑셀 파일의 경로를 입력받을 parameter를 생성해준다. 우선 문자 타입으로 만들어준다.   
보기 편하게 Selection texts를 활용해 파일경로로 보이 parameter 변수명을  바꿔준다.

![Selection screen](../../.gitbook/assets/image%20%28340%29.png)

![Selection texts](../../.gitbook/assets/image%20%28342%29.png)



### 2\) Search help 설정 

실행해보면 직접 모든 부분을 입력해야 한다. 따라서 search help 기능을 추가해준다. 단, 이전까지 사용하던 것과 내부에 저장된 값을 search help로 이용하는 것이 아니기 때문에 사용자 정의 값으로 search help를 사용하도록 설정한다. 

![](../../.gitbook/assets/image%20%28394%29.png)

![&#xC2E4;&#xD589; &#xD654;&#xBA74;](../../.gitbook/assets/image%20%28349%29.png)



### 3\) FILE\_OPEN\_DIALOG 설정 

실행해보면 일반적으로 파일을 가져올 때 사용하는 것 처럼 파일 선택 창이 뜨지 않고, 직접 모든 주소 값을 입력해줘야 한다. 따라서 해당 기능을 추가해준다. 

{% hint style="info" %}
CL\_GUI\_FRONTED\_SERVICES=&gt;FILE\_OPEN\_DIALOG : 파일 선택 창 기능 
{% endhint %}

![CL\_GUI\_FRONTED\_SERVICES=&amp;gt;FILE\_OPEN\_DIALOG](../../.gitbook/assets/image%20%28357%29.png)

해당 method를 사용하기 위해서는 다음 두 값이 필수적으로 입력되야 한다.  
따라서 필요한 WA 및 데이터 또한 선언해준다. 

| 입력 값 | 설명  |
| :--- | :--- |
| FILE\_TABLE  | Table Holding Selected Files |
| RC | Return Code, Number of Files or -1 If Error Occurred |

이 때, 파일의 path를 얻기 위한 해당 코드는 main program에서 selection screen 이후에 GET\_FILE\_PATH 라는 이름의 새로운 form으로 생성해주었다. 

![Main program](../../.gitbook/assets/image%20%28346%29.png)

![GET\_FILE\_PATH](../../.gitbook/assets/image%20%28376%29.png)

실행해보면, 다음과 같이 파일을 선택할 수 있는 창이 뜬다. 

![FILE\_OPEN\_DIALOG](../../.gitbook/assets/image%20%28395%29.png)

하지만 업로드하고자 하는 파일을 선택해줘도, parameter 입력칸에 주소 값이 들어가지 않는다.  
이는 LT\_FILE 이라는 테이블에 주소 값을 읽어들였으나, parameter 변수에 할당되지 않았기 때문이다.   
이를 위해 파일 주소 값을 가지고 있는  LT\_FILE 테이블을 읽어 parameter 변수\(ex. PA\_PATH\)에 넣어준다. 

![GET\_FILE\_PATH](../../.gitbook/assets/image%20%28390%29.png)

그 다음 실행하면 다음과 같이 주소가 들어감을 확인할 수 있다. 

![Selection screen](../../.gitbook/assets/image%20%28353%29.png)



## 3. Excel file upload

### EXCEL UPLOAD

![](../../.gitbook/assets/image%20%28377%29.png)

다음 함수 사용

![](../../.gitbook/assets/image%20%28375%29.png)

### 값 입력을 위해 TYPE 설정

LT\_INTERN 생성 

![](../../.gitbook/assets/image%20%28366%29.png)

![](../../.gitbook/assets/image%20%28348%29.png)

### 함수를 통해 받은 값을 저장

GS\_EXCEL 생성 

![](../../.gitbook/assets/image%20%28352%29.png)

### 저장된 GT\_EXCEL 값을 GT\_DISP로 옮겨주고 ALV에 뿌려주기

뿌려주는 부분 PERFORM으로 생성 

![](../../.gitbook/assets/image%20%28361%29.png)

![](../../.gitbook/assets/image%20%28341%29.png)

지금까지 결과는 다음과 같다. 

![](../../.gitbook/assets/image%20%28365%29.png)



![](../../.gitbook/assets/image%20%28356%29.png)

![](../../.gitbook/assets/image%20%28381%29.png)

