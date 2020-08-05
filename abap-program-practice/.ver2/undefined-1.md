# 툴바 버튼 및 이벤트 추가

### 툴바 버튼 추가 

LCL\_EVENT\_RECEIVER CLASS에서 HANDLE\_TOOLBAR을 추가해준다. \(Definition, Implementation\)

![CLASS &amp;gt; LCL\_EVENT\_RECEIVER &amp;gt; HANDLE\_TOOLBAR &#xCD94;&#xAC00;](../../.gitbook/assets/image%20%28265%29.png)

Implementation에서 다음과 같은 perform, HANDLE\_TOOLBAR 을 작성해준다. 

![Perform &amp;gt; HANDLE\_TOOLBAR](../../.gitbook/assets/image%20%28280%29.png)

### 이벤트?

![CLASS &amp;gt; HANDLE\_USER\_COMMAND &#xCD94;&#xAC00; : Definition](../../.gitbook/assets/image%20%28263%29.png)

![CLASS &amp;gt; HANDLE\_USER\_COMMAND &#xCD94;&#xAC00; : Implementation](../../.gitbook/assets/image%20%28279%29.png)

![CLASS &amp;gt; HANDLE\_USER\_COMMAND](../../.gitbook/assets/image%20%28285%29.png)

잊지 말고 EVENT 선언해주

![](../../.gitbook/assets/image%20%28304%29.png)

결과



![](../../.gitbook/assets/image%20%28291%29.png)

사원등록 누르면 ㄷㅏ음과 같이 데이터가 추가된다. 

![](../../.gitbook/assets/image%20%28298%29.png)

## 2. 사원 등록시 설정

사원등록시 사번이 없으면 새로 생성, 있으면 내부 데이터 가져와서 변경으로 하는 등 기타 설정을 해준다. 

SCREEN 0100 &gt; USE\_COMMAND\_0100 &gt; SAVE\_DATA Perform 생

![Screen 0100 &amp;gt; USER\_COMMAND\_0100](../../.gitbook/assets/image%20%28269%29.png)



### 변경 데이터가 없는 경우

![](../../.gitbook/assets/image%20%28267%29.png)

