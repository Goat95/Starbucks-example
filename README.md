[![Netlify Status](https://api.netlify.com/api/v1/badges/320a68cf-fd26-49ae-aa2e-0928ecf2e2f1/deploy-status)](https://app.netlify.com/sites/goatstarbucks/deploys)

# 스타벅스 클론코딩

패스트캠퍼스에서 제공해주는 온라인 강의를 보면서 스타벅스 랜딩 페이지를 클론 코딩했습니다.

[스타벅스 클론 사이트](https://goatstarbucks.netlify.app/)

## HTML 클래스 속성의 작명법

BEM(Block Element Modifier)

- 요소\_\_일부분: Underscore(Lodash) 기호로 요소의 일부분을 표시
- 요소--상태: Hyphen(Dash) 기호로 요소의 상태를 표시

## 사용한 JS 라이브러리

1. GSAP & ScrollToPlugin  
   GSAP은 자바스크립트로 제어하는 타임라인 기반의 애니메이션 라이브러리입니다. ScrollToPlugin은 스크롤 애니메이션을 지원하는 GSAP 플러그인입니다.

```html
<script
  src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.5.1/gsap.min.js"
  integrity="sha512-IQLehpLoVS4fNzl7IfH8Iowfm5+RiMGtHykgZJl9AWMgqx0AmJ6cRWcB+GaGVtIsnC4voMfm8f2vwtY+6oPjpQ=="
  crossorigin="anonymous"
></script>
<script
  src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.5.1/ScrollToPlugin.min.js"
  integrity="sha512-nTHzMQK7lwWt8nL4KF6DhwLHluv6dVq/hNnj2PBN0xMl2KaMm1PM02csx57mmToPAodHmPsipoERRNn4pG7f+Q=="
  crossorigin="anonymous"
></script>
```

```js
gsap.to(요소, 시간, 옵션);
// 또는
TweenMax.to(요소, 시간, 옵션);

gsap.to(window, 0.7, {
  scrollTo: 0,
});
```

2. Swiper  
   Swiper는 하드웨어 가속 전환과 여러 기본 동작을 갖춘 현대적인 슬라이드 라이브러리입니다.

```html
<!-- in HEAD -->
<link
  rel="stylesheet"
  href="https://unpkg.com/swiper@6.8.4/swiper-bundle.min.css"
/>
<script src="https://unpkg.com/swiper@6.8.4/swiper-bundle.min.js"></script>

<!-- in BODY -->
<div class="swiper-container">
  <div class="swiper-wrapper">
    <div class="swiper-slide">1</div>
    <div class="swiper-slide">2</div>
    <div class="swiper-slide">3</div>
  </div>
</div>
```

```js
new Swiper(요소, 옵션);

new Swiper(".swiper-container", {
  direction: "vertical", // 수직 슬라이드
  autoplay: true, // 자동 재생 여부
  loop: true, // 반복 재생 여부
});
```

3. ScrollMagic  
   ScrollMagic은 스크롤과 요소의 상호 작용을 위한 자바스크립트 라이브러리입니다.
   대표적으로 어떤 요소가 현재 화면에 보이는 상태인지를 확인할 때 사용합니다.

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/ScrollMagic/2.0.8/ScrollMagic.min.js"></script>
```

```js
new ScrollMagic.Scene({
  // 감시할 장면(Scene)을 추가
  triggerElement: spyEl, // 보여짐 여부를 감시할 요소를 지정
  triggerHook: 0.8, // 화면의 80% 지점에서 보여짐 여부 감시
})
  .setClassToggle(spyEl, "show") // 요소가 화면에 보이면 show 클래스 추가
  .addTo(new ScrollMagic.Controller()); // 컨트롤러에 장면을 할당(필수!)
```

4. Lodash  
   Lodash는 다양한 유틸리티 기능을 제공하는 자바스크립트 라이브러리입니다.

```html
<script
  src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/4.17.20/lodash.min.js"
  integrity="sha512-90vH1Z83AJY9DmlWa8WkjkV79yfS2n2Oxhsi2dZbIv0nC4E6m5AbH8Nh156kkM7JePmqD6tcZsfad1ueoaovww=="
  crossorigin="anonymous"
></script>
```

## Youtube API

IFrame Player API를 통해 YouTube 동영상을 제어할 수 있습니다.

유튜브 영상이 출력될 위치에 요소를 지정(생성)합니다.

```html
<!-- in HEAD -->
<script defer src="./js/youtube.js"></script>

<!-- in BODY -->
<div id="player"></div>
```

onYouTubePlayerAPIReady 함수 이름은 Youtube IFrame Player API에서 사용하는 이름이기 때문에 다르게 지정하면 동작하지 않습니다!
그리고 함수는 전역(Global) 등록해야 합니다!

플레이어 매개변수(playerVars)에서 더 많은 옵션을 확인할 수 있습니다.

```js
// Youtube IFrame API를 비동기로 로드합니다.
const tag = document.createElement("script");
tag.src = "https://www.youtube.com/iframe_api";
const firstScriptTag = document.getElementsByTagName("script")[0];
firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);

function onYouTubePlayerAPIReady() {
  // <div id="player"></div>
  new YT.Player("player", {
    videoId: "An6LvWQuj_8", // 재생할 유튜브 영상 ID
    playerVars: {
      autoplay: true, // 자동 재생 유무
      loop: true, // 반복 재생 유무
      playlist: "An6LvWQuj_8", // 반복 재생할 유튜브 영상 ID 목록
    },
    events: {
      // 영상이 준비되었을 때,
      onReady: function (event) {
        event.target.mute(); // 음소거!
      },
    },
  });
}
```
