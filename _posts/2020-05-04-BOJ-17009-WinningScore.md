---
title: '[BOJ] 17009 - Winning Score'
date: 2020-05-04 13:37:09 +0900
categories: [Algorithm, BOJ]
tags: [node.js]
---

[[백준] 17009 - Winning Score](https://www.acmicpc.net/problem/17009)<br>

여러줄 입력을 받을 수 있어야 한다. 근데 원래 node.js로 여러줄 입력 받으려면 이렇게 해야 하는걸까? 다른 사람들 코드를 참고해보고 싶은데 js로 풀이한 사람이 별로 없는 것 같다. 종종 찾아봐야겠다.

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```javascript
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});
let sumA=0;
let sumB=0;
let i=0;
rl.on('line', function(line) {
    if(i<3) sumA+=line*(3-i);
    else sumB+=line*(6-i);
    i+=1;
}).on("close", function() {
    console.log(sumA>sumB?"A":sumA<sumB?"B":"T");
    process.exit();
});
```

</div>
</details>