CAULY WEB SDK 사용자 가이드
----

### 개요
* Cauly Web 광고를 사용하기 위한 SDK입니다.
모바일웹을 대상으로 하며 https를 지원합니다.

#### Javascript 작성 방법
- 광고영역의 div id와 CaulyAds의 displayid는 동일해야 합니다.
- 한 페이지에 카울리광고가 여러 개 일 경우 div id는 중복되지 않아야 합니다.
- 구버전에서 신버전으로 변경 시 동일한 AppCode를 사용 할 경우 [고객센터](https://www.cauly.net/index.html#/apps/contactUs/dev)로 문의 바랍니다.
- parameter

인자명|설명|필수
---|---|---
app_code|<a href="http://www.cauly.net" target="_blank">CAULY</a> 에서 발급 받은 app code|O
displayid|광고 노출 영역|O|
placement|광고 노출 영역 ID(Default:1)|O 
success|광고 노출 성공시 호출될 callback| 
passback|광고 노출 실패시 호출될 callback| 


#### SDK Example
- 배너, 네이티브
```html
<div id='caulyDisplay'>
	<script src='//image.cauly.co.kr/websdk/common/lasted/ads.min.js'></script>
	<script>
      new CaulyAds({
        app_code:app_code,
        placement:1,
        displayid:'caulyDisplay',
        passback:function(){},
        success:function(){}
      });
   </script>
</div>
```
- 전면
	- 전면광고의 노출주기는 5초 입니다. 노출주기 변경을 원하시는 경우 [고객센터](https://www.cauly.net/index.html#/apps/contactUs/dev)를 통해 연락 바랍니다.
```html
<div id='caulyDisplay'>
	<script src='//image.cauly.co.kr/websdk/common/lasted/ads.min.js'></script>
	<script>
      var cauly_ads = new CaulyAds({
        app_code:app_code,
        placement:1,
        displayid:'caulyDisplay',
        passback:function(){},
        success:function(){}
      });
      cauly_ads.showPopup();
   </script>
</div>
```
