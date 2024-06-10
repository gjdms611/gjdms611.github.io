---
title: '[프로그래머스] SQL 고득점 Kit - JOIN'
date: 2020-03-12 11:41:19 +0900
categories: [Programmers, SQL]
tags: [SQL]
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17046)

### 문제
[없어진 기록 찾기](#없어진-기록-찾기)<br>
[있었는데요 없었습니다](#있었는데요-없었습니다)<br>
[오랜 기간 보호한 동물(1)](#오랜-기간-보호한-동물1)<br>
[보호소에서 중성화한 동물](#보호소에서-중성화한-동물)<br>

### 없어진 기록 찾기
LEFT JOIN을 사용할 수 있는지 묻는 문제. LEFT JOIN은 묵시적인 방법으로는 사용이 불가하므로 반드시 명시해주어야 한다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT OUTS.ANIMAL_ID, OUTS.NAME
FROM ANIMAL_OUTS AS OUTS LEFT JOIN ANIMAL_INS AS INS
ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE INS.ANIMAL_ID IS NULL
ORDER BY OUTS.ANIMAL_ID;
```

</div>
</details>

### 있었는데요 없었습니다
INNER JOIN을 사용할 수 있는지 묻는 문제. 기본적인 묵시적 조인은 INNER JOIN이므로 묵시적 방법을 사용해도 된다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT INS.ANIMAL_ID, INS.NAME
FROM ANIMAL_INS AS INS JOIN ANIMAL_OUTS AS OUTS
ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE INS.DATETIME > OUTS.DATETIME
ORDER BY INS.DATETIME;
```

</div>
</details>

### 오랜 기간 보호한 동물(1)  
상위 N개의 데이터를 출력하는 방법으로 LIMIT를 사용했다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT INS.NAME, INS.DATETIME
FROM ANIMAL_INS AS INS LEFT JOIN ANIMAL_OUTS AS OUTS 
ON INS.ANIMAL_ID = OUTS.ANIMAL_ID
WHERE OUTS.DATETIME IS NULL
ORDER BY INS.DATETIME LIMIT 3;
```

</div>
</details>

### 보호소에서 중성화한 동물
두 테이블에 각각 조건을 걸어 조인할 수 있는지 묻는 문제이다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT INS.ANIMAL_ID, INS.ANIMAL_TYPE, INS.NAME
FROM ANIMAL_INS AS INS, ANIMAL_OUTS AS OUTS
WHERE INS.ANIMAL_ID = OUTS.ANIMAL_ID
    AND INS.SEX_UPON_INTAKE LIKE 'Intact%'
    AND OUTS.SEX_UPON_OUTCOME NOT LIKE 'Intact%'
ORDER BY INS.ANIMAL_ID;
```

</div>
</details>