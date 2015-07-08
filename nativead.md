## Cauly Integration Guide For NativeAd

* Cauly NativeAd 광고 사용자 가이드
* version 4.0.2


#### 문서 이력
* 4.0.2 2015.01.29 초안 작성

#### 문서의 목적 및 범위
* 본 문서는 Cauly NativeAd 광고를 모바일 웹에서 사용하기 위한 Web SDK 가이드입니다. 

#### 개요
* Cauly 광고 형태 중 NativeAd 광고를 위한 SDK 입니다.<br/>모바일 웹을 대상으로 합니다.

#### 절차
* http://www.cauly.net 에서 앱을 등록하고 app code를 발급받습니다.


#### SDK Javascript link
+  web sdk는 다음 주소를 사용 합니다.
	-   http://image.cauly.co.kr:15151/websdk/caulyad.native.js
+  사용 방법
	- ```<script src="http://image.cauly.co.kr:15151/websdk/caulyad.native.js"></script>```

#### 네이티브 디자인 DIV 삽입
- 아이콘, 메인이미지, 제목, 부제목, 상세설명 중 원하는 콘텐츠 선택하여 디자인

- 예제
	```html
	<!-- 원하시는 대로 디자인 가능  ,  5개의 콘텐츠 중, 원하는 디자인에 따라 골라 사용 가능 -->
	<div id="caulyNativeAd1" style="display:none;position:relative; width:300px; height:300px;">
	<img id="image" style="position:absolute; width:300px; height:150px;"></img>
	<img id="icon" style="position:absolute; top:10px; left:10px;width:50px; height:50px;"></img>
	<font color="red" size="3" id="title" style="position:absolute; top:10px; left:100px;width:200px; height:50px;" ></font>
	<font color="blue" size="1" id="subtitle" style="position:absolute; top:50px; left:100px;width:200px; height:50px;" ></font>
	<font color="white"  size="2"  id="description" style="position:absolute; top:80px; left:100px;width:200px;"></font>
	</div>
	```
#### NativeAd 변수 생성
* Cauly 광고를 사용하기 위해서 NativeAd 객체를 생성합니다.
* Paramter

	인자명|설명|필수
	--- | --- | ---
	appcode|www.cauly.net 에서 발급 받은 app code|O
	setTitleId |광고영역 중, 제목에 해당하는 ID 설정|
	setSubTitleId |광고영역 중, 부제목에 해당하는 ID|
	setDescriptionId|광고영역 중, 상세설명에 해당하는 ID 설정 |
	setImageId|광고영역 중, 메인이미지에 해당하는 ID 설정 |
	setIsImageLandscape|메인이미지가 가로인지, 세로인지 (true or false)|
	setIconId|광고영역 중, 아이콘에 해당하는 ID 설정|
	showNativeAd(appcode, fuction success, fuction fail)|광고영역 Div ID 설정, 광고 수신 성공 callback,광고 수신 실패 callback|





* 사용 예제
	```javascript
	var caulyNativeAd = new CaulyNativeAd("발급AppCode");
		caulyNativeAd.setTitleId("title"); 
		caulyNativeAd.setSubTitleId("subtitle"); 
		caulyNativeAd.setDescriptionId("description"); 
		caulyNativeAd.setIconId("icon");   
		caulyNativeAd.setImageId("image"); 	caulyNativeAd.setIsImageLandscape(true); 
		caulyNativeAd.showNativeAd("caulyNativeAd1", 
		function(onSuccess){
			document.getElementById("caulyNativeAd1").style.display = "block";
		},
		function(onFailed)  
		{
			document.getElementById("caulyNativeAd1").style.display = "none";
		});
	```



	
	인자명|설명|필수
	--- | --- | ---
	success|광고 노출 성공시 호출될 callback|
	fail| 광고 노출 실패시 호출될 <br/>callback 인자값으로 결과code 전달 <br/>0 : 정상처리 <br/>100 : 광고 출력 시간이나 회수등으로 노출제한 <br/>200 : 출력할 광고 없음 <br/>400 : app code 오류. app이 등록되지 않았거나 사용이 불가능 <br/>500 : server에서 오류 발생<br/>|
	


 






* 작성 예제 1 (기본 사용 방법)
	```javascript
	<script src="http://image.cauly.co.kr:15151/websdk/caulyad.native.js"></script>
	
	<script type="text/javascript">
	var caulyNativeAd = new CaulyNativeAd("발급AppCode");
	caulyNativeAd.setTitleId("title"); 
	caulyNativeAd.setSubTitleId("subtitle"); 
	caulyNativeAd.setDescriptionId("description"); 
	caulyNativeAd.setIconId("icon");   
	caulyNativeAd.setImageId("image");
	caulyNativeAd.setIsImageLandscape(true); 
	caulyNativeAd.showNativeAd("caulyNativeAd1", 
	function(onSuccess){
		document.getElementById("caulyNativeAd1").style.display = "block";
	},
	function(onFailed){
	document.getElementById("caulyNativeAd1").style.display = "none";
	});
	</script>
	
	<!-- 원하시는 대로 디자인 가능  ,  5개의 콘텐츠 중, 원하는 디자인에 따라 골라 사용 가능 -->
	<div id="caulyNativeAd1" style="display:none;position:relative; width:300px; height:300px;margin-left: 100px;">
		<img id="image" style="position:absolute; width:300px; height:150px;"></img>
		<img id="icon" style="position:absolute; top:10px; left:10px;width:50px; height:50px;"></img>
		<font color="red" size="3" id="title" style="position:absolute; top:10px; left:100px;width:200px; height:50px;" ></font>
		<font color="blue" size="1" id="subtitle" style="position:absolute; top:50px; left:100px;width:200px; height:50px;" ></font>
		<font color="white"  size="2"  id="description" style="position:absolute; top:80px; left:100px;width:200px;"></font>
	</div>
	```

[sample](http://image.cauly.co.kr:15151/richad/test/native_web/sample/joins.html)
 
####  주의 사항
+ HybridApp에서 web-sdk를 사용하는 경우,WebView의 setWebviewClient 의 shouldOverrideUrlLoading function에서
redirection을 처리하지 않아야 합니다.  

