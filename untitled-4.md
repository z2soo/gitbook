# Untitled

crud 기능을 각각 따로의 function module로 생

![](.gitbook/assets/image%20%28671%29.png)



![](.gitbook/assets/image%20%28755%29.png)

![](.gitbook/assets/image%20%28689%29.png)

![](.gitbook/assets/image%20%28727%29.png)

![](.gitbook/assets/image%20%28704%29.png)







![](.gitbook/assets/image%20%28696%29.png)





//

odata service를 만들기 위한 gate way 만들기

t-code segw

024로 만

![](.gitbook/assets/image%20%28706%29.png)

![](.gitbook/assets/image%20%28695%29.png)

![](.gitbook/assets/image%20%28672%29.png)

table울 가지고 entity set structure 만둘 것

entity set 이름처럼 이름 주는 것

abap structure눈 위에서 만든 tavble 이름

![](.gitbook/assets/image%20%28720%29.png)

![](.gitbook/assets/image%20%28716%29.png)

![](.gitbook/assets/image%20%28731%29.png)

![](.gitbook/assets/image%20%28685%29.png)

![](.gitbook/assets/image%20%28759%29.png)

![](.gitbook/assets/image%20%28677%29.png)

상단 register &gt; package나 local해주기 

![](.gitbook/assets/image%20%28742%29.png)

그러면 register 파란불 구라고 sap gate way

이제 functuin mapping

![](.gitbook/assets/image%20%28761%29.png)

![](.gitbook/assets/image%20%28724%29.png)

f4누르면 확인 가

![](.gitbook/assets/image%20%28670%29.png)

아까 생성한 함수는 값을 입력받아서 테이블에 create, delete, update,,,등의 행동을 해주는 것

화면에서 odata service로 데이터 주고받을 때 property가 위에서의 pproperty ; IDE에서 보여지는 ...  이것과 입력하는 값을 mapping 

data source parameter: 함수에 입력되눈 



![](.gitbook/assets/image%20%28737%29.png)

![](.gitbook/assets/image%20%28679%29.png)

마찬가지로 delete, update 또한 mapping 해줌  
지금까지의 설명: ide에서 입력하거나 실행?하게되는 부분이 왼쪽의 entity set property이고 이 값을 odata service에 연결받아? map해서 이를 data source parameter로 mapping해주는 것data source parameter는 functino의 입력값으로 들어감



query는 다중행의 값이 결과로 나오고 read는 단일행의 값이 결과로 나옴  
get entity, get entity set에도 함수 mapping하면되는데 read라는 부분에 무조건 mapping되어 있어야지 나머지 함수들도 수행됨\(값을 읽어야지 수행할 수 있기 떄문, create 제\)  
  
 get entity mapping해줌 그 중 read

이때 row 하나 추가해서 empid추가: 이곳운 위에처럼 mapping; iv로 mapping  


![](.gitbook/assets/image%20%28700%29.png)

![](.gitbook/assets/image%20%28693%29.png)

나멎; 부분은 ET부분이랑 map하면 화설표가 반대로 map될 

![](.gitbook/assets/image%20%28680%29.png)

머마찬가리조 query부분도 해줌;zmm\_emp\_24\_get으로 mapping

![](.gitbook/assets/image%20%28705%29.png)



gateway 해서 execute 만약 에러나면

maintain 들어가서 아래로 node연결 

![](.gitbook/assets/image%20%28683%29.png)

![](.gitbook/assets/image%20%28668%29.png)

![](.gitbook/assets/image%20%28728%29.png)



sap gate way &gt; execute &gt; 200으로 정

![](.gitbook/assets/image%20%28667%29.png)

![](.gitbook/assets/image%20%28691%29.png)

상단 entity set &gt; 여러개 등록 ㅏ능 

![](.gitbook/assets/image%20%28725%29.png)

url 변경됨

![](.gitbook/assets/image%20%28750%29.png)

optoin우로 다양한 정보 확인가능



![](.gitbook/assets/image%20%28729%29.png)

//

상단 method로 crud test버로 해봏 수 있

![](.gitbook/assets/image%20%28699%29.png)

update로 한번 해보자

/



WEB IDE에서 새로운 프로젝트 생성, ODATA 생성; 위에서 만든 푸로젝트 이룸으로

[http://doidesap.dfocus.net:8010/sap/opu/odata/SAP/ZMM\_emp\_024\_srv](http://doidesap.dfocus.net:8010/sap/opu/odata/SAP/ZMM_emp_024_srv)



![](.gitbook/assets/image%20%28694%29.png)

![](.gitbook/assets/image%20%28703%29.png)

