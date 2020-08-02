---
description: 컴퓨터는 어떻게 작동하는가?
---

# How computer works?

## 1. 데이터의 형식과 구현

영화 'The Imitation Game'은 Turing Test라고도 하는 실제 용어로써, 영화는 컴퓨터 개념을 수학적으로 정립한 인물에 대한 내용이다. 컴퓨터로 데이터를 처리하기 위해서는 이진법을 통해, 문자를 코딩이라는 과정을 통해 표현해야 한다. 따라서, 액션을 취하기 전에 우선 데이터를 표현하는 과정이 우선시되며 중요하다. 메신저를 예를 들면, 데이터의 형태\(format\)는 txt, emoji, mp3, jpeg, mov, presence, HTML, css, material 등으로 표현되고, 이러한 데이터를 가지고 구현 방식은 messaging, mpbile push, VoLP, streaming, OAuth, react native, graphDB, Hbase, AI, openstack Cloud 등이 있다. 

#### 컴퓨터를 경험적으로 정의하면?

intelligence, smart 두 단어가 공통적으로 등장한다. IoT는 사물에 intelligence\(인지, 지능\)가 없는 것에 이를 붙이는 것으로 이해하면 된다. 

### 1\) Coding이란?

* encoding : 컴퓨터의 규약에 맞춰 다양한 형식으로 데이터를 맞추는 것
* decoding : encoding의 반대
* transcoding : encoding 되어 있는 데이터를 다른 형식으로 변환하는 것

예전에는 파일 형식이 다른 경우 encoder, decoder 일명 CODEC\(coding + decoding\) 프로그램이 없으면 다른 형식의 파일을 열지 못했다. 즉, 해당 데이터를 만든 회사에서만 그 데이터를 열어볼 수 있었는데, 이를 해결하기 위해 여러 디코더를 설치해야만 했고, 곰플레이어가 다수의 디코더를 가지고 비디오 파일을 열어주는 대표적인 프로그램이었다 그러나 최근에는 모두 동일한 형식의 파일을 가지기 때문에 별도의 인코더, 디코더 프로그램 설치가 불필요하다.

### 

### 2\) 게임

* FPS : First Person Shooting
* MMO : Massivey Mulriplayer Online

게임에는 대표적으로 위와 같은 종류가 있다. 그 중 MMO는 내가 취한 동작이 상대방에게도 같이 업데이트가 되어야 함. 그리고 사실상 모바일 게임의 경우 인풋은 터치. 따라서 그래픽 처리가 다수임. Graphics Engine, Unity, Unreal 과 같은 작업을 하게 됨. 

### 

### 3\) 결제

* OLTP : Online Transaction Processing
* OLAP : Online Analytical Processing 

상품을 판매하지 않는 기업이란 없다. 따라서 모든 사업에는 결제가 이루어지는데, 최근에는 개인적인 결제가 손쉽다. 이러한 payment 처리를 OLTP, Online Transaction Processing로 처리하는데, 이 때의 transaction은 더이상 쪼갤 수 없는 최소 단위의 데이터의 이동이다. 위에 언급한 MMO 게임에서 내가 상대의 캐릭터에 영향을 주면 바로 상대 캐릭터가 영향을 받는 것, 결제 내역이 쌍방향으로 바로 이루어지는 것 등이 이에 속한다. 가끔 SNS에서 업로드한 글이 바로 업데이트 되지 않는 경우는 transaction이 이루어지지 않은 경우라 볼 수 있다. 만약, 결제 시에 오류가 나서 결제 취소가 되는 경우는 roll back이라 말할 수 있다. \(반대로 마케팅을 시행하는 것 등은 roll up이라 함\) 

CRM, customer relationship management과 같이 고객에 대한 데이터를 가지고 분석을 하는 것은 OLAP, Online Analytical Processing로 처리된다. 주로 지속적인 구매, 고객유치 등을 알아내기 위해 사용된다.

### 

### 4\) 위치

* GPS Coordinates : Global Positioning System
* GIS : Geographic Information System
* WPS : WiFi Positioning System
* IoT : Internet of Things

