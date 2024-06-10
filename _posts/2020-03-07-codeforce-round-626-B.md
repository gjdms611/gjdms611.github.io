---
title: '[Codeforces] Codeforces Round #626(Div.2) - B. Count Subrectangles'
date: 2020-03-07 22:45:44 +0900
categories: [Algorithm, Codeforces]
tags: [C++, 수학]
---

[문제 링크](https://codeforces.com/contest/1323/problem/B)

터지지 않도록 하기 위해 입력받을 때 연속된 1의 길이로 저장해 나누어지는 블록(구역?)별로 저장해 경우의 수를 구해주었다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```c++
#include <iostream>
#include <queue>
#include <algorithm>
#include <functional>
#include <vector>
#include <stack>
#include <map>
#include <set>
#include <string.h>
#define MAX 50000000
using namespace std;
typedef long long ll;
typedef pair<int, int> PII;

map<int, int> a, b;
map<PII, int> rect;

int main(void) {
    int n, m, k, t;
    scanf("%d %d %d", &n, &m, &k);
    ll cnt = 0;
    for (int i = 0; i < n; i++) {
        scanf("%d", &t);
        if (t) cnt++;
        else if (cnt) {
            a[cnt]++;
            cnt = 0;
        }
    }
    if (cnt) {
        a[cnt]++;
        cnt = 0;
    }
    for (int i = 0; i < m; i++) {
        scanf("%d", &t);
        if (t) cnt++;
        else if (cnt) {
            b[cnt]++;
            cnt = 0;
        }
    }
    if (cnt) {
        b[cnt]++;
        cnt = 0;
    }

    for (auto i : a)
        for (auto j : b)
            if (i.first * j.first >= k)
                rect[{min(i.first, j.first), max(i.first, j.first)}] += i.second * j.second;

    for (auto it : rect)
        for (int i = 1; i <= it.first.first; i++)
            if (!(k % i) && k / i <= it.first.second)
                cnt += (it.first.first - i + 1) * (it.first.second - (k / i) + 1) * it.second;

    printf("%lld", cnt);
    return 0;
}
```

</div>
</details>