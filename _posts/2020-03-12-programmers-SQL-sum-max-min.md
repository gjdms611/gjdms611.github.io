---
title: '[프로그래머스] SQL 고득점 Kit - SUM, MAX, MIN'
date: 2020-03-12 10:40:04 +0900
categories: [Programmers, SQL]
tags: [SQL]
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17043)

### 문제
[최댓값 구하기](#최댓값-구하기)<br>
[최솟값 구하기](#최솟값-구하기)<br>
[동물 수 구하기](#동물-수-구하기)<br>
[중복 제거하기](#중복-제거하기)<br>

### 최댓값 구하기
MAX()를 사용할 수 있는지 묻는 문제. 또한 컬럼명을 AS 혹은 그냥 띄어쓰기로 재정의할 수 있다. 아래 두 문장은 같은 출력 결과를 낸다.
```sql
SELECT DATETIME AS '시간' FROM ANIMAL_INS;
```
```sql
SELECT DATETIME '시간' FROM ANIMAL_INS;
```

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT MAX(DATETIME) AS '시간' FROM ANIMAL_INS;
```

</div>
</details>

### 최솟값 구하기
MIN()를 사용할 수 있는지 묻는 문제.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT MIN(DATETIME) AS '시간' FROM ANIMAL_INS;
```

</div>
</details>

### 동물 수 구하기
COUNT()를 사용할 수 있는지 묻는 문제.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT COUNT(ANIMAL_ID) AS count FROM ANIMAL_INS;
```

</div>
</details>

### 중복 제거하기
DISTINCT를 사용할 수 있는지 묻는 문제. 중복 제거시에 DISTINCT를 사용하면 된다. 또한 NULL인 데이터를 제거해야 할 경우 IS NOT NULL조건을 사용하면 NULL이 아닌 데이터만 골라서 출력할 수 있다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT COUNT(DISTINCT NAME) AS count
FROM ANIMAL_INS
WHERE NAME IS NOT NULL;
```

</div>
</details>