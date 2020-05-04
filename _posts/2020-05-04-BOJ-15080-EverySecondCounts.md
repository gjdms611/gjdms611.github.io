---
title: '[BOJ] 15080 - Every Second Counts'
date: 2020-05-04 13:48:38 +0900
categories: [Algorithm, BOJ]
tags: [node.js]
---

[[백준] 15080 - Every Second Counts](https://www.acmicpc.net/problem/15080)<br>

<details>
  <summary> 소스코드 </summary>
    <div markdown="1">

```javascript
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});
let i=0;
let start=[];
let end=[];
rl.on('line', function(line) {
    if(i==0){
        start=line.split(' : ');
    }
    else if(i==1){
        end = line.split(' : ');
    }
    i+=1;
}).on("close", function() {
    let ans=0;
    ans+=(end[0]-start[0])*3600;
    ans+=(end[1]-start[1])*60;
    ans+=end[2]-start[2];
    if(ans<0) ans+=24*3600;
    console.log(ans);
    process.exit();
});
```

</div>
</details>