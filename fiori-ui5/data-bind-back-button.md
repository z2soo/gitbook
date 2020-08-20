# Data bind, Back button 설정

## 1. Project 생성 

SAP Cloud Cockpit 사이트에서 Neo 평가판 &gt; 서비스 부분으로 들어가면 다음과 같이 제공하는 서비스에 대해 확인할 수 있다. 이 중 SAP Web IDE를 클릭해서 들어간다. 

![SAP CLOUD COCKPIT &amp;gt; NEO &#xD3C9;&#xAC00;&#xD310;](../.gitbook/assets/image%20%28446%29.png)

하단에 위치한 서비스로 이동을 누른다. 

![WEB IDE &amp;gt; &#xC11C;&#xBE44;&#xC2A4;&#xB85C; &#xC774;&#xB3D9;](../.gitbook/assets/image%20%28437%29.png)

다음과 같은 화면이 나온다. 이 때, 상단 우측 work space를 통해 work space manage로 이동할 수 있다. 

![SAP WEB IDE FULL-STACK](../.gitbook/assets/image%20%28479%29.png)

![WORK SPACE MANAGER](../.gitbook/assets/image%20%28438%29.png)

새로운 work space를 생성할 수 있으며, 기존 work space 삭제 또한 가능하다. 우선 앞으로 사용할 work space를 z2soo 라는 이름으로 생성해주었다. 

![WORK SPACE MANAGER](../.gitbook/assets/image%20%28465%29.png)

다음으로 해당 work space로 들어가서 새로운 프로젝트를 생성해준다. 이 때, template을 활용해서 만들어 줄 것이기 때문에 다음과 같이 생성한다.

{% hint style="info" %}
Work Space &gt; New &gt; Project From Template 
{% endhint %}

![&#xB0B4; WORK SPACE &amp;lt; NEW &amp;lt; PROJECT FROM TEMPLATE](../.gitbook/assets/image%20%28495%29.png)

Template 설정에서는 가장 마지막 것을 클릭해주고, 나머지는 기존 default 값으로 진행한다. 

![TEMPLATE SELECTION](../.gitbook/assets/image%20%28482%29.png)

Project Name은  STUDYPROJECT01, App Description은 SAPSTUDY로 설정해주었다. 

![BASIC INFORMATION](../.gitbook/assets/image%20%28409%29.png)

![TEMPLATE CUSTOMIZATION](../.gitbook/assets/image%20%28444%29.png)

Project를 생성하면 다음과 같은 화면을 확인할 수 있다. 

![STUDYPROJECT01](../.gitbook/assets/image%20%28475%29.png)



## 2. View 생성 및  이동 버튼 생성 

### 1\)  View 생성 

생성된 프로젝트 좌특 툴바를 보면 자동적으로 생성된 파일을 확인할 수 있다. 이 중, view 부분은 사용자에게 보여지는 부분으로써 view 폴더 하위에 존재하는 view 파일과 동일한 명으로 controller 폴더 하위에도 자동적으로 생성되어 존재하게 된다. 한 번 기존에 default로 생성된 view 외에 새로운 view를 만들어서 확인해보자. 

![default View&#xB9CC; &#xC874;&#xC7AC;&#xD558;&#xB294; &#xC0C1;&#xD0DC;](../.gitbook/assets/image%20%28417%29.png)

![&#xC0C8;&#xB85C;&#xC6B4; View2&#xB97C; &#xC0DD;&#xC131;&#xD55C; &#xC0C1;&#xD0DC;](../.gitbook/assets/image%20%28463%29.png)

생성된 View를 가지고 간단한 기능만 구현해보자. 우선 편집하려는 View 파일을  우클릭하여 Open Layout Editor로 열어준다. 그러면 코드가 아닌 툴바로 작업 가능한 화면이 나온다.

![View &amp;gt; &#xC6B0;&#xD074;&#xB9AD; &amp;gt; Open Layout Editor](../.gitbook/assets/image%20%28418%29.png)

![Open Layout Editor&#xB85C; &#xC5F4;&#xC5B4;&#xBCF8; View ](../.gitbook/assets/image%20%28434%29.png)



### 2\) Label 입력 

Label을 추가해서 Hello world! 를 입력하고, 제대로 실행되는지 확인해본다. 

![View1.xml](../.gitbook/assets/image%20%28449%29.png)

실행시 다음과 같은 화면이 나온다면 제대로 연결되었으니 계속 진행한다.  

![View1.xml &#xC2E4;&#xD589; &#xD654;&#xBA74;](../.gitbook/assets/image%20%28424%29.png)



### 3\) 이동 버튼 생성 

{% hint style="info" %}
버튼 생성 &gt; Properties &gt; Icon action 추가 &gt; Event &gt; Press &gt; Navigate to  설정 
{% endhint %}

우선 버튼을 하나 넣어주고, 해당 버튼을 누른 상태에서 우측에 뜨는 설정 값 중 Icon을 클릭한다. 버튼을 누르면 다른 창으로 이동하는  action을 취하게끔 할 것이니 action icon을 추가해준다. 

![View1 &amp;gt; Button &amp;gt; Icon](../.gitbook/assets/image%20%28419%29.png)

원래 Button은 화살표 방향이 없었는데,  action을 추가함으로써 이동 의미의 화살표 icon이 추가되었다. 

![View1 &amp;gt; Button &amp;gt; Icon action](../.gitbook/assets/image%20%28445%29.png)

이동 버튼 클릭시 어디로 이동하는지 설정해줘야 한다. 해당 버튼 위에서 생성한 View2로 이동하게 생성해준다. 해당 버튼을 누르고 우측 설정 창 중 Event &gt; Press &gt; Navigate to 를 통해 설정해준다. 

![View1 &amp;gt; Button &amp;gt; Event &amp;gt; Navigate to](../.gitbook/assets/image%20%28469%29.png)

Navigate to 설정은 다음과 같이 View2로 설정해준다. 

![View1 &amp;gt; Button &amp;gt; Event &amp;gt; Navigate to View2&#xB85C; &#xC124;&#xC815;](../.gitbook/assets/image%20%28450%29.png)

실행하면 다음과 같이 버튼이 생성되고 클릭하면 View2 창으로 이동한다. 

![&#xC2E4;&#xD589;&#xCC3D;](../.gitbook/assets/image%20%28415%29.png)



## 3. 데이터 추가 및 모델 등록 

### 1\) URL 데이터 추가

{% hint style="info" %}
manifest.json 파일 &gt; Data source &gt; 추가 버튼 + &gt; 데이터 정보 입력 
{% endhint %}

manifest.json 파일의 Data source 탭으로 이동해서 추가 버튼을 눌러주면 팝업 창이 뜬다. 

![manifest.json &amp;gt; Data source &amp;gt; + ](../.gitbook/assets/image%20%28493%29.png)

지금은 URL 주소를 활용해서 데이터를 가져올 것이기 때문에 Service URL을 선택해주고, create a new data source를 클릭한다. 

![manifest.json &amp;gt; Data source &amp;gt; + ](../.gitbook/assets/image%20%28497%29.png)

create a new data source를 클릭하면 다음과 같은 팝업창이 뜬다. 이용자 메일과 비밀번호를 입력해주고, oData 이름 설정 및 바인드 하고자 하는 데이터의 URL을 입력해준다. URL을 통해 데이터를 가져올 것이기 떄문에 Procy Type은 Internet 그대로 둔다. 

![URL &#xC0AC;&#xC6A9;&#xD55C; data bind &#xB4F1;&#xB85D;](../.gitbook/assets/image%20%28411%29.png)

아래와 같은 화면이 나오면 등록이 완료되었다. 

![URL &#xC0AC;&#xC6A9;&#xD55C; data bind &#xC644;&#xB8CC;](../.gitbook/assets/image%20%28425%29.png)



### 2\) 데이터 연결 확인 

URL 데이터 연결이 잘 되었는지 확인을 위해서는  SAP Cockpit neo 평가판 초기화면 &gt; 연결 &gt; 대상으로 들어가서 확인 가능하다. 해당 연결 대상 옆에 보이는 아이콘 중 네번째 아이콘을 누르면 된다.

{% hint style="info" %}
SAP Cockpit neo 평가판 화면 &gt; 연결 &gt; 대상 &gt; 적합한지 확인 
{% endhint %}

![AP Cockpit neo &#xD3C9;&#xAC00;&#xD310; &#xD654;&#xBA74; &amp;gt; &#xC5F0;&#xACB0; &amp;gt; &#xB300;&#xC0C1; &amp;gt; &#xC801;&#xD569;&#xD55C;&#xC9C0; &#xD655;&#xC778;](../.gitbook/assets/image%20%28481%29.png)

연결이 정상적으로 되었다면 다음과 같이 확인 가능하다. 

![&#xC5F0;&#xACB0; &#xD655;&#xC778; ](../.gitbook/assets/image%20%28439%29.png)



### 3\) 데이터 모델 확인 

{% hint style="info" %}
manifest.json &gt; Models
{% endhint %}

연결이 성공적으로 되었으면, 아까 create a new data source 클릭한 창으로 다시 돌아가보자. 아까 연결시킨 oData가 뜨면, relative URL에 다음의 주소\(/V2/Northwind/Northwind.svc/\)를 추가한 후, 다수의 entity set이 들어있는 oData임을 확인할 수 있다면 next를 눌러 저장한다.

![manifest.json &amp;gt; Data source &amp;gt; + ](../.gitbook/assets/image%20%28456%29.png)

![manifest.json &amp;gt; Data source &amp;gt; + ](../.gitbook/assets/image%20%28480%29.png)

manifest.json 파일의 models 탭을 들어가보면, 데이터 모델이 default 이름으로 등록이 된 것을 확인할 수 있다. 이제 해당 프로젝트에서 데이터를 바인드할 수 있다. 

![manifest.json &amp;gt; Models](../.gitbook/assets/image%20%28483%29.png)

![manifest.json &amp;gt; Models](../.gitbook/assets/image%20%28430%29.png)



## 4. 데이터 Bind

### 1\) 리스트 Bind

{% hint style="info" %}
리스트 &gt; Entity Set &gt; 선
{% endhint %}

프로젝트를 하다보면 리스트 control을 가장 많이 쓰게 될 것이다. List control에 데이터를 바인드해보도록한다. 우선, View1 화면에 control list 중 일반 List를 선택해서 가져온다. 단, 위에서 선행한 데이터 추가 과정이 완료된 상태여야 한다. 

![View1 &amp;gt; List &#xCD94;&#xAC00;](../.gitbook/assets/image%20%28500%29.png)

리스트를 바인딩하는 방법은 다양하게 존재한다. 지금은 우선 한 가지 방법을 살펴본다.  

우측 Entity set이 데이터를 바인딩하는 부분이다. 클릭하면 모델에 등록된 데이터 entity들이 쭉 뜨고, 원하는 데이터 entity를 찾아 bind해주면 된다. 

![Entity set &amp;gt; data bind](../.gitbook/assets/image%20%28416%29.png)

모델에 등록된 데이터 entity 중 employee 누르고 bind를 해주었다. 

![Entity set &amp;gt; data bind](../.gitbook/assets/image%20%28490%29.png)

 여기까지 저장하고 실행하면 View1 화면에서 다음을 확인할 수 있다. 

![View1 &#xC2E4;&#xD589;&#xD654;&#xBA74;](../.gitbook/assets/image%20%28488%29.png)



### 2\) Bind 포멧 설정 

employ 데이터를 바인드 해주었지만, 실제 row별로 어떤 데이터가 뜨는지 원하는 포멧으 확인하고자 한다. View1에서 List 클릭시 뜨는 우측 설정 중 Title을 클릭하면 다음과 같은 창이 뜬다. 

![View1 &amp;gt; List &amp;gt; Title](../.gitbook/assets/image%20%28498%29.png)

바인드 하려는 영역이 Title이며, First 이름과 Last 이름으로 합쳐 띄우고 싶어 다음과 같이 설정했다. 

![View1 &amp;gt; List &amp;gt; Title](../.gitbook/assets/image%20%28421%29.png)

마찬가지로 Description 부분도 employee ID와 주소를 합쳐 띄우게 설정했다. 

![View1 &amp;gt; List &amp;gt; Description](../.gitbook/assets/image%20%28476%29.png)

보여지는 아이콘 또한 연관성 있어 보이는  것으로 설정해주었다. 

![View1 &amp;gt; List &amp;gt; Icon](../.gitbook/assets/image%20%28429%29.png)



### 3\) 다른 View로 데이터 넘기기 

지금까지는 View1 리스트에 데이터를 바인드했다. 그러나 View1 뿐 아니라 View2에서도 해당 데이터를 확인하고 싶다. View1에 뜨는 데이터 리스트 중 하나를 클릭했을 때, 그 정보를 View2에서 확인할 수 있도록 이 동 및 데이터 바인드를 설정하고자 한다. 

기존에는 Navigate to 를 통해 경로만 적어주면 됬지만, 데이터 바인딩이 되어있는 부분을 navigate to 하면 이제 이 데이터 정보도 넘길 것인지에 대한 설정도 해줘야 한다. 

데이터 바인드가 되어 있는 List의 Event로 가서 Press &gt; Navigate to 설정을 한다.  

![View1 &amp;gt; Event &amp;gt; Press](../.gitbook/assets/image%20%28447%29.png)

가장 상단의 Data Binding 설정을 none이 아닌 Propagate current context 로 설정해준다.  

![View1 &amp;gt; Event &amp;gt; Press &amp;gt; Navigate to ](../.gitbook/assets/image%20%28467%29.png)

실행 결과 다음과 같이 View2에서 View1에서 클릭한 데이터의 상세 정보를 확인할 수 있게 되었다. 

![View1 &#xC2E4;&#xD589;&#xD654;&#xBA74;](../.gitbook/assets/image%20%28478%29.png)

![View2 &#xC2E4;&#xD589;&#xD654;&#xBA74;](../.gitbook/assets/image%20%28442%29.png)



### 4\) 뒤로가기 버튼 생성 

{% hint style="info" %}
페이지 &gt; Properties &gt; Show Nav Button True 설정 &gt; ID 확인 &gt; Event &gt; Press &gt; Navigate To 설정 
{% endhint %}

화면 이동 및 데이터 바인드를 완료했지만, View2 페이지에서 뒤로가기 기능이 없어 불편한 상태이다. 뒤로가기 버튼을 만들기 위해, 대상 페이지 View2 &gt; 우측 설정 &gt;  Properties &gt; Show Nav Button 설정을  True로 해준다. 여기까지 저장하고 실행하면 버튼은 보이지만 뒤로가기가 정상적으로 작동하지는 않을 것이다. 

![View2 &amp;gt; Properties &amp;gt; Show Nav Button True &#xC124;&#xC815;](../.gitbook/assets/image%20%28486%29.png)

그 이유는 버튼을 만듦과 동시에 해당 값에 default로 생성되는 View ID와 script code에 생성되는 ID가 다르기 떄문이다. 따라서 manifest,json 파일의 Routing 탭 하단 Routes 설정에서 View ID로 떠있는 값을 지워준다. 스크립트 값과 ID 값을 동일하게 맞추거나 하나를 지워주면 문제가 해결되기 때문! 이 부분을 하지 않으면 아래 Navigate To 연결을 하려 해도 정상적인 Target Control이 뜨지 않는다. 

![manifest.json &amp;gt; Routing &amp;gt; Routes &#xC124;&#xC815; ](../.gitbook/assets/image%20%28496%29.png)

그 다음 View2의 Event &gt; Press &gt; Navigate To를 이전 페이지인 View1으로 설정해준다. 

![View2 &amp;gt; Event &amp;gt; Press &amp;gt; Navigate To](../.gitbook/assets/image%20%28462%29.png)

그 결과  View1에서 원하는 형태로 포맷된 데이터를 확인하고, 클릭시 해당 데이터 description을 원하는 형태로 포맷된 상태로 View2에서 확인할 수 있으며, 뒤로가기 버튼 또한 정상적으로 작동한다. 

![View1 &#xC2E4;&#xD589;&#xD654;&#xBA74;](../.gitbook/assets/image%20%28485%29.png)

![View2 &#xC2E4;&#xD589;&#xD654;&#xBA74; ](../.gitbook/assets/image%20%28443%29.png)



