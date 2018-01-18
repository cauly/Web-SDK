CAULY WEB SDK 사용자 가이드
----
* SDK Version 5.3.6

#### 문서의 목적 및 범위
* 본 문서는 CAULY 광고를 모바일 웹에서 사용하기 위한 Web SDK 가이드입니다. 

### 개요
* Cauly Web 광고를 사용하기 위한 SDK입니다.
모바일웹을 대상으로 하며 https를 지원합니다.

#### Javascript 작성 방법
- 광고를 사용하기 위해서 CaulyAds 객체를 생성합니다.
- 변수의 이름이 CaulyAds 아닐 경우 정상 동작하지 않을 수 있습니다.
- parameter

인자명|설명|필수
---|---|---
app_code|<a href="http://www.cauly.net" target="_blank">CAULY</a> 에서 발급 받은 app code|O
success|광고 노출 성공시 호출될 callback| |
passback|광고 노출 실패시 호출될 callback| |


#### SDK Example
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
