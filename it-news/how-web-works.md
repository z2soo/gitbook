---
description: 웹은 어떻게 작동하는가?
---

# How web works?

## 1. Computing

컴퓨팅에는 분산 컴퓨팅과 병렬 컴퓨팅 두 종류가 있다. 

* **Distributed Computing** : 인터넷에 연결된 여러 컴퓨터들의 처리 능력을 이용하여 연산을 하는 방법
* **Parallel Computing** : 동시에 많은 계산을 하는 연산의 방법

![https://subscription.packtpub.com/book/application\_development/9781787126992/1/ch01lvl1sec10/parallel-versus-distributed-computing](../.gitbook/assets/image%20%28244%29.png)



## 2. Web Server & Web Browser \(1\)

### Web Server 

* web browser 같은 클라이언트로부터 HTTP 요청을 받아들이고, HTML 문서와 같은 웹 페이지를 반환하는 프로그램
* 위 언급한 기능을 제공하는 프로그램을 제공하는 컴퓨터 하드웨어



### Web Browser

* web server에서 이동하며 쌍방향으로 통신하고 HTML 문서나 파일을 출력하는 GUI 기반의 응용 소프트웨어 주요 브라우저로 구글 크롬, 인터넷 익스플로러, 파이어 폭스 등이 있음 



### 작동 원리

서버는 간단하게 4가지 단계로 작동된다.

1. 브라우저는 도메인 이름으로부터 IP 주소를 얻는다.
2. 브라우저가 서버에 full URL을 요청한다.
3. 서버가 요청에 응답하여 요청한 페이지를 보낸다.
4. 브라우저가 웹 페이지를 display 한다. 

![https://www.geeksforgeeks.org/web-servers-work/](../.gitbook/assets/image%20%28228%29.png)

![https://www.researchgate.net/figure/Dataaow-between-the-Browser-and-the-Web-Server-The-Browser-requests-the-webpage-from\_fig8\_271510079](../.gitbook/assets/image%20%28240%29.png)



## 3. Web Server & Web Browser \(2\)

web browser가 어떻게 구성되고 구현되는지 조금 더 알아보면, 전체적인 흐름은 다음과 같다.  

* Browser = Networking + Parsing + Rendering + Painting

![https://medium.com/@gneutzling/the-rendering-process-of-a-web-page-78e05a6749dc](../.gitbook/assets/image%20%28226%29.png)



### Parsing

* 언어학 : 문장을 이루고 있는 구성 성분을 분해하고, 그것들의 위계 관계를 분석하여 문장 구조를 결정하는 것
* 컴퓨터 과학 : 일련의 문자열을 의미있는 token\(어휘 분석의 단위\)으로 분해하고, 그것들로 이루어진 parse tree 생성

parsing은 한 마디로 어떤 문장을 분석하거나 문법적 관계를 해석하는 행위를 말한다. 예를 들어, 웹 브라우저 explorer 또한 하나의 응용 프로그램으로, XML parser가 parsing\(해석\)한 결과를 이용해 display하도록 프로그래밍이 되어 있다. parsing 기법으로는 SMI 파싱 기법 DOM과 SAX/JSON 파싱 기법이 있다.

parser는 parsing을 수행하는 processor이다. 즉, parsing을 수행하는 프로그램이자 compiler의 일부로 컴파일러나 인터프리터에서 원시 프로그램을 읽어들여 구문 분석을 행하는 프로그램이다. 

![https://tomassetti.me/guide-parsing-algorithms-terminology/](../.gitbook/assets/image%20%28229%29.png)



### Rendering

* 논리적인 문서의 표현식을 그래픽 표현식으로 변환시키는 과정

rendering의 과정은 크게 2단계를 거쳐 이루어진다. 일반적인 전체 흐름은 브라우저에 문서가 로딩 됨에 따라 DOM 트리의 구성이 진행되면, 레이아웃을 계산한 후 문서에 요소를 그린다. 

1. DOM 요소와 스타일에 기반을 둔 레이아웃 계산
2. 계산된 요소의 화면 표현

![HTTP &#xC694;&#xCCAD; &#xD6C4; &#xC751;&#xB2F5;&#xC744; &#xD1B5;&#xD575; &#xAD6C;&#xD604;&#xB418;&#xB294; &#xBE0C;&#xB77C;&#xC6B0;&#xC800; &#xCC98;&#xB9AC; &#xACFC;&#xC815; : https://12bme.tistory.com/140](../.gitbook/assets/image%20%28237%29.png)







### DOM tree

브라우저는 HTML 태그를 parsing하여 DOM tree를 구성한다. DOM은 데이터의 표현식으로 모든 HTML 태그에는 그에 상응하는 노드가 있으며, 태그 사이에는 텍스트 데이터가 포함될 수 있다. 각 태그는 태그 데이터의 표현식인 DOM 요소로 1:1로 대응해 표현되며, DOM 요소 노드는 트리 형태로 구성되기 때문에 DOM tree라고 부른다. 

![https://12bme.tistory.com/140](../.gitbook/assets/image%20%28227%29.png)



### Style structure

스타일 정보를 통해 스타일 구조체를 생성한다. 스타일 정보는 단계적으로 처리되며, 가장 마지막 단계의 스타일 정보가 이전 스타일보다 우선으로 적용된다. 스타일 정보는 다음과 같이 3단계로 나누어 처리된다. 

1. 브라우저에 포함된 기본 스타일 정보
2. 사용자 정의 스타일 정보 \(외부 파일 혹 내부 정의 스타일\)
3. HTML 태그에 style 속성을 사용해 기술되는 인라인 스타일 정보



### Render tree

DOM tree와 스타일 구조를 통해 render tree가 생성된다. 

render tree는 DOM tree와는 다르게 각 노드에 스타일 정보가 설정되어 있고, 화면에 표현되는 노드로 구성된다. 단, 스타일이 'display:none'으로 설정된 노드는 렌더 트리에 포함되지 않는다. 

DOM tree와 render tree의 노드는 서로 1:1 대응되지 않는다. DOM 트리의 구성원 중 일부 녿\(&lt;head&gt;, &lt;title&gt;, &lt;script&gt; 등\)는 화면에 표현되는 노드가 아니므로 DOM 트리의 구성원이지만, 렌더 트리의 구성원은 아니다. 또한, DOM 트리의 단일 구성원이지만, 렌더 트리에서는 여러 개의 노드로 구성되는 경우도 있다. &lt;br&gt; 태그로 읺 줄이 바뀌거나 노드 내에서 자연스럽게 줄이 바뀐 경우 등 단일 텍스트 노드가 여러 줄로 출력되는 경우가 여기에 해당한다.

렌더 트레에서 각 노드는 '프레임\(frame\)'이나 '박스\(box\)'로 불리며, CSS 박스 속성 정보가 있다. 

\[Rendering 설명 출처 : [https://12bme.tistory.com/140](https://12bme.tistory.com/140])[\]](https://12bme.tistory.com/140]) 



### Painting

렌더링 엔진이 요소가 어디에 표현되어야 할 지 알고 있는 상태에서, 렌더 트리를 순회하면서 페인트 함수를 호출해 노드를 화면에 표현하는 과정이다. 한 마디로 정보를 모두 모아 화면을 그리는 의미로 받아들였다.



### 종합

위에서 하나씩 다룬 개념들을 모두 모아서 조금 상세하게 브라우저 처리 과정을 살펴보자.

아래의 그림에서 DOM은 HTML을 파싱한 것, CSSOM은 CSS를 파싱한 것이다. 이 둘을 합쳐 Render Tree를 만든 후, Render Tree를 출력할 노드를 결정하고, 해당 노드의 스타일 값을 계산, 뷰 포트에서 노드가 가져야 할 정확한 위치와 크기를 계산 및 전부 절대값으로 paint 과정을 거쳐 화면에 출력하면 된다.

1. DOM 및 CSSOM 크리가 결합되어 rendering tree를 형성
2. rendering tree에는 페이지를 렌더링하는데 필요한 노드만 포함됨
3. 레이아웃은 각 객체의 정확한 위치 및 크기를 계산함
4. 마지막 단계는 최종 rendering tree에서 수행되는 paint로 픽셀을 화면에 렌더링함

![https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-tree-construction?hl=ko](../.gitbook/assets/image%20%28224%29.png)



## 4. Etc

### Router

둘 혹은 그 이상의 네트워크들 간 데이터 전송을 위해 최적 경로를 설정해주며, 데이터를 해당 경로를 따라 통신할 수 있도록하는 인터넷 접속 장비이다. 즉, 전화국과 비슷한 개념이다. 내부 네트워크를 사용하면 기종, 운영체제, 프로토콜 등을 확실하게 알 수 있어 네트워크 최적화가 가능하지만, 외부 네트워크와 연결할 때에는 그러한 정보를 알 수 없기 때문에 라우터를 사용한다. 

라우터는 다른 기종 간 네트워크를 연결하는 기능을 하기 때문에 여러 프로토콜에서 전송되는 packet\(통신망에서 주고 받는 메세지의 조각으로 데이터와 목적지 주소를 포함\)을 받아들여 가장 효율적인 경로로 보내며 흐름제어를 한다. 예를 들어 A 정보를 보내고자 한다면, 그 정보를 여러개 A1, A2, A3 .. 으로 쪼개 상대방 서버를 찾아가고 상대방에 붙은 라우터는 쪼개진 정보를 다시 A 모습으로 조합한다. 



### DNS : Domain Name System

네트워크에서 도메인이나 호스트 이름을 숫자로 된 IP 주소로 해석해주는 TCP/IP 네트워크 서비스이다. 

![https://aws.amazon.com/ko/route53/what-is-dns/](../.gitbook/assets/image%20%28245%29.png)



### load balancer

서버에 가해지는 부하\(=load\)를 분산시켜 밸런싱\(=balance\) 해주는 장치 또는 기술을 통칭한다. 클라이언트와 서버풀\(Server Pool, 분산 네트워크를 구성하는 서버들의 그룹\) 사이에 위차하며, 한 대의 서버로 부하가 집중되지 않도록 트래픽을 관리해 각각의 서버가 최적의 퍼폼너스를 보일 수 있도록 한다. 

![https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&amp;memberNo=2521903](../.gitbook/assets/image%20%28235%29.png)

이는 여러 대의 서버를 두고 서비스를 제공하는 분산 처리 시스템에서 필요한 기술이다. 서비스 제공 초기에 적은 수의 클라이언트 만이 있는 경우, 서버 한 대로 요청에 응답하는 것이 가능하다. 하지만 클라이언트 수가 늘어나게 되면 트레픽이 증가하기에 대처가 필요하다. 대처 방법으로는  두 가지가 있다. 만약, scale-out 방식으로 서버를 증설한다면, 여러 대의 서버로 트래픽을 균등하게 분산해주는 로드밸런싱이 필수적이다. 

* Scale-up : 서버 자체의 성능 확장
* Scale-out :  서버 갯수 증가, 증설

![https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&amp;memberNo=2521903](../.gitbook/assets/image%20%28241%29.png)

\[ Load balance 추가 설명 [https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903](https://post.naver.com/viewer/postView.nhn?volumeNo=27046347&memberNo=2521903) \]



### Hosting : web, server, cloud

호스팅 방법은 다양하게 존재하지만, 가장 많이 비교하는 것은 web, server, cloud 세 가지이다. 운영하는 서비스에 따라 호스팅 방법을 선택하면 되고, 그 외에도 서버 이용 방식, 관리 권한, 활용 등의 특징에 따라서 선택해도 된다. 

![http://library.gabia.com/contents/infrahosting/1311](../.gitbook/assets/image%20%28259%29.png)

![http://library.gabia.com/contents/infrahosting/1311](../.gitbook/assets/image%20%28254%29.png)

다양한 측면에서 차이를 보이는 호스팅 방법 중 필요에 따라 택하면 된다. 위에서 web server, browser를 다루었으니, web hosting에 대해 조금 더 알아보자. 

![https://medium.com/@eonian.social/static-vs-dynamic-websites-8e80d231bf86](../.gitbook/assets/image%20%28236%29.png)

Web hosting의 작동 원리는 위의 사진과 같다. 간단한 HTML 만을 서비스한다면 static web hosting, 동적 부분을 추가한다면 dynamic web hosting으로 구분된다. 

![https://medium.com/@eonian.social/static-vs-dynamic-websites-8e80d231bf86  ](../.gitbook/assets/image%20%28257%29.png)



