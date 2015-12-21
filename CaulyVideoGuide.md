![Valid XHTML](http://cauly044.fsnsys.com:10010/images/logo_cauly_main.png) CAULY Video Mobile Web SDK 연동 가이드  
----

* CAULY Video 사용자 가이드
* version 4.2.1


#### 문서 이력
* 4.2.0 2015.07.31 초안 작성
* 4.2.1 2015.09.04 작성
* 
#### 문서의 목적 및 범위
* 본 문서는  CAULY Video 를 모바일 웹에서 사용하기 위한 Web SDK 가이드입니다. 

#### 개요
* CAULY 광고 형태 중  CAULY Video를 위한 SDK 입니다.<br/>모바일 웹을 대상으로 합니다.

#### 절차
* <a href="http://cauly.net" target="_blank">CAULY</a> 에서 앱을 등록하고 app code를 발급받습니다.


#### SDK Javascript link
+  web sdk는 다음 주소를 사용 합니다. (not yet uploaded)
	-   http://image.cauly.co.kr/websdk/caulyad.video_4.2.1.js
+  사용 방법
	- ```<script src="http://image.cauly.co.kr/websdk/caulyad.video_4.2.1.js"></script>```


#### CaulyVideoAd 변수 생성
*  CAULY Video를 사용하기 위해서 CaulyVideoAd 객체를 생성합니다.
* Paramter

	인자명|설명|필수
	--- | --- | ---
	appcode|<a href="http://cauly.net" target="_blank">CAULY</a> 에서 발급 받은 app code|O
  setKeywords	|광고 타켓팅에 활용되는 키워드 설정( 카테고리, 태그 등을 ','(컴마)로 구분하여 최대 3개까지 설정가능)|
  setSkipCount	|광고의 건너띄우기 버튼의 노출시간설정|
  setVideoContainer|Video를 감싸고 있는 DIV의 아이디 설정|
  setLandingOpenWindow(true)|광고랜딩을 새창으로 열게 한다|
  destroy| 카울리비디오를 삭제한다.
  requestVideoAd(appcode, caulyVideoAdCallback)|앱의 메인콘텐츠 비디오 ID 설정, 광고 callback|
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
	var caulyVideoAdReceived =false;
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
		document.getElementById('mainPlayer').style.display = "block";
		document.getElementById('mainPlayer').play();
		/*
		 Do what you want to do.
		*/
	}
	
	//광고가 준비되었을 때, 2가지 방법으로 플레이 가능.  디폴트는 INJECTION
	//INJECTION type : MainVideo(광고가 아닌 메인 컨텐츠영상)에 source injection 방식
	//FLOATING type  : MainVideo와 별개로  <video> 태그를 삽입하는 방식(단, 사용자 클릭이벤트 시, 재생가능) 
	function caulyVideoPlay()
	{
		//광고수신에 성공되었을 때,  카울리비디오를 수행한다.
		if(caulyVideoAdReceived==true)
			videoAd.showVideoAd('INJECTION');  // INJECTION, FLOATING  디폴트는 INJECTION
		else
			loadVideo();
	}
	//광고수신에 성공되었을 때 호출된다.
	function onReceiveVideoAd(info)
	{
		caulyVideoAdReceived = true;	
		
	}
	//광고의 재생시작을 알려준다.
	function onStartVideoAd()
	{
	}
  // CAULY Video 재생 중, 재생완료, 광고클릭, 스킵버튼클릭, 플레이에러 등으로 광고영상이 끝났을 때 호출
	function onFinishVideoAd(code, msg)
	{
		caulyVideoAdReceived = false;
		loadVideo();
	}
//	광고수신에 실패되었을 때 호출된다.
	function onFailToReceiveVideoAd(code,msg)
	{
		caulyVideoAdReceived = false;
		loadVideo();
	}
	//CaulyVideoAd를 호출한다. 
	function loadVideoAd()
	{
		videoAd = new CaulyVideoAd("APPCODE");
		videoAd.setVideoContainer('mvContainer');
		videoAd.setKeywords("category1,category2,category3"); //카테고리 설정 최대 3개까지 설정가능 
		videoAd.requestVideoAd("mainPlayer", caulyVideoAdCallback);
	}
	loadVideoAd();
	
	window.onload = function()
	{
		//메인 컨텐츠의 재생 버튼 시, INJECTION TYPE 카울리 비디오 호출. 
		document.getElementById('mainPlayer').addEventListener('play',function()
		{
			if(caulyVideoAdReceived==true)
				caulyVideoPlay();  
		}, false);
	}
	```

[onFailToReceiveVideoAd 코드 정의](onFailToReceiveVideoAd)
		
Code|Message|설명
---|---|---
0|OK|유료 광고
100|	Non-chargeable ad is supplied|무료 광고(속성 : 공익 광고, Cauly 기본 광고)
200|	No filled AD	|광고 없음
400|	The app code is invalid. Please check your app code!	|App code 불일치 또는default app code
500|	Server error	|cauly서버 에러
-100|	SDK error	|SDK 에러
-200|	Request Failed(You are not allowed to send requests under minimum interval)	|최소요청주기 미달

[ onFinishVideoAd 코드 정의](onFinishVideoAd)
		
Code|Message|설명
---|---|---
201|	COMPLETE|광고를 끝까지 시청했을 시
202|	ERROR	|광고 시청 시  에러 발생 시 
203|	CLICK	|광고의 랜딩이미지 클릭 시
204|	SKIP	|광고의 스킵버튼을 클릭 시
205|	PAUSE	|광고 시청 중,  전원버튼이나 홈버튼 클릭 시
[샘플 페이지 이동](http://image.cauly.co.kr/richad/test/CaulyVideo/videoad.html)
 