WPS 데이터는 모든 지역의 와이파이를 잡아 해당 와이파이 위치를 파악하는 것으로 GPS보다 오차가 적은 장점이 있다. 최근에는 통신사 데이터를 통해서도 위치 데이터를 확보한다. 

### 

### 5\) 인지

* Radar : Radio Detection and Ranging
* LIDAR : Light Detection and Ranging

카메라, 전파 등을 통해서 주위에 어떤 사물이 있는지를 확인하는 방식으로 이러한 데이터를 가지고 자동차에 intelligence를 부여한 것이 바로 자율주행 자량이다. 

### 

### 6\) 스트리밍

* Live Streaming
* CDN : Contents Delivery Network

비디오를 스트리밍 데이터라고 하는 것은 이전부터 있었다. 최근에는 데이터 스트리밍이라고도 하는데, 온도와 미세먼지의 지속적인 변화를 측정하는 것과 같이 지속적으로 데이터가 나오는 것을 데이터 스트리밍이라고 한다. 이러한 스트리밍 데이터는 transcoding이 중요하다. 일명 서버가 터진다고 하는 경우를 방지하기 위해 사용하는 것이 CDN이다. 컨텐츠를 cash화 해두고 접속자에게 빠르게 서비스를 제공화 해주는 것을 의미한다. 이는 단순하게 스트리밍 데이터에 한정된 것이 아닌 모든 컨텐츠에 해당된다. 

### 

### 7\) 이미지

* Image Detection
* Deep Learning
* CNN : Convolutional Neural Network

이미지를 인식하고 학습을 통해서 구별해내는 것이 최근 주목받는 AI 빅데이터 중 가장 성과를 보이고 있는 부분이다. 이를 위해 사용되는 알고리즘이 바로 CNN이다. 

### 

### 8\) 브라우저

* HTML : Hyper Text Markup Language
* CSS : Cascading Style Sheets
* JavaScripts
* HTTP2 : Hyper Text Transfer Protocol v2

예전에는 PC에 많은 프로그램을 설치했지만, 최근에는 추가적인 프로그램을 많이 설치하지 않는다. 그 이유로 첫번째로 windows에서 기본으로 제공되는 프로그램이 많아졌기 때문이며, 두번째로 웹\(브라우저\)에서 해당 기능 수행이 가능해졌기 때문이다. 이는 데이터의 format이 표준화되어 웹에서 처리가 가능해진 것이다. 이전에는 PC 개발자가 있었다면, 최근에는 웹 개발자가 있는 것이 이러한 변화를 단편적으로 보여준다.  

* HTML : 인터넷 상의 페이지\(주소\)로 이동하는 것
* CSS : 컨텐츠가 보여지는 일종의 style을 설정하는 것 \(style, cotents가 분리되어 있음\)
* JavaScripts : input 값에 대한 처리를 해주는 것

즉, 위 세 가지를 통해 서버에서 정보를 받아서 동적 브라우저로 보여준다. 이처럼 최근에는 개발도 웹 상에서 진행된다.

HTML 상태 브라우저에 새로운 댓글을 달면 전체 페이지가 다시 로드\(다시 HTML을 열음\)해야 업데이트 되었다면, 최근에는 AJAX\(JavaScripts\)를 통해 특정 부분만을 업데이트 된다. 

### 

### 9\) 메일

* MIME : Multipurpose Internet Mail Extensions
* SMTP : Simple Mail Transfer Protocol
* POP3 : Post Office Protocol v3
* IMAP4 : Internet Message Access Protocol v4ㅇ

### 

### 10\) 달력

* ICS : Industrial Control System

ICS 형식으로 하면 일정 공유가 가능해지며, iCalendar가 대표적이다.  

### 

### 11\) 기타

* AJAX : Asynchronous JavaScripts and XML
* CSV : Comma Seperated Values
* JSON : JavaScript Object Notation
* YAML : Ain't Markuo Language
* SAML : Security Assertion Markup Language
* BI : Business Intelligence
* CMS : Contents Management System
* LMS : Learning Management System



