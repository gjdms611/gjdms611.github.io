---
title: '[프로그래머스] SQL 고득점 Kit - GROUP BY'
date: 2020-03-12 13:41:43 +0900
categories: [Programmers, SQL]
tags: [SQL]
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17045)

## 문제
[이름이 없는 동물의 아이디](#이름이-없는-동물의-아이디)<br>
[이름이 있는 동물의 아이디](#이름이-있는-동물의-아이디)<br>
[NULL 처리하기](#null-처리하기)<br>

## 이름이 없는 동물의 아이디
IS NULL조건을 사용할 수 있는지 묻는 문제.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID FROM ANIMAL_INS
WHERE NAME IS NULL;
```

</div>
</details>

## 이름이 있는 동물의 아이디
IS NOT NULL을 사용할 수 있는지 묻는 문제.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID;
```

</div>
</details>

## NULL 처리하기
IFNULL()을 사용할 수 있는지 묻는 문제.
```sql
IFNULL(컬럼명, 대체할 내용)
```

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_TYPE, IFNULL(NAME, 'No name') AS NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS;
```

</div>
</details>