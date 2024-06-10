---
title: '[BOJ] 17874 - Piece of Cake!'
date: 2020-08-30 00:48:21 +0900
categories: [Algorithm, BOJ]
tags: []
---

[[백준] 17874 - Piece of Cake!](https://www.acmicpc.net/problem/17874)<br>

인턴 생활이 끝난 기념으로 행복 코딩을 해보고 싶어서 푼 문제..   
높이는 4로 고정되어있으며, 길이가 n인 정사각형을 가장 왼쪽 위 사각형이 가로 v, 세로 h가 되도록 잘랐을 때 네 육면체 중 최대 부피를 출력하는 문제다.   
가로의 길이는 n-v, v중 2가지이고 세로의 길이는 n-h, h 중 2가지이므로 각각의 최대값과 높이 4를 곱한 값을 출력하면 된다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```c++
#include <iostream>
#include <algorithm>
using namespace std;

int main(void) {
	int n, h, v;
	scanf("%d %d %d", &n, &h, &v);
	printf("%d", 4 * max(n - v, v) * max(n - h, h));
	return 0;
}
```

</div>
</details>