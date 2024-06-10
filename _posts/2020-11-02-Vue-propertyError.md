---
title: '[vue.js error] Property or method is not defined on the instance but referenced
  during render. Make sure that this property is reactive, either in the data option,
  or for class-based components, by initializing the property.'
date: 2020-11-02 12:22:42 +0900
categories: [Web, Vue.js]
tags: [Vue.js, Web, javascript]
seo:
  date_modified: 2021-03-09 13:50:09 +0900
---

크게 두 가지 실수를 했을 때 발생하는 에러이다.
1. 변수명 오타가 발생했을 경우
    - 사용한 변수명과 실제 선언한 변수명이 달라서 정의되지 않았다고 판단하게 된 것.
    - 가장 많은 경우이다. 이 에러가 뜨면 일단 오타부터 찾아보면 된다.
2. 메소드가 너무 밑에 있어서 렌더링이 되는 시점에 해당 메소드가 아직 렌더링이 되지 않았을 경우
    - 오류가 발생하는 메소드를 root(최상단)으로 옮겨주면 된다.


어이없는 해결방법인 것 같다..

> [참고]
> [https://stackoverflow.com/questions/42908525/vue-warn-property-or-method-is-not-defined-on-the-instance-but-referenced-dur](https://stackoverflow.com/questions/42908525/vue-warn-property-or-method-is-not-defined-on-the-instance-but-referenced-dur)