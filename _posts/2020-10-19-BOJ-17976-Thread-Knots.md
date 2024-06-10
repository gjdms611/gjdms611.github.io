---
title: '[BOJ] 17976 - Thread Knots'
date: 2020-10-19 19:18:52 +0900
categories: [Algorithm, BOJ]
tags: [그리디]
use_math: true
seo:
  date_modified: 2020-10-23 14:25:36 +0900
---

[[백준] 17976 - Thread Knots](https://www.acmicpc.net/problem/17976)<br>

## 아이디어
### 관점의 변화
이 문제는 관점에 따라 두가지 방법으로 접근할 수 있다.
- n개의 매듭을 잘 배치해서 최소 거리 중에 최대 거리가 되는 배치를 찾아내는 방법
	- 각각의 실의 길이는 최대 10억이고, 따라서 각 매듭을 배치하는 경우의 수가 10억이다.
	- 한 번 매듭을 배치하는 경우의 수가 10억이고, 이것이 n개로 반복되므로 단순히 완전탐색으로 문제를 해결할 때, 최악의 시간복잡도는 $O(l^n)$이다.

- 매듭 간의 최소 거리가 d일 때 n개의 매듭을 모두 배치할 수 있는지 여부를 확인하는 문제
	- 최소 거리가 d라고 가정하고 n개의 실을 탐색하며 매듭을 배치한다.
	- 가능한 d의 범위는 $x_i=0$인 실과 $x_j=10^9$, $l_j=10^9$인 실이 함께 주어지는 경우 최대 20억이다.
	- 따라서 단순히 완전탐색으로 문제를 해결할 때 최악의 시간복잡도는 $O(2*10^9n)$이다.

여기서 2번째 방식으로 문제를 해결한다고 생각하면, 이분탐색으로 문제를 해결해야겠구나 하는 생각이 들 것이다.      

사실 간단히 생각하면, n이 이렇게 크게 주어지는 경우에는 문제를 풀 때 O(n) 혹은 O(nlogn)정도에 해결을 해야 하고, 일반적으로 많이 사용하는 알고리즘에는 이분탐색이나 세그먼트 트리 등을 먼저 떠올리게 되므로 이분탐색..? 까지만 생각해도 머릿속에 느낌표가 몇 개 떠오를 것이라 생각한다.   

## 구현
우선 선의 시작점이 되는 x의 위치를 기준으로 모든 스레드를 정렬한다.   
거리가 가장 최소가 되는 경우는 0, 가장 클 수 있는 값은 $2x10^9$일 것이다. (0과 $2x10^9$에 점이 각각 있는 경우) 따라서 각각의 값을 L과 R로 설정한다.   
가장 시작점을 가장 앞에 있는 x로 지정한다. 점 사이의 거리가 가장 커지길 바라므로 양 끝에 위치한 스레드는 스레드의 가장 끝에 점을 배치해야 한다는 것은 직관적으로 알 수 있다.   
두 번째 스레드부터 마지막 점 + mid 이상의 위치에 점을 배치할 수 있는지 판단한다.   
만일 스레드의 끝점($x_i+l_i$)보다 마지막으로 배치한 점의 위치+mid가 더 크다면, 해당 스레드에는 점을 배치할 수 없다는 의미이므로 R을 mid로 옮긴다.   
모든 스레드에 점을 배치할 수 있었다면, mid에서도 배치가 가능하다는 의미이므로 L을 mid로 옮긴다.   

## 시간 복잡도
스레드를 정렬하는 시간 = O(nlogn)   
이분탐색을 진행할 때 각 탐색에서 소요되는 시간 = O(n)   
이분탐색을 진행하는 탐색 횟수 = O(logn)
=> 이분탐색을 진행하는 시간 = O(n*logn) = O(nlogn)   
따라서 O(nlogn)의 시간복잡도를 갖는다.


<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <functional>
using namespace std;
typedef long long ll;
typedef pair<ll, ll> PII;

ll n;
vector<PII> v;

int main(void) {
    scanf("%lld", &n);
    for (ll i = 0; i < n; i++) {
        ll x, l;
        scanf("%lld %lld", &x, &l);
        v.push_back({ x, x + l });
    }
    sort(v.begin(), v.end());
    ll L = 0, R = 2000000000;
    while (true) {
        ll m = ll(L + R) / 2LL;
        ll prev = v[0].first;
        bool ck = true;
        for (ll i = 1; i < n; i++) {
            if (v[i].second - prev < m) {
                ck = false;
                break;
            }
            prev = max(v[i].first, prev + m);
        }
        if (L == m) {
            if (ck) {
                m = R;
                prev = v[0].first;
                for (ll i = 1; i < n; i++) {
                    if (v[i].second - prev < m) {
                        ck = false;
                        break;
                    }
                    prev = max(v[i].first, prev + m);
                }
                if (ck) {
                    printf("%lld", R);
                }
                else {
                    printf("%lld", L);
                }
            }
            break;
        }
        else {
            if (ck) {
                L = m;
            }
            else {
                R = m - 1;
            }
        }
    }
    return 0;
}
```

</div>
</details>