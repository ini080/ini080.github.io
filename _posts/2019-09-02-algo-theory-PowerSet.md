---
layout: post
title:  "부분집합(PowerSet)"
subtitle:   "PowerSet"
categories: Algorithm
tags: theory

---

### 부분집합 : 집합에 포함된 원소를 선택하는 것

예) {1,2,3} 의 부분 집합

{},{1},{2},{3},{1,2},{1,3},{2,3},{1,2,3}

=> 공집합 + 1개의 원소를 가지는 집합 + 2개의 원소를 가지는 집합 + 3개의 원소를 가지는 집합 => 각각은 조합 원소의 값과 같음 (3C0+3C1+3C2+3C3)

```java
static void powerSet(int[] arr, boolean[] visited, int n, int idx) {
    if(idx == n) {
        print(arr, visited, n);
        return;
    }

    visited[idx] = false;
    powerSet(arr, visited, n, idx + 1);

    visited[idx] = true;
    powerSet(arr, visited, n, idx + 1);
}
```

```java
3
2
2 3
1
1 3
1 2
1 2 3
```
