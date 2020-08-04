---
description: Web crawling과 연관한 용어에 대해 알아본다.
---

# Web crawling 용어

### 웹 크롤링

웹 페이지의 하이퍼링크를 순회하면서 웹 페이지를 다운로드하는 작업이다.



### 웹 스크레이핑

다운로드한 웹 페이지에서 필요한 콘텐츠를 추출하는 작업이다. 웹 페이지를 구성하고 있는 HTML 태그의 콘텐츠나 속성의 값을 읽는 작업을 말한다. 



### URL \(Uniform Resource Locator\)

컴퓨터 네트워크와 검색 메커니즘에서의 자원의 위치를 지정하는 문자열로써, 네트워크 상에서 자원이 어디 있는지를 알려주기 위한 규약이다. 



### URI \(Uniform Resource Identity\)

웹 사이트에 요청하고자 하는 대상의 패스정보와 파일명이다. 구성 파일명이 생략되면 디폴트로 index.html을 사용한다.



### HTTP \(HyperText Transfer Protocol\)

{% hint style="info" %}
* 프로토콜://계정:패스워드@호스트:포트번호/하위경로?질의조건\#색인
* http:// 도메인 이름 or ip 주소 : port 번호 / root context / sub context
{% endhint %}

* http://도메인 이름 혹은 ip 주소 : host 몇번 port에 저장할 것인지의 port 번호
* http는 port 번호 80이 default
* / : root context, 최상위 웹 자원 혹은 웹 컨텍스트, root context 안에 sub context 생성 가능

웹상에서 클라이언트와 서버 간에 정보를 주고받을 수 있는 통신 규약\(프로토콜\) URL 문자열을 직접 입력하거나, 하이퍼링크 텍스트\(Hyper text는 링크가 걸려 있는 문자를 의미한다. ex\) 이메일 주소\) 또는 이미지를 클릭하여 HTML 문서를 주고받는데 사용한다. 

디폴트로 80번 포트를 사용하며, 다른 포트 번호를 사용하는 웹 서버에 요청하는 경우에는 도메인명 뒤에 : 기호와 함께 포트 번호를 지정해준다.



### GET방식

아이디나 패스워드를 그대로 보내면 보안에 취약하기 때문에, 웹 자원을 가져오기 위해 설계된 방식이다. 브라우저에서 직접 요청하려는 페이지의 URL 문자열을 입력하여 요청 하이퍼링크가 설정된 텍스트나 이미지를 클릭하여 요청한다. Query 문자열 없는 요청과 Query 문자열을 추가한 요청 모두 가능하며, Query 문자열을 추가한 경우 URL 문자열 뒤에 query가 추가되어 전달된다.

### 

### POST방식

Query 문자열을 추가한 요청만 가능하다. Query 문자열이 요청 바디에 따로 담겨서 전달되므로 요청 URL 문자열에서는 볼 수 없다. 



### SNS, 소셜 네트워킹 서비스\(Social Networking Service\)

사용자 간의 자유로운 의사소통과 정보 공유, 인맥 확대 등을 통해 사회적 관계를 생성하고 강화해주는 온라인 플랫폼이다. 최근 스마트폰 이용자의 증가와 무선인터넷 서비스의 확장과 더불어 SNS의 이용자 또한 급증하고 있다.



### OPEN API 

인터넷 이용자가 웹 검색 결과 및 사용자 화면 등을 제공받는데 그치지 않고 직접 응용 프로그램과 서비스를 개발할 수 있도록 공개된 개발자를 위한 인터페이스이다. 대부분의 SNS 사이트들은 개발자로 등록하고 인증키를 받아 제공되는 API 사용한다.



### RSS\(Really Simple Syndication/Rich Site Summary\) 

뉴스나 블로그와 같이 콘텐츠 업데이트가 자주 일어나는 웹 사이트에서 업데이트된 정보를 정해진 규격의 XML 형식으로 자동화하여 사용자에게 제공하기 위한 서비스이다. RSS가 등장하기 전에는 원하는 정보를 얻기 위해 해당 사이트를 직접 방문해야 했다. RSS 관련 프로그램\(혹은 서비스\)을 이용하여 자동 수집이 가능해졌기 때문에, 사용자는 각각의 사이트 방문 없이 최신 정보들만 골라 한 자리에서 볼 수 있다. 

* 정적인 웹 페이지 기술 - HTML , CSS 
* 동적인 웹 페이지 기술 - JavaScript , Ajax
