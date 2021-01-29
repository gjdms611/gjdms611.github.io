---
title: "[vue.js error] Unknown custom element: did you register the component correctly?\
  \ For recursive components, make sure to provide the 'name' option."
date: 2020-11-21 22:21:52 +0900
categories: [Web, Vue.js]
tags: [Vue.js, Web, javascript]
seo:
  date_modified: 2021-01-29 14:13:28 +0900
---

'Unknown element'라는 말에서 알 수 있듯이, 오타가 났을 때 뜨는 것이다.  
처음에는 recursive라는 단어에 꽂혀 같은 컴포넌트를 중복해서 사용하면 안되는 줄 알고 name도 설정해보고 별짓을 다했었지만 대개 actions를 action으로 쓴다던지 하는 오타가 나서 이 에러가 뜨는 일이 많다.
