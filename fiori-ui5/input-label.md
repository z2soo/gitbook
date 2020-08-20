---
description: Sap Demo Kit 사이트를 참고하여 input label 기능을 넣어본다.
---

# Input label

## 1. Input label

Sap Demo Kit 사이트에서 필요한 기능에 대한 부분을 가져와서 사용할 수 있다. 사이트에 들어가서 Sample에서 Label을 검색한다. 

{% embed url="https://sapui5.hana.ondemand.com/\#/controls" %}

![](../.gitbook/assets/image%20%28441%29.png)

![](../.gitbook/assets/image%20%28451%29.png)

 이 중 label with input을 눌러준다. download 옆 source 보  


![](../.gitbook/assets/image%20%28461%29.png)

![](../.gitbook/assets/image%20%28499%29.png)

이 중 두번째 단락 부분 복사

```markup
		<Label
			text="Label B (bold)"
			labelFor="input-b"
			design="Bold" />
		<Input id="input-b" />
```

이전에 만든 project1의 view1에 들어가서 넣어주기

![](../.gitbook/assets/image%20%28448%29.png)

![](../.gitbook/assets/image%20%28491%29.png)

![](../.gitbook/assets/image%20%28470%29.png)

![](../.gitbook/assets/image%20%28501%29.png)







![](../.gitbook/assets/image%20%28471%29.png)

![](../.gitbook/assets/image%20%28472%29.png)

```markup
		<Input
			id="productInput"
			placeholder="Enter Product ..."
			showSuggestion="true"
			suggest=".onSuggest"
			suggestionItems="{/ProductCollection}" >
			<suggestionItems>
				<core:Item text="{Name}" />
			</suggestionItems>
		</Input>
```

suggest=".onSuggest" 지우고 button 밑에 넣기

이때 Name은 FirstName으로 변경, suggestionItems="{/Employees}"로 변경, 즉 Employees entity에서 데이텉를 받아오겠다는 의미 

![](../.gitbook/assets/image%20%28406%29.png)

에러가 남; xmlns:core="sap.ui.core" 이 부분이 위에 설정되어 있지 않기 때문에 다음과 같이 넣어줌

![](../.gitbook/assets/image%20%28440%29.png)

//







![](../.gitbook/assets/image%20%28452%29.png)

```text
			<ComboBox
				showSecondaryValues= "true"
				items="{
					path: '/CountriesCollection',
					sorter: { path: 'text' }
				}">
				<core:ListItem key="{key}" text="{text}" additionalText = "{key}"/>
			</ComboBox>
```

input 밑에 view1에서 넣어줌

 바꿔

```text
						<ComboBox showSecondaryValues="true" items="{/Employees}" id="combo_empList" selectedKey="3">
							<core:ListItem key="{EmployeeID}" text="{FirstName}" additionalText="{key}"/>
```



![](../.gitbook/assets/image%20%28436%29.png)

![](../.gitbook/assets/image%20%28484%29.png)





//

새로운 view4 생성



table 추가 

![](../.gitbook/assets/image%20%28431%29.png)

데이터를 바인드 해줄 때는 해당 table에 통으로 하는 것이 아니라 table 아래의 template 에 해줘야지 됨! 중요하니 잘 기억하기/ 다음과 같이 세번째로 설정홰주기 

![](../.gitbook/assets/image%20%28464%29.png)

![](../.gitbook/assets/image%20%28458%29.png)

만들어진 테이블에 위와 같이 이름 및 format 변경 

view1으로 가서 이벤트에 view2가 아닌 4를 연결해주자

![](../.gitbook/assets/image%20%28413%29.png)

// 다이얼로그 추가



![](../.gitbook/assets/image%20%28408%29.png)

```markup

	
	
	onEscapePreventDialogPress: function () {
			if (!this.oEscapePreventDialog) {
				this.oEscapePreventDialog = new Dialog({
					title: "Dialog with prevent close",
					content: new Text({ text: "Try to close this Dialog with the Escape key" }),
					type: DialogType.Message,
					buttons: [
						new Button({
							text: "Simply close",
							press: function () {
								this.oEscapePreventDialog.close();
							}.bind(this)
						})
					],
					escapeHandler: function (oPromise) {
						if (!this.oConfirmEscapePreventDialog) {
							this.oConfirmEscapePreventDialog = new Dialog({
								title: "Are you sure?",
								content: new Text({ text: "Your unsaved changes will be lost" }),
								type: DialogType.Message,
								icon: IconPool.getIconURI("message-information"),
								buttons: [
									new Button({
										text: "Yes",
										press: function () {
											this.oConfirmEscapePreventDialog.close();
											oPromise.resolve();
										}.bind(this)
									}),
									new Button({
										text: "No",
										press: function () {
											this.oConfirmEscapePreventDialog.close();
											oPromise.reject();
										}.bind(this)
									})
								]
							});
						}

						this.oConfirmEscapePreventDialog.open();
					}.bind(this)
				});
			}

			this.oEscapePreventDialog.open();
		},
	
```

그냥 붙여 넣으면 library가 없어서 오류가 남, library define/import 해줘야 함, 그리고 function 안으로도 매개 변수도 순서대로 넣어줘야 함 

![](../.gitbook/assets/image%20%28412%29.png)

아직ing

///

![](../.gitbook/assets/image%20%28433%29.png)

message source controller 복사 , 위에는 매개변수 넣어줘여

```text
MessageBox.confirm("Approve purchase order 12345?");
```

![](../.gitbook/assets/image%20%28468%29.png)

//

message toast

//









