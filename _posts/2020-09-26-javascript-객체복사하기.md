---
title: '[javascript] 객체 복사하기'
date: 2020-09-26 01:14:07 +0900
categories: [Programming language, javascript]
tags: [javascript, Web]
seo:
  date_modified: 2020-10-29 17:18:17 +0900
---

## 얕은 복사(Shallow Copy)

get으로 받아온 값을 객체 1에 복사하고, 값을 조금 수정해 또 다른 객체 2에 복사한 후 객체 1과 2의 값을 비교해 달라진 값만 비교하고 싶었다.  
그런데 이게 웬걸, 난 분명 객체 2의 값만 변경했는데 객체 1의 값도 같이 변경되는게 아닌가?

```javascript
let obj1 = {
  a: 1,
  b: {
    c: 1,
  },
};
let obj2 = obj1;

obj2.a = 2;
obj2.b.c = 2;

console.log(obj1.a); // 2
console.log(obj1.b.c); // 2
```

그렇다, 나는 `let 객체2 = 객체1`과 같은 형식으로 넣어주었기 때문에 객체1이 고대로 객체2에 대입되었고 같은 객체를 참조하는 변수만 두 개가 생긴 셈이므로 객체 2를 바꾸면 객체 1도 바뀌어버리는 것이다. 이를 **얕은 복사** 라고 한다.  
곤란하다. 난 객체1을 참조하는 것이 아니라 객체1의 값을 갖는 객체2를 새로 생성하고 싶다.  
객체를 복사하는 방법에는 다음과 같은 방법들이 있었다.

## Deep-Shallow Copy

객체를 복사하지만 하위 객체는 참조한다. 다음의 두 가지 방법이 있다.

1. Object.assign()
2. spread 사용

처음에 이 말이 잘 이해가 안돼서, 그러면 복사를 하는게 아니지 않나? 하고 Deep-Copy를 코드에 적용했다. 그러나 Object.assign()에 비해 효율이 더 떨어진다고 한다..  
예컨대 이런 이야기다. 1단계 깊이까지는 복사를 하지만, 그 밑은 복사하지 않고 그냥 가져온달까.

```javascript
let obj1 = {
  a: 1,
  b: {
    c: 1,
  },
};
let obj2 = Object.assign({}, obj1);

obj2.a = 2;
obj2.b.c = 2;

console.log(obj1.a); // 1
console.log(obj1.b.c); // 2
```

사실 내가 필요했던 코드에서는 객체 내부에 하위 객체가 없었기 때문에.. 객체를 얕은 복사하는 방법도 괜찮았다.(나는 몰랐을 뿐.. 나중에 고치러 가야겠다.)  
알반적으로 하위객체까지 복사해야 할 일이 많지 않기 때문에 가장 많이 사용하는 방법이라고 한다.

# 깊은 복사(Deep Copy)

깊은 복사를 하는 방법도 여러가지가 있다고 한다.
그 중에서 내가 사용한 방법은 JSON 객체의 메소드를 이용하는 방법이다.

```javascript
let obj1 = {
  a: 1,
  b: {
    c: 1,
  },
};
let obj2 = JSON.parse(JSON.stringify(obj1));

obj2.a = 2;
obj2.b.c = 2;

console.log(obj1.a); // 1
console.log(obj1.b.c); // 1
```

객체를 스트링으로 변환했다가 다시 오브젝트로 변환하기 때문에 속도가 느리다는 단점이 있다. 그러나 하위 객체에 대해서도 확실히 복사할 수 있기 때문에 이런 면에서는 장점을 갖고 있다.

이렇게 삽질을 했는데 또 객체를 바로 대입하다가 문제가 발생했었다.
꼭 조심하도록 하자!!!

> 참고
> https://velog.io/@ddalpange/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EA%B0%9D%EC%B2%B4-%EB%B3%B5%EC%82%AC%ED%95%98%EA%B8%B0  
> https://m.blog.naver.com/wideeyed/221789258087  
> https://junwoo45.github.io/2019-09-23-deep_clone/
