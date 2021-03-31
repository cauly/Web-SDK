CAULY Web SDK 가이드
----

### 개요
모바일 웹 사이트에서 Cauly 광고를 사용하기 위한 Web SDK 가이드 문서입니다.

### 1. 사전 안내
- 광고가 표시될 DIV 태그의 id 와 CaulyAds 에 전달하는 파라메터 displayid 는 동일해야 합니다.
- 한 페이지에 Cauly 광고가 여러 개 일 경우 DIV 태그의 id 는 중복되지 않도록 주의해주십시오.
- 구버전에서 신버전으로 변경 시 동일한 AppCode를 사용 할 경우 [고객센터](https://www.cauly.net/index.html#/apps/contactUs/dev) 로 문의해주십시오.

### 2. 초기화 파라메터 정의

|파라메터 이름|파라메터 설명|필수 여부|
|:---:|:---:|:---:|
|app_code|<a href="http://www.cauly.net" target="_blank">CAULY</a> 에서 발급 받은 app code|O|
|displayid|광고 노출 DIV 태그 ID|O|
|placement|광고 노출 지면 ID (Default:1)|O 
|success|광고 노출 성공 시 호출 될 callback method| 
|passback|광고 노출 실패 시 호출 될 callback method| 

### 

### 3. 작성 예제

#### 1) 배너 (Banner)
Cauly 배너 광고를 사용하기 위해서는  
아래와 같이 위에서 정의한 필요한 파라메터들과 함께 CaulyAds 클래스를 초기화 하도록 합니다.
```html
<div id='caulyDisplay'>
  <script src='//image.cauly.co.kr/websdk/common/lasted/ads.min.js'></script>
  <script>
    new CaulyAds({
      app_code:"매체사에 발급된 App Code",
      placement:1,
      displayid:'caulyDisplay',
      success:function(){},
      passback:function(){}
    });
  </script>
</div>
```
:warning: 모바일 웹페이지를 WebView 를 통해 표시하는 Hybrid 앱에서는 디바이스 광고 식별자,  
즉 GAID (Google Advertiser Indentifier) 혹은 IDFA (Apple Identifier For Advertising) 를 Cauly 로 전달해야 합니다. 흐름은 다음과 같습니다.  

a) Hybrid 앱에서 에서 먼저 GAID 혹은 IDFA 를 직접 추출합니다.  
b) Hybrid 앱에서는 아래 예제의 Javascript 코드가 WebView 내에 구현되어 있다면 saveAdvertiserId() 메소드의 "ADID 정보" 부분에 실제 추출한 디바이스 광고 식별자를 전달합니다.  
c) saveAdvertiserId() 메소드를 호출한 이후에 CaulyAds 클래스가 초기화 될 수 있도록 합니다.  

* 디바이스 광고 식별자 추출 방법 : [Android](https://developers.google.com/android/reference/com/google/android/gms/ads/identifier/AdvertisingIdClient) / [iOS](https://developer.apple.com/kr/app-store/user-privacy-and-data-use)
* WebView 내의 Javascript 와 네이티브 코드 간 데이터 전달 방법 : [Android](https://developer.android.com/guide/webapps/webview?hl=ko#BindingJavaScript) / [iOS](https://developer.apple.com/documentation/webkit/wkusercontentcontroller?language=objc)
```html
<div id='caulyDisplay'>
  <script src='//image.cauly.co.kr/websdk/common/lasted/ads.min.js'></script>
  <script>
    // Advertiser Id 를 저장하는 메소드
    function saveAdvertiserId(adid) {
      try {
        if (!!window.localStorage) {
          localStorage.removeItem("caulyad_adid");
          localStorage.setItem("caulyad_adid", adid);
          return true;
        } else if (navigator.cookieEnabled) {
          var date = new Date();
          date.setTime(date.getTime() + (365*24*60*60*1000));
          document.cookie = "caulyad_adid=" + adid + ";path=/;expire=" + date.toUTCString() + ";domain=" + location.hostname + ";";
          return true;
        } else {
          return false;
        }
      } catch(e) {
        return false;
      }
    }

    // 매체사에서 추출한 Advertiser Id 를 저장
    saveAdvertiserId("ADID 정보");

    // Cauly SDK 초기화
    var cauly_ads = new CaulyAds({
      app_code:"매체사에 발급된 App Code",
      placement:1,
      displayid:'caulyDisplay',
      success:function(){},
      passback:function(){}
    });
   </script>
</div>
```

#### 2) 전면 (Interstitial)
Cauly 전면 광고를 사용하기 위해서는  
아래와 같이 위에서 정의한 필요한 파라메터들과 함께 CaulyAds 클래스를 초기화 하도록 합니다.  
다만, 전면 광고의 경우에는 광고 표시 시점에 따로 showPopup() 메소드를 호출해주어야만 합니다.

참고로, 전면 광고의 노출 주기는 5초로 동작하게 됩니다.  
노출 주기 변경이 필요하신 경우 [고객센터](https://www.cauly.net/index.html#/apps/contactUs/dev) 를 통해 연락해주십시오.
```html
<div id='caulyDisplay'>
  <script src='//image.cauly.co.kr/websdk/common/lasted/ads.min.js'></script>
  <script>
    // Cauly SDK 초기화
    var caulyAds = new CaulyAds({
      app_code:"매체사에 발급된 App Code",
      placement:1,
      displayid:'caulyDisplay',
      success:function(){},
      passback:function(){}
    });
  
    // Cauly 전면 광고 표시
    caulyAds.showPopup();
  </script>
</div>
```
:warning: 모바일 웹페이지를 WebView 를 통해 표시하는 Hybrid 앱에서는 디바이스 광고 식별자,  
즉 GAID (Google Advertiser Indentifier) 혹은 IDFA (Apple Identifier For Advertising) 를 Cauly 로 전달해야 합니다. 흐름은 다음과 같습니다.

a) Hybrid 앱에서 에서 먼저 GAID 혹은 IDFA 를 직접 추출합니다.  
b) Hybrid 앱에서는 아래 예제의 Javascript 코드가 WebView 내에 구현되어 있다면 saveAdvertiserId() 메소드의 "ADID 정보" 부분에 실제 추출한 디바이스 광고 식별자를 전달합니다.  
c) saveAdvertiserId() 메소드를 호출한 이후에 CaulyAds 클래스가 초기화 될 수 있도록 합니다.  

