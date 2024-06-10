---
title: '[Codeforces] Codeforces Round #624 - A. Add Odd or Subtract Even'
date: 2020-02-25 22:14:06 +0900
categories: [Algorithm, Codeforces]
tags: [Python]
seo:
  date_modified: 2020-03-05 05:02:41 +0900
---

[문제 링크](http://codeforces.com/contest/1311/problem/A)

이번 대회의 등록문제.<br>
문제를 해석하자면, 두 개의 수가 주어졌을 때 a를 b와 같게 만들기 위해 몇 번의 계산을 거쳐야 하는지 출력하는 문제다.<br>
덧셈은 홀수만, 뺄셈은 짝수만 가능하다.<br>
즉 a가 b보다 작을 경우 홀수 차가 나면 1번 만에, 짝수차가 나면 차-1 + 1 이렇게 두 번만에 가능하다!<br>
a가 b보다 클 경우에도 비슷한 방식으로 답을 구할 수 있다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```python

import sys
def input(): return sys.stdin.readline().rstrip()
 
for T in range(int(input())):
    a, b = map(int, input().split())
    if a==b:
        print(0)
    elif a>b:
        if (b-a)%2:
            print(2)
        else :
            print(1)
    else:
        if (a-b)%2:
            print(1)
        else:
            print(2)
```

</div>
</details>