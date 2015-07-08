## Cauly Integration Guide For Floating popup

* Cauly Floating Popup 광고 사용자 가이드
* version 1.0.0


#### 문서 이력
* 1.0.0 2014.07.14 초안 작성

#### 문서의 목적 및 범위
* 본 문서는 Cauly Floating Popup 광고를 모바일 웹에서 사용하기 위한 Web SDK 가이드입니다.


#### 개요
* Cauly 광고 형태 중 Floating Popup 광고를 위한 SDK 입니다.<br/>모바일 웹을 대상으로 합니다.

#### 절차
* http://www.cauly.net 에서 앱을 등록하고 app code를 발급받습니다.

#### SDK Javascript link
+ web sdk는 다음 주소를 사용 합니다.
	- http://image.cauly.co.kr:15151/websdk/caulyad.popup.js
+ 사용 방법
	 - ```<script type="text/javascript" src="http://image.cauly.co.kr:15151/websdk/caulyad.popup.js"> </script>```

+ Javascript 작성 방법
	- CaulyPopupAd 변수 생성
		- Cauly 광고를 사용하기 위해서CaulyPopupAd 객체를 생성합니다.
		- Paramter

			인자명|설명|필수
			---|---|---
			appcode|www.cauly.net 에서 발급 받은 app code|O
			options|추가적인 option (object 사용)<br/>charset : 사용하는 charater set (default : “UTF-8”)|
		- 변수명은 caulyPopupAd로 설정
			- 변수의 이름이 caulyPopupAd가 아닐 경우 정상 동작하지 않을 수 있습니다.
			
		- 사용 예제
			```javascript 
			var caulyPopupAd = new CaulyPopupAd(“appcode”, {charset : “UTF-8”});
			```

	- showPopupAd 함수 호출
		- 변수를 생성하고 showPopupAd 함수를 호출하면 광고 정보를 조회하고 화면에 출력합니다.
		- showPopupAd(options)
		- Parameter 
			- options는 object로 전달되며 optional 입니다.
			- object에는 다음과 같은 내용이 가능합니다.
			
			인자명|설명|필수
			---|---|---
			top|광고 출력시 상단에서 얼마만큼 떨어져서 구동할지 정하는 옵션<br/>광고 top offset (default : 0)<br/>최대 100 (100 이상은 무시됨)|
			success|광고 노출 성공시 호출될 callback<br/>function success() 형식|
			fail| 광고 노출 실패시 호출될 <br/>callback 인자값으로 결과code 전달 <br/>0 : 정상처리 <br/>100 : 광고 출력 시간이나 회수등으로 노출제한 <br/>200 : 출력할 광고 없음 <br/>400 : app code 오류. app이 등록되지 않았거나 사용이 불가능 <br/>500 : server에서 오류 발생<br/>|
 
		- 사용 예제
			```javascript
			function onSuccess() {
					// 성공시 처리할 내용
				}
			
				function onFail() {
						// 실패시 처리할 내용 
			}
			
			caulyPopupAd.showPopupAd({top : 90, success : onSuccess, fail : onFail});
			```

	+ 작성 예제 1 (기본 사용 방법)
		```javascript
		<script type="text/javascript"
		 src="http://image.cauly.co.kr:15151/websdk/caulyad.popup.js">
		</script>
		<script type="text/javascript">
			// appcode는 발급받은 app code
			var caulyPopupAd = new CaulyPopupAd(“appcode”); 
			
			caulyPopupAd.showPopupAd();
		</script>
		```
	* 작성 예제 2  (상단 특정 Pixel 확보)
		```javascript
		<script type="text/javascript"
		 src="http://image.cauly.co.kr:15151/websdk/caulyad.popup.js">
		</script>
		<script type="text/javascript">
			// appcode는 발급받은 app code
			var caulyPopupAd = new CaulyPopupAd(“appcode”); 
			
			// 광고가 top offset 100 이상이 되도록 함.
			// 단, 최대값은 100
			caulyPopupAd.showPopupAd({top : 100});
		</script>
		```
	* 작성 예제 3 (callback 사용)
		```javascript
		<script type="text/javascript"
		 src="http://image.cauly.co.kr:15151/websdk/caulyad.popup.js">
		</script>
		<script type="text/javascript">
			function onSuccess(info) {
				// 성공시 처리할 내용
			}
			function onFail(retcode) {
				// 실패시 처리할 내용
		}
		
			// appcode는 발급받은 app code
			var caulyPopupAd = new CaulyPopupAd(“appcode”); 
			
			caulyPopupAd.showPopupAd({success : onSuccess, fail : onFail});
		</script>
		```

* [sample](http://showcase.cauly.net/floating/index.html )
