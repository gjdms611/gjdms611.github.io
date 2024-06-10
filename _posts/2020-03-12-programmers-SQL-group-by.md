---
title: '[프로그래머스] SQL 고득점 Kit - GROUP BY'
date: 2020-03-12 11:35:38 +0900
categories: [Programmers, SQL]
tags: [SQL]
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17044)

## 문제
[고양이와 개는 몇 마리 있을까](#고양이와-개는-몇-마리-있을까)<br>
[동명 동물 수 찾기](#동명-동물-수-찾기)<br>
[입양 시각 구하기(1)](#입양-시각-구하기1)<br>
[입양 시각 구하기(2)](#입양-시각-구하기2)<br>

## 고양이와 개는 몇 마리 있을까
GROUP BY를 통해 특정 컬럼의 데이터를 기준으로 그룹을 묶어 데이터를 처리할 수 있는지를 묻는 문제.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_TYPE, COUNT(ANIMAL_ID) AS count
FROM ANIMAL_INS
GROUP BY ANIMAL_TYPE;
```

</div>
</details>

## 동명 동물 수 찾기
그룹함수는 SELECT문에서는 그냥 사용이 가능하지만, WHERE절에서는 사용이 불가능하다. 따라서 HAVING을 통해 따로 조건을 주어야 한다.
ORDER BY는 반드시 가장 마지막에 사용해야 함을 잊지 말것.(LIMIT 제외)

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT NAME, COUNT(ANIMAL_ID) AS COUNT FROM ANIMAL_INS
WHERE NAME IS NOT NULL
GROUP BY NAME
HAVING COUNT(ANIMAL_ID) >= 2
ORDER BY NAME;
```

</div>
</details>

## 입양 시각 구하기(1)
HOUR를 통해 DATETYPE을 변환할 수 있는지를 묻는 문제.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT HOUR(DATETIME) AS HOUR, COUNT(ANIMAL_ID) AS COUNT
FROM ANIMAL_OUTS
GROUP BY HOUR
HAVING HOUR BETWEEN 9 AND 19
ORDER BY HOUR;
```

</div>
</details>

## 입양 시각 구하기(2)
어떻게 풀어야 할지 몰라 고통받다가 [구글링](https://codingmoonkwa.tistory.com/26)을 통해 해결했다.<br>
흥미로운 점은 DECLARE를 통해 변수를 선언하지 않고 바로 SET을 사용해도 오류가 나지 않는다는 점이다.(몰랐음)<br>
또한 그냥 아무데서나 저렇게 변수를 선언해 활용할 수 있다는 점 또한 인상깊었다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SET @hour := -1;
SELECT (@hour:=@hour+1) AS HOUR,
    (SELECT COUNT(*) FROM ANIMAL_OUTS
     WHERE HOUR(DATETIME) = @hour) AS COUNT
FROM ANIMAL_OUTS
WHERE @hour < 23;
```

</div>
</details>