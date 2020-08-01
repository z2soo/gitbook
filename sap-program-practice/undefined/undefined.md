---
description: >-
  조회 스크린에서 조회되는 값 중 부서, 직급, 재직구분의 도메인 값에 따른 range value 즉, 실제 의미하는 도메인 텍스트 데이터를
  가져와 추가해준다.
---

# 도메인 값 추가

> 도메인 텍스트 가져오기  
> ZR025\_0010\_EX02 파일이 도메인 값 가져오기 완료한 파일 
>
> 버튼 및 팝업 창 생성한 부분  
> ZR025\_0010\_EX03 파일이 버튼 및 정보 입력 팝업창 생성 완료 한 파일



## 1. Domain range value 추가

### 1\) Structure 선언

도메인 value에 따른 text 값을 담기 위한 structure가 필요하다. 









![](../../.gitbook/assets/image%20%28194%29.png)

생성된 버튼에 대한 USER COMMAND 생성

//



![](../../.gitbook/assets/image%20%28178%29.png)

통화키를 참조하도록 하여 기본급 SALARY를 설정: GS\_0200-WAERS

