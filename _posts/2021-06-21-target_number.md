---
title:  Target Number
author: JOSEOYEON
date:   2021-06-21 17:10:16
categories: [Algorithm,study]
tags: [Algorithm]
---

### **[1]** [프로그래머스타겟 넘버]


[문제]
![image](https://user-images.githubusercontent.com/46625602/122729115-c6219280-d2b3-11eb-9277-77e8ff78c78d.png)



[답안]

```python
def solution(numbers, target):
    answer = 0 # 개수 
    
    for i in range(2**len(numbers)) :    
        fin = 0 
        binary = list(str(format(i, '0'+ str(len(numbers)) +'b')))
        binary = [int(-1) if value=='0' else int(value) for value in binary]

        for j in range(len(numbers)) : 
            fin = fin + numbers[j]*binary[j]
        if fin == target : 
            answer = answer + 1
    return answer
```

2^n 승으로 모든 경우의 수를 다 구해서 target 이 맞는지 구하는 식이다. 

```python
from itertools import product
def solution(numbers, target):
    l = [(x, -x) for x in numbers]
    s = list(map(sum, product(*l)))
    return s.count(target)
```
product 를 사용한점, 그리고 map 으로 list 를 만들어서 count 로 target 의 개수를 return 했다. 제일 빠름

```python
def solution(numbers, target):
    if not numbers and target == 0 :
        return 1
    elif not numbers:
        return 0
    else:
        return solution(numbers[1:], target-numbers[0]) + solution(numbers[1:], target+numbers[0])
```
**** 
return 해서 분할로 풀어버렸다..
이진 트리 구조로 +,- 의 모든 경우의 수를 쪼갠 다음에 terget이 0 이 되는 tree의 노드의 수를 구해서 답안을 구했다. 


---

**[Reference]**

**[1]**  [https://programmers.co.kr/learn/courses/30/lessons/43165](https://programmers.co.kr/learn/courses/30/lessons/43165)

**[Python 순열, 조합, product - itertools]** [https://velog.io/@davkim1030/Python-%EC%88%9C%EC%97%B4-%EC%A1%B0%ED%95%A9-product-itertools](https://velog.io/@davkim1030/Python-%EC%88%9C%EC%97%B4-%EC%A1%B0%ED%95%A9-product-itertools)


