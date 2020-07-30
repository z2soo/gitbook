# Untitled

사원 정보를 등록하기 위한 pop up 정보 입력 창을 띄우는 것까지 구현하였다. 이제는 이 창에 값을 입력하여 저장 버튼을 입력시, DB 테이블과 ALV에 반영되도록 해주는 과정을 진행해보도록 한다. 이를 위해서는 다음의 과정을 따른다. 

1. 입력 데이터가 DB에 저장이 되도록 함
2. 성공적으로 저장될 경우, Internal table에 append
3. Refresh하고 사원등록 팝업 창을 닫아주면 ALV에도 반영이 되도록 함



내가 작성한 부분과 강사님 코드 차이 존재

강사님은 ITAB에 APPEND 해주고 나는 아얘 새로 UPDATE된 DB를 다시 읽어옴

중요한 부분은 PATTERN: REFRESH FOR THE TABLE DISPLAY







