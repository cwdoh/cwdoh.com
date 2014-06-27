---
layout: post
title: "Chrome Enchanted: HTML5 2014"
date:   2014-05-11 02:16:00
categories: HTML5
author: Chang W. Doh
description: "2014년은 HTML5의 정식으로 Recommended되는 시점입니다. 또 개인적으로 기대하고 있는 몇가지 HTML5 새로운 규격들이 라이브되는 시기이기도 합니다. Web Components, Web Animations, ServiceWorker, WebRTC에 대해 개괄적으로 정리해보고 이 규격들이 향후 웹 개발 패러다임에 어떤 영향을 미칠지에 대해 조심스럽게 예측해보았습니다."
published: false
---

시간은 화살처럼 흐른다더니 어느덧 2014년의 절반에 닿아가고 있습니다. [W3C는 올해 말 HTML 5.0 표준안을 확정할 예정][1]입니다만 살아있는 표준(Living Standard)로써의 HTML5의 혁신은 지속되고 있습니다. 이번 포스트에서는 현재 시점에서 크롬에 코드가 일부 혹은 전체가 탑재되고 있는 HTML5 규격 중 주목할만한 것들에 대해 정리해보았습니다.

* **Web Components**
  * 웹 페이지 구성요소 혹은 다른 페이지를 컴포넌트화하여 사용할 수 있는 규격.
  * 세부적인 규격은 [Shadow DOM], [HTML Imports], [Template], [Custom Elements]으로 구성되어 있습니다.
* **Web Animations**
  * CSS3 Animation, CSS3 Transition, SVG Animation을 동적으로 제어할 수 있는 자바스크립트 기반 애니메이션 규격.
* **WebRTC**
  * 실시간 통신(RealTime Communication)을 지원하기 위한 새로운 P2P 통신 규격.
* **Service Worker**
  * 웹 페이지와 독립적인 생명주기(Life Cycle)로 동작하며 웹 페이지의 리소스 등의 요청에 대한 Hook 등이 가능한 이벤트 기반 Worker 시스템.

![Chrome]("http://www.google.com/intl/ko/chrome/assets/common/images/chrome_logo_2x.png)

## Web Components

| 항목 | 설명 |
|---|---|
| 구현 상태 | |
| 지원 버전 |  |
| 관련 오픈소스 | |

Web Components는 (HTML, CSS, JavaScript을 통해) 통상적으로 구성된 웹 페이지 일부 혹은 그 자체를 컴포넌트화하여 다른 웹 페이지 내에서 재사용할 수 있도록 하는 기술입니다. `Web Components`를 규격이 아니라 기술이라고 하는 이유는 통상적인 웹 기능과는 달리 4가지의 독립적인 규격의 집합으로 구현되는 기술이기 때문입니다.

> 개괄적인 내용은 '[웹 컴포넌트: 차세대 프론트엔드 웹 개발로 가는 관문]()'이라는 거창한 제목의 포스트에서 다룬 바가 있기 때문에 여기서 이를 복잡하게 다루지는 않을 것입니다. :)

### 웹에서 컴포넌트가 왜 필요할까?

> 여전히 우리는 다른 프로젝트에서 사용했던 리스트 아이템들을 새로운 프로젝트에서도 적용하기 위해 마크업을 복사해서 수정하고 스타일링을 위한 새로운 CSS를 작성하거나 기존 스타일과의 충돌을 제거하고, 자바스크립트를 최대한 모듈화하여 작성하고 있습니다. 그러나 여전히 이는 근본적인 재활용 방법이 아닌 개발자의 역량과 경험에 의존하고 있는 일종의 개선된 작업흐름에 가깝습니다. 즉, 언제든지 우리는 태그의 바다(Tag Soup)와 같은 위험 지역에 다시 빠질 수 있는 가능성을 안고 있습니다.

웹 컴포넌트(Web Component)의 개념 자체가 아주 새롭고 특별한 기술은 아닙니다. '컴포넌트(Component)'라는 말은 들어보셨으리라 생각합니다.


사실 우리는 필요한 것이 무엇인지는 이미 알고 있습니다. 다만 지금까지는 이를 방법론으로, 개발도구로, 경험으로 해결해왔을 뿐이죠. 이제 우리에게 필요한 것은 '자주 사용되는 유용한 것들 혹은 구조 상 분리가 필요한 것들을 개발의 다른 요소들과 충돌하지 않는 형태로 재활용이 가능하도록 만들어 주는 일관적인 방법'입니다. 특히 UI 요소들이 많은 프론트엔드 개발에서는 '리소스 관점에서 분리되어 있는 HTML, CSS, 자바스크립트를 하나로 묶어 주는 것' 또한 중요한 기능 중의 하나가 됩니다. 소프트웨어 개발에서는 이러한 요소들을 '컴포넌트(Component)'라는 개념으로 오랜동안 사용해 왔으며 예를 들자면 백엔드에서는 이미 다양한 형태의 컴포넌트가 각 플랫폼에 적합한 형태로 오랜동안 배포되고 사용되어 왔습니다. 이제 조금 더 나아가서 우리는 컴포넌트를 웹에서 (특히 프론트엔드 개발에서) 사용할 방법이 필요하며 가능하다면 도구적인 지원을 받을 수 있으면 더 좋을 것입니다.

다행스럽게도 W3C에서는 이러한 컴포넌트 기술을 웹에서 적용할 수 있도록 새로운 규격의 집합을 만들었으며 이 규격들을 묶어 '웹 컴포넌트(Web Component)'라고 부르게 되었고 이를 지원하는 도구와 라이브러리들의 작업이 여러 곳에서 매우 빠르게 진행되고 있습니다.

#### 컴포넌트의 미덕은 재사용성과 재사용성 :)

### 4 Pillars of Web Components

웹 컴포넌트는 다음과 같은 4가지의 규격으로 구성되어 있습니다.

| 규격 | 설명 |
|---|---|
| Shadow DOM | 컴포넌트의 DOM, CSS, JS의 캡슐화(encapsulation)와 스코프(Scope)의 분리를 제공 |
| HTML Template | 로딩 시간에는 비활성화되는 마크업을 정의하고 이를 실행 시간에 복제할 수 있는 기능을 제공 |
| Custom Element | 웹 문서에서 사용할 엘리먼트의 동적인 등록을 통해 컴포넌트의 명시적인 alias를 선언 |
| HTML Imports | 웹 문서 내에 외부 리소스를 포함(Import)하기 위한 기능을 제공 |

###

### 참고 링크

* [WebPlatform - WebRTC API](http://docs.webplatform.org/wiki/apis/webrtc)


## Web Animations

| 항목 | 설명 |
|---|---|
| 구현 상태 | |
| 지원 버전 | |
| 관련 오픈소스 | |


## WebRTC


| 항목 | 설명 |
|---|---|
| 구현 상태 | |
| 지원 버전 | |
| 관련 오픈소스 | |


## Service Worker

| 항목 | 설명 |
|---|---|
| 구현 상태 | |
| 지원 버전 | |
| 관련 오픈소스 | |


[1]: http://dev.w3.org/html5/decision-policy/html5-2014-plan.html#plan "W3C Plan 2014"

[Shadow DOM]:
[HTML Imports]:
[Template]:
[Custom Elements]:
[Web Animations]:
[WebRTC]:
[Service Worker]:
