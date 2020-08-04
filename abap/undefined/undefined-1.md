---
description: PERFORM으로 값을 주고받는  형식으로 코드를 정리해본다.
---

# 코드 정리

> ZR025\_0010\_EX05  
> 04 파일에서 코드정리하고 난 파일이 EX05  
> 추가적으로 COMMIT 구문도 입력되었음

Commit 구문을 추가했다. 현재 상황에서는 큰 의미가 없고, ABAP에서는 자동 commit 기능이 있기 때문에 평소에도 필요성을 느끼지 못했을 수 있지만 중요한 부분이다. 

DB에 가반영 상태에서 COMMIT을 하기 전까지 약간의 시간이 존재한다. 이 시간 차이 때문에 사용자가 사용시 됬다 안됬다 하는 경우가 있다. 따라서 COMMIT AND WAIT 옵션은 COMMIT 반영이 끝날 때 까지 기다렸다가 다음을 수행하도록 설정해준다. 