## 2. 컴퓨터란?

### Turing test

Turing Test 혹 Imitation Game이란 컴퓨터 초기 개념에 대한 실험을 말한다. 컴퓨터에 대한 학문적인 기초를 처음 정립한 사람이 바로 Turing이기 떄문에 turing이라 부른다. 이를 실행하기 위해 turing machine을 구현하였으며, 당시는 반도체가 없었기 때문에 종이로 이러한 기계적 장치를 만들었다. 그리고 turing machine을 통해 input에 대해 output을 얻을 수 있게 된다면 이를 complete turing이라고 한다. 

![https://searchenterpriseai.techtarget.com/definition/Turing-test](../.gitbook/assets/image%20%28222%29.png)

![https://www.how2shout.com/what-is/what-is-turing-test-and-it-used-for.html](../.gitbook/assets/image%20%28220%29.png)

![https://en.wikipedia.org/wiki/Turing\_machine\_gallery](../.gitbook/assets/image%20%28216%29.png)



### Von Neumann Architecture

이후에 Von Neumann이라는 사람이 컴퓨터에 대한 장치적인 architecture를 처음 정립하였다. 이후 새로운 컴퓨터를 정립하고자 하는 시도도 있었지만 현재도 이와 같은 architecture를 사용한다. 이렇게 정립된 컴퓨터를 사용하기 위해 8086 Instruction Set이 가장 기초적으로 사용된다. 

![https://www.computerscience.gcse.guru/theory/von-neumann-architecture](../.gitbook/assets/image%20%28223%29.png)

![http://mayurkalablogs.blogspot.com/2012/02/8086-instruction-set.html](../.gitbook/assets/image%20%28218%29.png)



### Abstraction Layer & Layered Thinking

컴퓨터의 동작 과정은 사실상 input에 대해 output을 뽑아내는 것이 중요하며, 이를 위해서는 abstraction과 layered thinking 과정이 중요하다. CPU와 같은 하드웨어를 추상화, 제어, 명령하는 일을 하는 것이 Operation System\(OS\), 운영체제이다.

![http://prex.sourceforge.net/doc/hal.html](../.gitbook/assets/image%20%28219%29.png)

![https://www.pinterest.co.kr/pin/119767671310939805/](../.gitbook/assets/image%20%28217%29.png)



### API : Application Programming Interface

input을 넣었을 때 output을 나오게끔 프로그래밍을 하되 프로그램들이 서로 상호작용하도록 작업하는 것이 바로 API이다. 가게라고 생각하면, API는 손님\(프로그램\)이 주문할 수 있게 메뉴\(명령 목록\)를 정리하고, 주문\(명령\)을 받으면 요리사\(응용프로그램\)와 상호작용하여 요청된 메뉴\(명령에 대한 값\)를 전달한다. 

컴퓨터 관련하여 다양한 것들이 있지만, 정말 단순하게 보면 input에 대해 output을 주는 것! 어떤 방식으로 그것을 수행하는지에 대한 기술의 차이일 뿐이라고 생각한다. 

![http://blog.wishket.com/api%EB%9E%80-%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85-%EA%B7%B8%EB%A6%B0%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8/ ](../.gitbook/assets/image%20%28221%29.png)

### 

### 미래의 컴퓨터 기술

> 미래 컴퓨터는 웨어러블 기계를 비롯해 VR 기술 등과 결합될 것이라고 보며, 이에 대한 다양한 활용에 대한 영상 설명이다.

* 수리 [www.youtu.be/biNebig1gUI?t=43](https://www.youtu.be/biNebig1gUI?t=43)
* 게임 [www.youtu.be/29xnzxgCx6I?t=68](https://www.youtu.be/29xnzxgCx6I?t=68)
* 교육 [www.youtu.be/567Eb-Gccn8?t=41](https://www.youtu.be/567Eb-Gccn8?t=41)
* 교육 [www.youtu.be/uIHPPtPBgHk](https://www.youtu.be/uIHPPtPBgHk)

