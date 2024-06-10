---
title: '[Codeforces] Codeforces Round #624 - C. Perform the Combo'
date: 2020-02-25 22:25:52 +0900
categories: [Algorithm, Codeforces]
tags: [C++, 구간합]
seo:
  date_modified: 2020-03-05 05:02:41 +0900
---

[문제 링크](http://codeforces.com/contest/1311/problem/C)

주어진 인덱스까지 각 알파벳이 몇 번 나왔는지를 계속 더해서 최종 결과값을 출력하는 문제다.<br>
구간합을 구한다는 발상까지는 좋았지만 초기화에서 자꾸 시간초과가 나서 많은 고통을 받았다.<br>
벡터를 쓴 것 까지는 좋았으나 n까지 있는 배열을 만들어야 할 것을 자꾸 20만개까지의 배열을 생성하여 시간초과의 늪에 빠져들었다.<br>
지금 생각하는 것인데 n이 20만개인 테스트 케이스만 1000개 있는 테스트 케이스가 있었다면 아마 다시 시간초과가 났을텐데..<br>
오픈 해킹이 끝난 후에도 살아남아있는 것을 보아 이 문제의 난이도를 그렇게까지 높이고 싶지 않았거나 혹은 다른 이들도 이렇게 바꾸면 시간초과가 나는 방법을 썼던 것이 아닌가 싶다.<br><br>
풀이 방법은 각 알파벳별로 각 인덱스만큼의 크기를 가진 구간합 배열을 만들고(결국 2차원 배열을 만든다는 소리다.) 구간합을 쭉 구한 후에 m만큼 돌면서 구간합에 저장되어있는 값을 알파벳마다 다 더해주면 된다!<br>
여담으로 파이썬으로 리스트 슬라이싱을 사용하여 내봤는데 나중에 알고보니 그게 그만큼의 크기를 가진 배열을 다시 만드는 것이라 엄청나게 오래걸린다고 한다. 안타깝다.

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
 
int p[200005];
char str[200005];
 
int main(void) {
	int t, n, m;
	scanf("%d", &t);
	for (int T = 0; T < t; T++) {
		int ans[26] = { 0, };
		vector<int> sum[26];
		scanf("%d %d", &n, &m);
		for (int i = 0; i < 26; i++)
			sum[i].resize(n, 0);
		scanf("%s", str);
		for (int i = 0; i < m; i++) {
			scanf("%d", p + i);
		}
 
		// 구간합 구하기
		sum[str[0] - 'a'][0]++;
		for (int i = 1; i < n; i++) {
			for (int j = 0; j < 26; j++) {
				sum[j][i] = sum[j][i - 1];
			}
			sum[str[i] - 'a'][i]++;
		}
 
		for (int i = 0; i < m; i++) {
			for (int j = 0; j < 26; j++) {
				ans[j] += sum[j][p[i] - 1];
			}
		}
 
		for (int i = 0; i < 26; i++) {
			printf("%d ", ans[i] + sum[i][n - 1]);
		}
		printf("\n");
	}
	return 0;
}
```

</div>
</details>