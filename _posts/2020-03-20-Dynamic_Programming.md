---
layout: post
title:  "Dynamic Programming "
date:   2020-03-20 19:22:31
categories: [Algorithm, All]
---

다이나믹 프로그램이랑 `하나의 문제는 단 한번만 풀도록`하는 알고리즘이다. 

1. 큰 문제를 작은 문제로 나눌 수 있다.
2. 작은 문제에서 구한 정답은 큰 문제에도 포함된다.

이 두가지 조건이 만족한다면 다이나믹 프로그래밍을 적용할 수 있다.

<BR/>

다이나믹 프로그램의 꽃은 당연 `점화식`을 찾는 것이다. 문제로 점화식을 찾을 수 있다면, 식을 세우고 작은 문제를 배열에 저장하여 더 큰 인덱스의 값을 찾는데 이 점화식을 사용한다.

<BR/>

예제에 해당하는 백준 문제를 한번 보자면
   
<BR/>  

### 타일링 문제


![image](https://user-images.githubusercontent.com/46625602/77155875-8e8ccf00-6ae1-11ea-965a-bab6ccffc28f.png)


이런 문제의 경우 다음 과 같이 분할 할 수 있는데 

<BR/>

n(큰 문제)의 해답을 찾으려고 할때 우리는 문제의 크기를 n-1 + 1로 쪼갤 수 있다. 1문제의 해답은, 타일 1개를 놓는 경우의 수는 1 이므로 1이다.

<BR/>

![image](https://user-images.githubusercontent.com/46625602/77155915-a401f900-6ae1-11ea-8b8a-8d1996c64260.png)


또한 n-2 + 2 로도 쪼갤 수 있는데, 타일 2개를 놓는 양상이 타일 1개를 놓는 문제로 쪼개어 질수 없는 양상의 경우의 수는 2개이다. 

<BR/>

따라서 다음과 같은 점화식을 찾을 수 있다. 

```c
D[I] = D[I-1] + 2*D[I-2];
```

2를 곱해준 이유는 타일 2개를 붙여 놓는 경우의 수가 2개 이기 때문이다. 

해당 문제의 풀이는 다음과 같다.

```c
#include<stdio.h>

int d[1001];

int dp(int n) {
    if(n == 1) return 1;
    if(n == 2) return 3;
    if(d[n] != 0) return d[n];
    return d[n] = (dp(n-1) + 2*dp(n-2)) % 10007;
}

int main() {
    int n ;
    scanf("%d",&n);
    int res = dp(n);
    printf("%d",res);
    return 0;
} 
```

---


**Refference:**

* dynamic programming : [https://blog.naver.com/PostView.nhn?blogId=ndb796&logNo=221233570962&parentCategoryNo=&categoryNo=&viewDate=&isShowPopularPosts=false&from=postView](https://blog.naver.com/PostView.nhn?blogId=ndb796&logNo=221233570962&parentCategoryNo=&categoryNo=&viewDate=&isShowPopularPosts=false&from=postView)

* dynamic programming 2 : [https://blog.naver.com/PostView.nhn?blogId=ndb796&logNo=221233586932&parentCategoryNo=&categoryNo=&viewDate=&isShowPopularPosts=false&from=postView](https://blog.naver.com/PostView.nhn?blogId=ndb796&logNo=221233586932&parentCategoryNo=&categoryNo=&viewDate=&isShowPopularPosts=false&from=postView)
