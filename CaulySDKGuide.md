CAULY WEB SDK 사용자 가이드
----
* SDK Version 5.3.6

### 개요
* Cauly Web 광고를 사용하기 위한 SDK입니다.
모바일웹을 대상으로 하며 https를 지원합니다.

#### Javascript 작성 방법
- 광고영역의 div id와 CaulyAds의 displayid는 동일해야 합니다.
- 한 페이지에 카울리광고가 여러 개 일 경우 div id는 중복되지 않아야 합니다.
- 페이지가 https일 경우 http://를 https://로 변경해야 합니다.
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
	<script src='http://image.cauly.co.kr/websdk/common/lasted/ads.js'></script>
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
```html
<div id='caulyDisplay'>
	<script src='http://image.cauly.co.kr/websdk/common/lasted/ads.js'></script>
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
