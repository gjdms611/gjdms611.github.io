---
title: '[프로그래머스] 코딩테스트 고득점 Kit - [해시] 전화번호 목록'
date: 2020-03-12 14:16:59 +0900
categories: [Programmers, 코딩테스트 고득점 Kit]
tags: [c++, trie]
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42577)

내가 보기에는 KTX타고 지나가면서 봐도 trie문제인데.. 이게 왜 해시에 있는걸까.. 다른 풀이를 봐야할 듯 하다..

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```c++
#include <string>
#include <vector>
using namespace std;

struct trie {
    trie* arr[26];
    bool end;
    trie() {
        for (int i = 0; i < 26; i++) {
            arr[i] = NULL;
            end = false;
        }
    }
};

bool solution(vector<string> phone_book) {
    bool answer = true;
    trie* root = new trie();
    for (string s : phone_book) {
        trie* now = root;
        for (char i : s) {
            if (!(now->arr[i - '0'])) {
                now->arr[i - '0'] = new trie();
            }
            now = now->arr[i - '0'];
        }
        now->end = true;
    }
    for (string s : phone_book) {
        trie* now = root;
        for (int i = 0; i < s.size() - 1; i++) {
            now = now->arr[s[i] - '0'];
            if (now->end) {
                answer = false;
                break;
            }
        }
    }
    return answer;
}
```

</div>
</details>