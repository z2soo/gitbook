# 사원 데이터 변경 기능

> 라인 선택하여 변경 버튼 누르면 해당 정보가 담긴 팝업 창이 뜨고 이것을 변경하는 코드 작성  
> 1\) 선택한 라인 확인  
> 2\) 팝업에 출력할 데이터 받아오기   
> 3\) 스크린 호출: get selected rows 함수 사  
> ZPJT01\_25 여기 7번 파일



///////////////////////////////////////////////////

![](../../.gitbook/assets/image%20%28215%29.png)

![](../../.gitbook/assets/image%20%28212%29.png)

이렇게 만들어서 실행해보니까 사원 데이터가 기존 값이 변경되는 것이 아닌, 새로운 값이 저장됨. 따라서 이에 대한 해결 필요.

기존에는 저장시 INSERT를 사용하였음. 그러나 이를 MODIFY로 변경해주면 문제 해결!

MODIFY는 이중적으로 사용이되는데, 일반 db에 사용하는 modify와 인터널테이블에 사용하는 modify가 있다. db에 modify를 하면 키값이 일치하는 자료가 있으면 update, 없으면 insert가 됩니다. 그러나 인터널테이블에서는 update 역할만 하게 됩니다. 자료가 없을 경우에 insert가 되지 않습니다.인터널테이블에 자료를 modify 하실때 자료가 없다면 append \( 또는 insert\) 해줘야 합니다..

![](../../.gitbook/assets/image%20%28214%29.png)

보니까 생성시 생성자 아이디, 시간, 날짜를 받게 안해서 그거 설정해줌

그리고 변경시 변경자 아이디, 시간, 날짜 받게해서 설정해줘야되서 위에 코드 조금 변경함, 이제 관련 값들도 db 테이블에 들어옴

![](../../.gitbook/assets/image%20%28211%29.png)

![](../../.gitbook/assets/image%20%28206%29.png)

사원 코드는 변경되면 안됨. 이를 lock하는 방법은??


