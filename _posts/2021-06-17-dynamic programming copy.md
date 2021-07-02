---
title:  "Dynamic Programming - 안경잡이 개발자"
author: JOSEOYEON
date:   2021-06-17 10:16:54
categories: [Algorithm, Algorithm]
tags: [Algorithm]
---

**[1]** 다이나믹 프로그래밍 타일링 문제 풀어보기

### 다이나믹 프로그래밍
```c
#include <stdio.h>

int d[100]; 

int dp(int x) {
    if (x == 1) return 1;
    if (x == 2) return 1;
    if (d[x] != 0) return d[x];
    return d[x] = dp(x-1) + dp(x-2);
}

int main(void){
    printf("%d", dp(30));
}
```

### 다이나믹 프로그래밍 타일링 문제 풀어보기

1. 문제를 이해한다
2. 점화식을 세운다 



---

**[Reference]**

**[1]**  [https://www.youtube.com/watch?v=YHZiWaL49HY&list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz&index=22](https://www.youtube.com/watch?v=YHZiWaL49HY&list=PLRx0vPvlEmdDHxCvAQS1_6XV4deOwfVrz&index=22)


