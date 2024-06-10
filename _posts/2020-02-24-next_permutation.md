---
title: '[STL] next_permutation'
date: 2020-02-24 20:06:03 +0900
categories: [Algorithm, STL]
tags: [C++, STL, next_permutation]
seo:
  date_modified: 2020-03-03 12:35:54 +0900
---

next_permutation은 순열을 계산해준다!<br>

`<algorithm>` 헤더에 저장되어있는 함수입니다.<br>
사용법은(VS가 매우 친절하게 알려주긴 하지만,)

```c++
next_permutation(시작주소, 마지막 원소의 바로 다음 주소)
```

중요한 점은 이 때 next_permutation에 넣어주는 배열은 반드시 정렬된 상태에서 시작해야 한다는 것이다!!<br>
아마 정렬이라고 하는 것은 오름차순 정렬인 것으로 추측..(확실히 알아본 것은 아니다.)<br>
이 점을 모르고 사용했다가 틀렸던 슬픈 사건이 있었으니 꼭꼭 기억해두도록 하자.