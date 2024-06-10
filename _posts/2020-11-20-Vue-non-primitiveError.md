---
title: '[vue.js error] Avoid using non-primitive value as key, use string/number value
  instead.'
date: 2020-11-20 20:23:22 +0900
categories: [Web, Vue.js]
tags: [Vue.js, Web, javascript]
seo:
  date_modified: 2021-01-29 14:13:28 +0900
---

v-for문을 사용할 때 나타나는 error.
key에 value를 바로 입력하는 것이 아닌 index값을 연결해주면 된다.

```javascript
v-for="item in items" :key="item"
```

이렇게 입력했을 때 오류가 발생한다.

```javascript
v-for="(item, idx) in items" :key="idx"
```

이렇게 item대신 idx를 연결하면 오류가 사라진다.