* 디바이스 광고 식별자 추출 방법 : [Android](https://developers.google.com/android/reference/com/google/android/gms/ads/identifier/AdvertisingIdClient) / [iOS](https://developer.apple.com/kr/app-store/user-privacy-and-data-use)
* WebView 내의 Javascript 와 네이티브 코드 간 데이터 전달 방법 : [Android](https://developer.android.com/guide/webapps/webview?hl=ko#BindingJavaScript) / [iOS](https://developer.apple.com/documentation/webkit/wkusercontentcontroller?language=objc)
```html
<div id='caulyDisplay'>
  <script src='//image.cauly.co.kr/websdk/common/lasted/ads.min.js'></script>
  <script>
    // Advertiser Id 를 저장하는 메소드
    function saveAdvertiserId(adid) {
      try {
        if (!!window.localStorage) {
          localStorage.removeItem("caulyad_adid");
          localStorage.setItem("caulyad_adid", adid);
          return true;
        } else if (navigator.cookieEnabled) {
          var date = new Date();
          date.setTime(date.getTime() + (365*24*60*60*1000));
          document.cookie = "caulyad_adid=" + adid + ";path=/;expire=" + date.toUTCString() + ";domain=" + location.hostname + ";";
          return true;
        } else {
          return false;
        }
      } catch(e) {
        return false;
      }
    }

    // 매체사에서 추출한 Advertiser Id 를 저장
    saveAdvertiserId("ADID 정보");

    // Cauly SDK 초기화
    var cauly_ads = new CaulyAds({
      app_code:"매체사에 발급된 App Code",
      placement:1,
      displayid:'caulyDisplay',
      success:function(){},
      passback:function(){}
    });

    // 전면 광고인 경우에만 필요
    cauly_ads.showPopup();
   </script>
</div>
```
#### 3) 네이티브 (Native)
Cauly 네이티브 광고를 사용하기 위해서는  
아래와 같이 위에서 정의한 필요한 파라메터들과 함께 CaulyAds 클래스를 초기화 하도록 합니다.
```html
<div id='caulyDisplay'>
  <script src='//image.cauly.co.kr/websdk/common/lasted/ads.min.js'></script>
  <script>
    // Cauly SDK 초기화
    new CaulyAds({
      app_code:"매체사에 발급된 App Code",
      placement:1,
      displayid:'caulyDisplay',
      success:function(){},
      passback:function(){}
    });
  </script>
</div>
```
:warning: 모바일 웹페이지를 WebView 를 통해 표시하는 Hybrid 앱에서는 디바이스 광고 식별자,  
즉 GAID (Google Advertiser Indentifier) 혹은 IDFA (Apple Identifier For Advertising) 를 Cauly 로 전달해야 합니다. 흐름은 다음과 같습니다.

a) Hybrid 앱에서 에서 먼저 GAID 혹은 IDFA 를 직접 추출합니다.  
b) Hybrid 앱에서는 아래 예제의 Javascript 코드가 WebView 내에 구현되어 있다면 saveAdvertiserId() 메소드의 "ADID 정보" 부분에 실제 추출한 디바이스 광고 식별자를 전달합니다.  
c) saveAdvertiserId() 메소드를 호출한 이후에 CaulyAds 클래스가 초기화 될 수 있도록 합니다.  

* 디바이스 광고 식별자 추출 방법 : [Android](https://developers.google.com/android/reference/com/google/android/gms/ads/identifier/AdvertisingIdClient) / [iOS](https://developer.apple.com/kr/app-store/user-privacy-and-data-use)
* WebView 내의 Javascript 와 네이티브 코드 간 데이터 전달 방법 : [Android](https://developer.android.com/guide/webapps/webview?hl=ko#BindingJavaScript) / [iOS](https://developer.apple.com/documentation/webkit/wkusercontentcontroller?language=objc)
```html
<div id='caulyDisplay'>
  <script src='//image.cauly.co.kr/websdk/common/lasted/ads.min.js'></script>
  <script>
    // Advertiser Id 를 저장하는 메소드
    function saveAdvertiserId(adid) {
      try {
        if (!!window.localStorage) {
          localStorage.removeItem("caulyad_adid");
          localStorage.setItem("caulyad_adid", adid);
          return true;
        } else if (navigator.cookieEnabled) {
          var date = new Date();
          date.setTime(date.getTime() + (365*24*60*60*1000));
          document.cookie = "caulyad_adid=" + adid + ";path=/;expire=" + date.toUTCString() + ";domain=" + location.hostname + ";";
          return true;
        } else {
          return false;
        }
      } catch(e) {
        return false;
      }
    }

    // 매체사에서 추출한 Advertiser Id 를 저장
    saveAdvertiserId("ADID 정보");

    // Cauly SDK 초기화
    var cauly_ads = new CaulyAds({
      app_code:"매체사에 발급된 App Code",
      placement:1,
      displayid:'caulyDisplay',
      success:function(){},
      passback:function(){}
    });
   </script>
</div>
```
