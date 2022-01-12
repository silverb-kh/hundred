# 움직이는 배너관리내 slick을 이용한 백그라운드 핸들링

관리자에서 슬라이드별로 컬러를 지정하고 배너를 포함한 상위 부모의 백그라운드 컬러를 변경하려고 함. 슬라이드별 이벤트를 선언할 떄 아래 스크립트를 이용할 수 있음.

## 움직이는 배너관리 (소스 위치)

* 컨트롤러 => Widget/Front/Proc/SliderBannerWidget.php
* 스킨소스 => data/skin/front/[***]/proc/_slider_banner.html
* 슬라이드 라이브러리 : slick[https://kenwheeler.github.io/slick/]

### 2022.01 작업 요청 - 메인 배너의 백그라운드 이미지를 변경하자.

```
$('.slider-banner-{=bannerCode}').on('afterChange', function(event, slick, currentSlide){
    var main_slide_default = "#f4f4f4";

    // 슬라이드 이후에 변화 시키기 위해서 current 값을 수동으로 계산해야 한다.
    var idx = currentSlide - 1;
    if (idx < 0){
	    idx = slick.$slides.length -1 ;
    }
    // description내용은 title에 표시된다.
    var title = slick.$slides[idx].querySelector('img').title;
    
    if (title.startsWith("#")){
	    // 설정된 값으로 변경합니다. 
	    $('.main-slide').css("background-color",title);
    } else {
	    // 기본값으로 변경합니다. 
	    $('.main-slide').css("background-color",main_slide_default);
    }
});
```