---
title: '[BOJ] 18809 - Gaaaaaaaaaarden'
date: 2020-06-04 22:21:38 +0900
categories: [Algorithm, BOJ]
tags: [C++, 구현, 완전탐색]
seo:
  date_modified: 2020-06-06 22:00:11 +0900
---

[[백준] 18809 - Gaaaaaaaaaarden](https://www.acmicpc.net/problem/18809)<br>

풀이 시간 : 2시간 50분정도<br>
아이디어를 떠올리는데는 크게 어렵지 않았지만 문제를 풀면서 다음과 같은 문제에 부딪혔다.<br>

## 모든 경우의 수를 확인해주지 못하는 경우
~~경우가 필요 이상으로 많아 보이는 것은 넘어가자..~~<br>
처음에는 재귀함수를 통해 2차원 배열에 직접 r와 g를 표시해준 다음 돌려주었는데, 그 과정에서 조합의 경우의 수를 제대로 따져주지 못하는 문제가 발생했다.<br>
그 해결책으로 생각했던 것이 바로 next_permutation이었는데..<br>

## 중복되는 경우의 수를 거르지 못하는 경우
처음에는 배양액을 뿌릴 수 있는 땅을 모두 vector에 저장해둔 다음 next_permutation으로 무작정 돌려 모든 순열의 경우를 확인해주었다. 그러나 뿌릴 수 있는 배양액의 숫자와 땅의 숫자는 다를 수 있으므로 그럴 경우 필요하지 않은 중복된 경우까지 일일이 BFS로 확인하는 것을 디버깅 하는 중에 발견하고 말았다. 이에 대한 해결책으로 제시된 것이 바로 현재 코드의 형태다.<br>
우선 재귀함수로 배양액을 뿌릴 수 있는 수 만큼만 뽑아 vector로 만들어준 다음 그 vector를 보내주었다. 그 다음 다시 vector를 next_permutation으로 무작정 돌려주었는데 디버깅을 하던 도중 여전히 중복 문제가 확인되지 않았다는 것을 깨달았다. 바로 어차피 뿌릴 수 있는 배양액의 종류는 2종류이므로 중복되는 원소가 많이 있는데, 일일이 순열의 모든 종류를 확인하면서 중복되는 경우를 엄청나게 많이 실행하고 있던 것이다.<br>
이 문제를 해결하기 위해 다시 color라는 배열의 각각의 r과 g만큼의 값을 넣어준 다음 color배열이 가능한 순열의 경우의 수를 돌려 주는 것으로 해결했다.

## 꽃이 핀 땅을 제대로 처리하지 못해준 경우
이것은 아직 이유를 완전히 찾아내지 못한 문제다.<br>
10번 TC가 자꾸 25로 출력되어 머리를 싸매며 별별 바리에이션을 모두 시도하던 도중 찾아낸 문제인데..<br>
처음에는 꽃이 피어나면 그냥 땅을 INF값으로 바꿔주기만 했다. 이유는 어차피 두 땅의 시간을 비교하는 과정에서 두 땅의 시간이 같을 수가 없기 때문에 배양액이 뿌려져있지 않다는 것을 표현할 수 있다고 생각했기 때문이다. 그러나 왜인지 따로 꽃이 핀 땅의 값을 지정한 후 해당 값이 아닐 때만 꽃이 필 수 있다는 것을 조건으로 명시해준 경우와 그렇지 않은 경우의 출력이 다르게 나온다...

## 꽃이 필 경우 배양액을 뿌리지 않는 예제를 처리하지 못한 경우
이제 TC는 모두 잘 나오는데 답은 계속하여 틀렸습니다를 내뱉는다. 고통스럽다. 문제를 풀기 시작한지 벌써 2시간이나 지났다.<br>
1시간쯤 고통받다가 문제를 해결했는데, 결국 예외처리를 미처 못해준 것이 원인이었다. 꽃이 피었을 때 확인을 하지 않는 것만 신경쓰고 꽃이 핀 땅은 배양액이 사라져 주변 땅을 확인하지 않아야 하는 것은 처리해주지 않았다.(43번째줄)<br>
그렇지만 결국 해결했다.. 이 문제만 3시간이나 풀었지만...

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <queue>
#include <string.h>
#define CUT 1000000
using namespace std;
typedef pair<int, int> PII;

const int dr[4] = { 0, 0, -1, 1 }, dc[4] = { 1, -1, 0, 0 };
int garden[55][55], n, m, g, r;
vector<PII> v;
vector<int> color;

bool is_in_range(int x, int y) {
	return x >= 0 && x < n&& y >= 0 && y < m;
}

int get_time(int x) {
	if (x > CUT) return x - CUT;
	return x;
}

bool color_is_different(int x, int y) {
	if (x > CUT && y < CUT) return true;
	else if (y > CUT && x < CUT) return true;
	else return false;
}

int seed(vector<PII> seedwater) {
	int rtn = 0;
	do {
		int flower = 0, ck[55][55] = { 0, };
		queue<PII> q;
		for (int i = 0; i < seedwater.size(); i++) {
			ck[seedwater[i].first][seedwater[i].second] = color[i];
			q.push(seedwater[i]);
		}

		while (!q.empty()) {
			int now_x = q.front().first, now_y = q.front().second;
			q.pop();
			if (ck[now_x][now_y] == -1) continue;
			for (int i = 0; i < 4; i++) {
				int next_r = now_x + dr[i], next_c = now_y + dc[i];
				if (is_in_range(next_r, next_c) && garden[next_r][next_c] != 0) {
					if (ck[next_r][next_c] == 0) {
						q.push({ next_r, next_c });
						ck[next_r][next_c] = ck[now_x][now_y] + 1;
					}
					else if (ck[next_r][next_c] != -1 && color_is_different(ck[next_r][next_c], ck[now_x][now_y]) &&
						(get_time(ck[next_r][next_c]) == get_time(ck[now_x][now_y] + 1))) {
						ck[next_r][next_c] = -1;
						flower++;
					}
				}
			}
		}
		rtn = max(flower, rtn);
	} while (next_permutation(color.begin(), color.end()));
	return rtn;
}

int choose(int idx, vector<PII> tmp) {
	int rtn = 0;
	if (tmp.size() > r + g) return 0;
	if (tmp.size() == r + g) {
		sort(color.begin(), color.end());
		return seed(tmp);
	}
	for (int i = idx; i < v.size(); i++) {
		vector<PII> tmp2;
		tmp2 = tmp;
		tmp2.push_back(v[i]);
		rtn = max(rtn, choose(i + 1, tmp2));
	}
	return rtn;
}

int main(void) {
	scanf("%d %d %d %d", &n, &m, &g, &r);
	for (int i = 0; i < g; i++) {
		color.push_back(1);
	}
	for (int i = 0; i < r; i++) {
		color.push_back(CUT + 1);
	}
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < m; j++) {
			scanf("%d", garden[i] + j);
			if (garden[i][j] == 2) v.push_back({ i, j });
		}
	}

	printf("%d", choose(0, vector<PII>()));
	return 0;
}
```

</div>
</details>