## Cauly Integration Guide For Banner

* Cauly Banner 광고 사용자 가이드
* version 4.1.0


#### 문서 이력
* 4.1.0 2015.01.29 초안 작성

#### 문서의 목적 및 범위
* 본 문서는 Cauly Banner 광고를 모바일 웹에서 사용하기 위한 Web SDK 가이드입니다. 

#### 개요
* Cauly 광고 형태 중 Banner 광고를 위한 SDK 입니다<br/>모바일 웹을 대상으로 합니다.
#### 절차
* http://www.cauly.net 에서 앱을 등록하고 app code를 발급받습니다


#### SDK Javascript link
* web sdk는 다음 주소를 사용 합니다.
 	- <pre>http://image.cauly.co.kr:15151/websdk/caulyad_4.1.0.js</pre>
+ 사용 방법
 	- ```<script src='http://image.cauly.co.kr:15151/websdk/caulyad_4.1.0.js' type='text/javascript'></script> ```
 	
#### Javascript 작성 방법
+ CaulyAd 변수 생성
- Cauly 광고를 사용하기 위해서CaulyAd 객체를 생성합니다.
- Paramter

	인자명|설명|필수
	---|---|---
	appcode|www.cauly.net 에서 발급 받은 app code|O
	options|추가적인 option (object 사용)<br/> 랜딩 시 새창 띄우는 방법<br/> open_new_window : true




+ 변수명은 caulyad로 설정
	- 변수의 이름이 caulyad가 아닐 경우 정상 동작하지 않을 수 있습니다.
+ 사용 예제
	```javascript
	var caulyad = {
			/*발급 ID */
			appcode : 'CAULY',
			/* 광고가 삽입될 div를 지정해주세요. */
			displayid : 'cauly_ad_area',
			/* callback function */
			nofill_callback : nofill_callback,
			success_callback : success_callback
	         
		}
	```


		인자명|설명|필수
		---|---|---
		success|광고 노출 성공시 호출될 callback|function success_callback() 형식|
		fail|광고 노출 실패시 호출될 callback<br/>function nofill_callback(code)형식<br/>인자값으로 결과code 전달<br/>0 : 정상처리<br/>100 : 광고 출력 시간이나 회수 등으로 노출 제한<br/>200 : 출력할 광고 없음<br/>400 : app code 오류. app이 등록되지 않았거나 사용이 불가능<br/>500 : server에서 오류 발생



 
* 사용 예제
	```javascript
	function success_callback( info ) {
		}
			
		function nofill_callback( retcode ) {
			/*   retcode 100 : non-chargeable ad */
			if ( retcode == '100' ) return true;
			
			/* 'return false'로 설정하면 광고가 표시되지 않습니다.  */
			return true;
		}
	```

* 작성 예제 1 (기본 사용 방법)
	```javascript
	<script src='http://image.cauly.co.kr:15151/websdk/caulyad_4.1.0.js' type='text/javascript'></script>
	<script type='text/javascript'>
	
		function success_callback( info ) {
		}
			
		function nofill_callback( retcode ) {
			/*   retcode 100 : non-chargeable ad */
			if ( retcode == '100' ) return true;
			
			/* 'return false'로 설정하면 광고가 표시되지 않습니다.  */
			return true;
		}
	
		var caulyad = {
			/*발급 ID */
			appcode : 'CAULY',
			/* 광고가 삽입될 div를 지정해주세요. */
			displayid : 'cauly_ad_area',
			/* callback function */
			nofill_callback : nofill_callback,
			success_callback : success_callback
		}
	</script>
	
	<div id='cauly_ad_area'></div>
	```
