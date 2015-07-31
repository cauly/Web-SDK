![Valid XHTML](http://cauly044.fsnsys.com:10010/images/logo_cauly_main.png) CAULY Video Mobile Web SDK 연동 가이드  
----

* CAULY Video 사용자 가이드
* version 4.0.2


#### 문서 이력
* 4.0.2 2015.07.31 초안 작성

#### 문서의 목적 및 범위
* 본 문서는  CAULY Video 를 모바일 웹에서 사용하기 위한 Web SDK 가이드입니다. 

#### 개요
* CAULY 광고 형태 중  CAULY Video를 위한 SDK 입니다.<br/>모바일 웹을 대상으로 합니다.

#### 절차
* <a href="http://cauly.net" target="_blank">Cauly</a> 에서 앱을 등록하고 app code를 발급받습니다.


#### SDK Javascript link
+  web sdk는 다음 주소를 사용 합니다. (not yet uploaded)
	-   http://image.cauly.co.kr:15151/websdk/.js
+  사용 방법
	- ```<script src="http://image.cauly.co.kr:15151/websdk/"></script>```

#### 네이티브 디자인 DIV 삽입
- 아이콘, 메인이미지, 제목, 부제목, 상세설명 중 원하는 콘텐츠 선택하여 디자인

- 예제
	```html
	<!--  CAULY Video가 노출 될 컨테이너 설정 -->
	<div class="ad-Cauly" id="caulyVideoAd" >   </div>
	```
#### CaulyVideoAd 변수 생성
*  CAULY Video를 사용하기 위해서 CaulyVideoAd 객체를 생성합니다.
* Paramter

	인자명|설명|필수
	--- | --- | ---
	appcode|<a href="http://cauly.net" target="_blank">Cauly</a> 에서 발급 받은 app code|O
  setKeywords	|광고 타켓팅에 활용되는 키워드 설정|
  setSkipCount	|광고의 건너띄우기 버튼의 노출시간설정|
	requestVideoAd(appcode, caulyVideoAdCallback)|광고영역 Div ID 설정, 광고 callback|
  showVideoAd()|수신된 광고를 재생시작 |

  광고Callback| 설명
  ---|---
  onReceiveVideoAd()	|광고 요청 성공 시 호출됨. 유,무료 광고 여부가 isChargeableAd 변수에 설정됨
  onFailToReceiveVideoAd( code, msg)	|광고 노출 실패 시 호출됨. 오류 코드와 내용이 errorCode, errorMsg 변수에 설정됨
  onStartVideoAd()	|광고의 재생시작을 알려준다.
  onFinishVideoAd()	| CAULY Video 재생 중, 재생완료, 광고클릭, 스킵버튼클릭, 플레이에러 등으로 광고영상이 끝났을 때 호출

* 사용 예제
	```javascript
	var videoAd ;
	var caulyVideoAdCallback =
	{
		onReceiveVideoAd		: onReceiveVideoAd,
		onFailToReceiveVideoAd  : onFailToReceiveVideoAd,
		onStartVideoAd   		: onStartVideoAd,
		onFinishVideoAd   		: onFinishVideoAd,
	}
	// CAULY Video를 없애고,   본 영상을 재생한다
	function loadVideo()
	{
		document.getElementById('caulyVideoAd').innerHTML="";
		document.getElementById('caulyVideoAd').style.display = "none";
		/*
		 Do what you want to do.
		*/
	}
	//광고수신에 성공되었을 때 호출된다.
	function onReceiveVideoAd(info)
	{
		videoAd.showVideoAd();
		setTimeout(function(){videoAd.play();}, 100);
		
	}
	//광고의 재생시작을 알려준다.
	function onStartVideoAd()
	{
	}
  // CAULY Video 재생 중, 재생완료, 광고클릭, 스킵버튼클릭, 플레이에러 등으로 광고영상이 끝났을 때 호출
	function onFinishVideoAd(code, msg)
	{
		loadVideo();
	}
	광고수신에 실패되었을 때 호출된다.
	function onFailToReceiveVideoAd(code,msg)
	{
		loadVideo();
	}
	//CaulyVideoAd를 호출한다. 
	function loadVideoAd()
	{
		videoAd = new CaulyVideoAd("APPCODE");
		videoAd.setKeywords("category");
		videoAd.requestVideoAd("caulyVideoAd", caulyVideoAdCallback);
	}
	loadVideoAd();
	```

[error 코드 정의](onFailToReceiveVideoAd)
		
Code|Message|설명
---|---|---
0|OK|유료 광고
100|	Non-chargeable ad is supplied|무료 광고(속성 : 공익 광고, Cauly 기본 광고)
200|	No filled AD	|광고 없음
400|	The app code is invalid. Please check your app code!	|App code 불일치 또는default app code
500|	Server error	|cauly서버 에러
-100|	SDK error	|SDK 에러
-200|	Request Failed(You are not allowed to send requests under minimum interval)	|최소요청주기 미달


[sample](http://image.cauly.co.kr:15151/richad/test/...)
 

