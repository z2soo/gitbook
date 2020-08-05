---
description: BAPI Funtion을 어떻게 적용하여 활용하는지 기초적인 부분을 익혀본다.
---

# BAPI 활용 기초

## 1. BAPI\_PO\_CHANGE 활용

> 프로그램을 실행하여 구매문서 번호와 판매자를 입력받고, 해당 구매문서의 판매자를 입력받은 이름으로 변경하는 프로그램을 짜보도록 한다. 참고로 판매오더에 대한 정보는 EKKO 테이블에 있다.



### 프로그램 생성 

우선적으로 기반이 되는 프로그램을 생성해준다. 이 부분에 대한 코드는 아래를 참조하도록 한다. 

![Main program](../.gitbook/assets/image%20%28272%29.png)

구매문서 번호 및 바꿔서 넣고자 하는 생성자 이름에 대해 다음과 같이 Parameter로 받아준다. 

![Selection screen](../.gitbook/assets/image%20%28282%29.png)

Text element 부분에서 다음과 같이 parameter 입력 변수 이름에 문자를 설정해준다. 

![Text element](../.gitbook/assets/image%20%28286%29.png)



### BAPI\_PO\_CHANGE 

Selection screen에서 입력받은 값을 가지고 특정 PO의 판매자 이름를 변경하고자 한다. 이를 위해 BAPI Function을 추가하고 필요한 값을 입력해준다. 

![](../.gitbook/assets/image%20%28270%29.png)

//

해당 PO에서 SALES PERSON에 이름을 넣어주고 싶은 상황이다.



![M23N &amp;gt; PO&#xC870;&#xD68C;](../.gitbook/assets/image%20%28274%29.png)

![&#xD504;&#xB85C;&#xADF8;&#xB7A8; &#xC2E4;&#xD589;](../.gitbook/assets/image%20%28287%29.png)

![](../.gitbook/assets/image%20%28294%29.png)

JISOO 값이 들어갔음을 확인할 수 있다. 

