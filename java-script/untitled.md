# HTML 기초문법

## 1. 소스 코드 

```markup
<!--이게 주석-->
<!DOCTYPE html><!--원래 이자리에 버전에 대한 문장 있음-->
<!-- html 버전. 안쓰면 html5

    <xxx> : 시작태그  <xxx 속성명='값', 속성명='값', ...>
    </xxx> : 종료태그

    DOM 객체 (Document object Model): 홈페이지 뼈대 만드는 언어.
-->

<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>

</head>
<body>
    br은 한 줄 바꾸기<br>
    hr은 가로선, 한 줄 바꾸기<hr>
    <p>p는 단락범위</p>
    &nbsp;띄&nbsp;어&nbsp;쓰&nbsp;기<br>
    'less than' 모양 : &lt;<br>
    'greater than' 모양: &gt<br>

    <hr>
    <font size='7' face='휴먼옛체' color='purple'>폰트적용</font><br>
    색을 제대로 넣고 싶으면 #RRGGBB 색상표로 넣어주기<br>

    <hr>
    <h1>1st 제목</h1>
    <h2>2nd 제목</h2>
    <h3>3rd 제목</h3>
    
    <hr>
    <h1>li 태그 활용</h1>
        <ol type="1">
            <!-- ol: order list -->
            <li>li 사용하면</li>
            <li>이렇게 순서 리스트</li>
        </ol>

    <hr>   
    <h1>ul 태그 활용</h1>
        <ul>
            <li>이렇게 모양 리스트</li>    
            <li>ul 사용하면</li>
        </ul>
        
</body>
</html>
```

## 2. 실행 화면 

![](../.gitbook/assets/image%20%28402%29.png)

## 2. 이미지 불러오기 

비율을 유지하려면 width만 설

