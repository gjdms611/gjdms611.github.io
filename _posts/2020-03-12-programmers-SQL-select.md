---
title: '[프로그래머스] SQL 고득점 Kit - SELECT'
date: 2020-03-12 10:10:41 +0900
categories: [Programmers, SQL]
tags: [SQL]
seo:
  date_modified: 2020-03-16 01:37:49 +0900
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17042)

### 문제
[모든 레코드 조회하기](#모든-레코드-조회하기)<br>
[역순 정렬하기](#역순-정렬하기)<br>
[아픈 동물 찾기](#아픈-동물-찾기)<br>
[어린 동물 찾기](#어린-동물-찾기)<br>
[동물의 아이디와 이름](#동물의-아이디와-이름)<br>
[여러 기준으로 정렬하기](#여러-기준으로-정렬하기)<br>
[상위 n개 레코드](#상위-n개-레코드)


### 모든 레코드 조회하기
기초적인 SELECT문을 사용할 줄 아는지 판단하는 문제.
ORDER BY로 정렬된 내용을 출력하는 것을 잊지 말아야 한다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT * FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

</div>
</details>

### 역순 정렬하기
내림차순으로 정렬하여 출력할 수 있는지 묻는 문제. 내림차순 정렬은 DESC를 통해 명시해주어야 한다는 것에 주의하자.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT NAME, DATETIME FROM ANIMAL_INS
ORDER BY ANIMAL_ID DESC;
```

</div>
</details>

### 아픈 동물 찾기
WHERE문을 통해 특정 조건에 해당하는 데이터만 골라 출력할 수 있는지 묻는 문제. 일부만 비교하는 것이 아니므로 단순 비교만으로 충분하다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE INTAKE_CONDITION = 'Sick';
```

</div>
</details>

### 어린 동물 찾기
NOT을 사용할 줄 아는지 묻는 문제. 보통 NOT을 앞에 붙이면 되는데, IS NOT NULL과 같은 경우만 주의하면 된다. 이 경우에는 영어문법과 같이 쓰면 되니까 그렇게 구분하자.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
WHERE NOT INTAKE_CONDITION = 'Aged';
```

</div>
</details>

### 동물의 아이디와 이름
원하는 컬럼의 데이터만 골라서 출력할 수 있는지 묻는 문제. SELECT문에 출력하고 싶은 컬럼명만 써주면 된다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID, NAME FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

</div>
</details>

### 여러 기준으로 정렬하기
두가지 이상의 기준으로 정렬하여 출력할 수 있는지 묻는 문제. 말 그대로 정렬 기준 순서대로 나열하면 된다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID, NAME, DATETIME FROM ANIMAL_INS
ORDER BY NAME, DATETIME DESC;
```

</div>
</details>

### 상위 n개 레코드
상위 N개만 출력할 수 있는지 묻는 문제.. 인데 나는 방법을 몰라서 그냥 서브쿼리를 사용해 해결했다. 이후에 LIMIT구문을 알게 되었다. 따라서 아래 코드는 답은 나오지만 효율성 측면에서는 그리 좋지는 않을 코드.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT NAME FROM ANIMAL_INS
WHERE DATETIME <= (SELECT MIN(DATETIME) FROM ANIMAL_INS);
```

</div>
</details>