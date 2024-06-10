---
title: '[Codeforces] Codeforces Round #627 - A. Yet Another Tetris Problem'
date: 2020-03-16 01:14:19 +0900
categories: [Algorithm, Codeforces]
tags: [Python]
---

[문제 링크](https://codeforces.com/problemset/problem/1324/A)

현재 테트리스 게임 내에 남아있는 블록의 상태가 주어질 때, 가로 1 세로 2짜리 블록만으로 모든 블록을 제거할 수 있는지 여부를 출력하면 된다.<br>
즉, 현재 남아있는 블록 중에서 세로 길이가 홀수인 블록이 있다면 불가능을 출력하면 된다.<br>
이 때 주의할 점은 이미 모든 줄이 채워진 부분은 사라질 수 있으므로 그것을 고려한 이후에 홀수높이가 존재하는지 판단해야 한다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```python
for t in range(int(input())):
    n = int(input())
    arr = [int(x) for x in input().split()]
    mn = min(arr)
    arr = [x-mn for x in arr]
    ck = True
    for i in arr:
        if i%2 :
            ck=False
            break
    print("YES" if ck else "NO")
```

</div>
</details>