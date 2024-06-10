---
title: '[Codeforces] Codeforces Round #627 - C. Frog Jumps'
date: 2020-03-16 01:28:14 +0900
categories: [Algorithm, Codeforces]
tags: [C++]
---

[문제 링크](https://codeforces.com/problemset/problem/1324/C)

첫 위치와 마지막 도착지를 'R'이라고 두고 각 'R'과의 사이 중에서 최댓값을 출력한다.<br>
어차피 가장 마지막에 도달하기 위해서는 'R'을 이용해야만 하기 때문이다.

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
 
char str[200005];
 
int main(void) {
    int t;
    scanf("%d", &t);
    for (int T = 0; T < t; T++) {
        int last = -1, ans = 0;
        scanf("%s", &str);
        for (int i = 0; i < strlen(str); i++) {
            if (str[i] == 'R') {
                ans = max(ans, i - last);
                last = i;
            }
        }
        ans = max(ans, (int)strlen(str) - last);
        printf("%d\n", ans);
    }
    return 0;
}
```

</div>
</details>