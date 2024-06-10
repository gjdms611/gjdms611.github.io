---
title: '[프로그래머스] 코딩테스트 고득점 Kit - [해시] 완주하지 못한 선수'
date: 2020-03-12 14:14:06 +0900
categories: [Programmers, 코딩테스트 고득점 Kit]
tags: [c++, 해시]
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42576)

map을 이용하여 각 이름마다 완주한 선수들이 몇명인지 세주고, 참가자 명단에서 비교하며 완주한 사람이 더 적으면 그 이름을 return했다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```c++
#include <string>
#include <vector>
#include <map>
using namespace std;

map<string, int> ck;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";
    for(string s:completion)
        ck[s]++;
    for(string s:participant){
        if(ck[s]) ck[s]--;
        else{
            answer = s;
            break;
        }
    }
    return answer;
}
```

</div>
</details>