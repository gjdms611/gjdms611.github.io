---
title: '[Codeforces] Codeforces Round #624 - B. WeirdSort'
date: 2020-02-25 22:19:24 +0900
categories: [Algorithm, Codeforces]
tags: [C++, 정렬]
seo:
  date_modified: 2020-03-05 05:02:41 +0900
---

[문제 링크](http://codeforces.com/contest/1311/problem/B)

버블소트를 구현하면 되는 문제다.<br>
문제를 해석하자면 두 개의 배열이 주어지며, 하나의 배열은 정렬이 필요한 배열, 나머지 하나는 swap이 가능한 인덱스가 주어진 배열이다.<br>
예를 들어 두번째 배열에 [1, 3]이 주어졌을 경우, 1과 2(1과 1+1), 그리고 3과 4(3과 3+1) 이렇게만 서로 원소를 바꿀 수 있다.<br><br>
나는 버블소트를 그대로 구현하고, 조건문으로 swap이 가능한지 따진 후 불가능하다면 NO를 출력하게 했다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```c++

#include <iostream>
#include <limits.h>
#include <algorithm>
#include <functional>
#include <vector>
#include <string.h>
#include <ctype.h>
#include <cmath>
#include <queue>
#include <stack>
#include <string>
#include <set>
#include <map>
using namespace std;
typedef tuple<int, int, int> T;
typedef pair<int, int> PII;
 
int main(void) {
	int t, n, m, a[105], dest[105];
	
	scanf("%d", &t);
	for (int T = 0; T < t; T++) {
		int aa;
		bool ck = true;
		bool p[105] = { false };
		scanf("%d %d", &n, &m);
		for (int i = 0; i < n; i++)
			scanf("%d", a + i);
		for (int i = 0; i < m; i++) {
			scanf("%d", &aa);
			p[aa-1] = true;
		}
 
		for (int j = 0; j < n - 1; j++) {
			for (int i = 0; i < n - 1; i++) {
				if (a[i] > a[i + 1]) {
					if (p[i]) swap(a[i], a[i + 1]);
					else {
						ck = false;
						break;
					}
				}
			}
		}
 
		for (int i = 0; i < n - 1; i++) {
			if (a[i] > a[i + 1]) {
				ck = false;
				break;
			}
		}
 
		printf("%s\n", ck ? "YES" : "NO");
	}
 
 
	return 0;
}
```

</div>
</details>