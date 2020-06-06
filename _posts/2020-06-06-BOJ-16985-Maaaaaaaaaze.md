---
title: '[BOJ] 16985 - Maaaaaaaaaze'
date: 2020-06-06 21:24:22 +0900
categories: [Algorithm, BOJ]
tags: [C++, 구현, 완전탐색, BFS]
---

[[백준] 16985 - Maaaaaaaaaze](https://www.acmicpc.net/problem/16985)<br>

풀이 시간 : 97분째(모의고사라서 두 문제를 다 읽은 후 풀었다.)<br>

## 당황포인트 1_구현한것과 반대로 작동하는 코드
역시나 TC가 나오지 않아서 디버깅을 시작했는데 판을 회전하는 코드가 반대로 작동했다.<br>
난 분명 오른쪽으로 회전하는 코드를 짰는데 판은 왼쪽으로 회전하고 있었다.<br>
일단 일관적으로 회전하긴 해서 문제는 없었기 때문에 침착하게 반대방향으로 디버깅 조건을 걸었지만.. 만약 방향까지 신경써야 했다면 혹시 잘못 구현한 것일까봐 검증을 해보려고 꽤나 고생했을 것 같다고 생각했다.<br>

## 당황포인트 2_TC보다 너무 적게 나오는 답
당황포인트 2 때문에 너무 많은 길을 돌아갔다..<br>
정답은 미로의 입구가 1일 때만 BFS를 돌려야 한다는 것이었다.<br>
나는 설마 모든 경우의 수를 봐주지 못해서 이런 일이 생긴 것일수도 있다고 생각해 입구의 모든 경우의 수를 따지는 코드를 추가했다.<br>
추가하는 과정에서 위에서 말한 예외를 발견하고 처리해주어 잘 통과하긴 했는데..<br>
나중에 다시 확인해봤지만 처음 생각했던 것 처럼 미로를 만드는 과정에서 모든 경우의 수가 만들어지기 때문에 BFS는 각 미로당 한 번만 돌리면 된다..<br>
모든 입구를 확인 하는 코드를 지우면 *4가 사라지므로 실행시간이 1초가 넘던 코드가 0.4초로 조금은 더 짧아진다.<br>

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <queue>
#include <functional>
#define INF 987654321
using namespace std;
typedef tuple<int, int, int> T;

const int dr[6] = { 0,0,-1,1, 0, 0 }, dc[6] = { 1,-1,0,0, 0, 0 }, dz[6] = { 0,0,0,0,1, -1 };
const int start[4][3] = { {0,0,0}, {0,0, 4}, {0,4,0}, {0,4,4} }, dest[4][3] = { {4, 4, 4}, {4, 4, 0}, {4, 0, 4}, {4, 0, 0} };
int board[7][7][7], maze[7][7][7];

/*
find의 요구조건
3차원 bfs를 돌린다 끗
입구는 4군데가 있을 수 있다(나머지 4개의 꼭짓점은 결국 입구-출구 pair가 정해져있어서 의미x
그런데 결국 한군데로만 해도 미로를 만들 때 돌리는 과정에서 모든 경우의 수를 다 보니까 괜찮을 것 같다
*/

bool is_in_range(int x, int y, int z) {
	return x >= 0 && x < 5 && y >= 0 && y < 5 && z >= 0 && z < 5;
}

int find() {
	int rtn = INF;
	for (int k = 0; k < 4; k++) {
		int visited[7][7][7] = { 0, };
		queue<T> q;
		if (maze[start[k][0]][start[k][1]][start[k][2]] == 0) continue;
		q.push({ start[k][0], start[k][1], start[k][2] });
		visited[start[k][0]][start[k][1]][start[k][2]] = 1;
		while (!q.empty()) {
			int zz = get<0>(q.front()), xx = get<1>(q.front()), yy = get<2>(q.front());
			q.pop();
			for (int i = 0; i < 6; i++) {
				int z = zz + dz[i], x = xx + dr[i], y = yy + dc[i];
				if (is_in_range(x, y, z) && maze[z][x][y] == 1 && !visited[z][x][y]) {
					q.push({ z, x, y });
					visited[z][x][y] = visited[zz][xx][yy] + 1;
					if (z == dest[k][0] && x == dest[k][1] && y == dest[k][2]) rtn = visited[z][x][y];
				}
			}
		}
	}
	return rtn;
}

/*
make_maze의 요구조건
1. 각 판들을 얼만큼 회전할지 결정한다.
2. 판들의 회전이 결정되면 판들의 순서를 결정한다.
*/

int make_maze() { // 판을 배열해 미로를 만든다.
	int rtn = INF;
	int turn[5] = { 0, };
	while (turn[0] < 4) {
		//판을 배열한다.
		int sunser[5] = { 0,1,2,3,4 };
		do {
			for (int idx = 0; idx < 5; idx++) {
				for (int i = 0; i < 5; i++) {
					for (int j = 0; j < 5; j++) {
						int x = turn[sunser[idx]] == 0 ? i : turn[sunser[idx]] == 1 ? j :
							turn[sunser[idx]] == 2 ? 4 - i : 4 - j;
						int y = turn[sunser[idx]] == 0 ? j : turn[sunser[idx]] == 1 ? 4 - i :
							turn[sunser[idx]] == 2 ? 4 - j : i;
						maze[idx][i][j] = board[sunser[idx]][x][y];
					}
				}
			}
			rtn = min(rtn, find());
		} while (next_permutation(sunser, sunser + 5));

		// 판을 회전한다.
		turn[4]++;
		for (int i = 4; i > 0; i--) {
			if (turn[i] > 3) {
				turn[i] = 0;
				turn[i - 1]++;
			}
		}
	}
	return rtn == INF ? 0 : rtn;
}

int main(void) {
	for (int i = 0; i < 5; i++) {
		for (int j = 0; j < 5; j++) {
			for (int k = 0; k < 5; k++) {
				scanf("%d", board[i][j] + k);
			}
		}
	}

	printf("%d", make_maze() - 1);
	return 0;
}
```

</div>
</details>