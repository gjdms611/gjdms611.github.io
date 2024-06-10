---
title: '[프로그래머스] SQL 고득점 Kit - String, Date'
date: 2020-03-12 14:05:23 +0900
categories: [Programmers, SQL]
tags: [SQL]
seo:
  date_modified: 2020-03-12 14:17:07 +0900
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17042)

## 문제
[루시와 엘라 찾기](#루시와-엘라-찾기)   
[이름에 el이 들어가는 동물 찾기](#이름에-el이-들어가는-동물-찾기)   
[중성화 여부 파악하기](#중성화-여부-파악하기)   
[오랜 기간 보호한 동물(2)](#오랜-기간-보호한-동물2)   
[DATETIME에서 DATE로 형 변환](#datetime에서-date로-형-변환)   


## 루시와 엘라 찾기
조건문에서 String형식으로 된 데이터를 처리할 수 있는지 보는 문제인 것 같은데.. 사실 앞에서도 비슷한게 나왔어서 왜 있는지는 잘..

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME ='Lucy' OR NAME = 'Ella' OR
    NAME = 'Pickle' OR NAME = 'Rogan'
    OR NAME = 'Sabrina' OR NAME = 'Mitty';
```

</div>
</details>

## 이름에 el이 들어가는 동물 찾기
대소문자 구분 없이 스트링을 비교할 수 있는지 묻는 문제. 일일이 다 치려다가 효율적인 방법이 있을 것 같아서 찾아봤더니 UPPER를 사용하는 간단한 방법이 있었다. 강아지만 출력해야 한다는 점에 주의하라.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE UPPER(NAME) LIKE '%EL%' AND ANIMAL_TYPE = 'Dog'
ORDER BY NAME;
```

</div>
</details>

## 중성화 여부 파악하기
검색을 통해 CASE-WHEN-THEN구문을 알게 되었는데, 조건문에서 LIKE를 사용할 수 없어 곤란했다.<br>
분명 다른 방법이 더 있을 것 같은데..

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID, NAME,
  (CASE SEX_UPON_INTAKE
  WHEN 'Intact Male' THEN 'X'
  WHEN 'Intact Female' THEN 'X' ELSE 'O' END) AS '중성화'
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

</div>
</details>

## 오랜 기간 보호한 동물(2)
그냥 두 수의 차를 바로 대입해주면 된다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT INS.ANIMAL_ID, INS.NAME
FROM ANIMAL_INS AS INS, ANIMAL_OUTS AS OUTS
WHERE INS.ANIMAL_ID = OUTS.ANIMAL_ID
ORDER BY OUTS.DATETIME - INS.DATETIME DESC
LIMIT 2;
```

</div>
</details>

## DATETIME에서 DATE로 형 변환
DATE_FORMAT을 이용해 형변환을 할 수 있는지 묻는 문제. 다 외우기는 어렵겠지만 대충 무엇이 있는지 적혀있는 표 정도는 소장해두도록 하자.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```sql
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, '%Y-%m-%d') AS '날짜'
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

</div>
</details>