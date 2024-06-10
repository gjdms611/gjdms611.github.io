---
title: '[Codeforces] Codeforces Round #627 - D. Pair of Topics'
date: 2020-03-16 01:37:09 +0900
categories: [Algorithm, Codeforces]
tags: [C++, upper_bound]
seo:
  date_modified: 2020-03-27 13:21:41 +0900
---

[문제 링크](https://codeforces.com/problemset/problem/1324/D)

조건식에서 오른쪽을 모두 왼쪽으로 넘겨서 정리하면, (a<sub>i</sub>-b<sub>i</sub>)+(a<sub>j</sub>-b<sub>j</sub>)>0이 된다.<br>
즉, 배열을 하나로 정리할 수 있다.<br>
또한 i와 j의 순서는 결국 상관이 없게되기 때문에 배열을 정렬해도 문제가 없다.<br>
이제 1 이상인 배열의 갯수는 <sub>n</sub>C<sub>2</sub>, 즉 (n*(n-1))/2로 계산해주면 된다.<br>
음수의 경우 upper_bound를 이용해 합해서 양수가 되는 지점을 찾아 그 갯수를 더해주었다.

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
typedef long long ll;
 
vector<ll> arr;
 
int main(void) {
    ll n, a, ans = 0;
    scanf("%lld", &n);
    for (int i = 0; i < n; i++) {
        scanf("%lld", &a);
        arr.push_back(a);
    }
    for (int i = 0; i < n; i++) {
        scanf("%lld", &a);
        arr[i] -= a;
    }
    sort(arr.begin(), arr.end());
    for (int i = 0; i < n; i++) {
        if (arr[i] > 0) {
            ans += (n - i) * (n - i - 1) / 2;
            break;
        }
        else {
            ans += arr.end() - upper_bound(arr.begin() + i, arr.end(), -arr[i]);
        }
    }
    printf("%lld", ans);
    return 0;
}
```

</div>
</details>