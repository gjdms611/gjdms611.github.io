---
title: '[Codeforces] Codeforces Round #627 - B. Yet Another Palindrome Problem'
date: 2020-03-16 01:17:59 +0900
categories: [Algorithm, Codeforces]
tags: [C++]
---

[문제 링크](https://codeforces.com/problemset/problem/1324/B)

배열이 주어질 때 해당 배열의 부분배열이 팰린드롬이 될 수 있는지를 판단하는 문제.<br>
완전 탐색으로 현재 위치부터 두 칸 뒤부터 동일한 원소가 하나라도 존재하면 반드시 YES.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```c++
#include <string>
#include <vector>
#include <map>
#include <algorithm>
#include <iostream>
#include <cmath>
#include <queue>
#include <functional>
#include <string.h>
#include <ctype.h>
#include <stack>
#include <set>
#include <stack>
using namespace std;
 
int arr[5005], n;
int tmp[3];
 
int main(void) {
    int t;
    scanf("%d", &t);
    for (int T = 0; T < t; T++) {
        memset(arr, 0, sizeof(arr));
        scanf("%d", &n);
        for (int i = 0; i < n; i++) {
            scanf("%d", arr + i);
        }
        bool ck = false;
        for (int i = 0; i < n; i++) {
            for (int j = i + 2; j < n; j++) {
                if (arr[i] == arr[j]) ck = true;
            }
        }
        printf("%s\n", ck ? "YES" : "NO");
    }
    return 0;
}
```

</div>
</details>