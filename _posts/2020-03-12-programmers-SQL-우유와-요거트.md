---
title: '[프로그래머스] 우유와 요거트가 담긴 장바구니'
date: 2020-03-12 14:09:55 +0900
categories: [Programmers, SQL]
tags: [SQL]
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/62284)

나는 방법을 딱히 찾지 못해서 조인을 이용했다. 그러나 전부 담아야 하는 목록이 많아진다면 이 방법으로는 해결하기가 어렵다.. 무언가 효율이 좋은 방법을 차후에 찾아보는 것으로 하자.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT A.CART_ID
FROM (SELECT CART_ID FROM CART_PRODUCTS WHERE NAME = '우유') AS A,
    (SELECT CART_ID FROM CART_PRODUCTS WHERE NAME = '요거트') AS B
WHERE A.CART_ID = B.CART_ID;
```

</div>
</details>