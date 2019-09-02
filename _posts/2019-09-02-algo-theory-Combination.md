---
layout: post
title:  "조합(Combination)"
subtitle:   "Combination"
categories: Algorithm
tags: theory
---

### 부분집합 :  n 개의 숫자 중에서 r 개의 수를 순서 없이 뽑는 경우를 말합니다.

예) [1, 2, 3] 이란 숫자 배열에서 2 개의 수를 순서 없이 뽑으면

[1, 2]
[1, 3]
[2, 3]

이렇게 3 개가 나옵니다.
순열을 뽑았을 때 나오는 [2, 1] [3, 1] [3, 2] 등은 중복이라 제거됩니다.


```java
public class Combination {
    public static void main(String[] args) {
    	// 5개중 3개 뽑기
        combination(new int[] {1,2,3,4,5}, new int[3], 0, 0);
    }

    static void combination(int[] arr, int[] temp, int n, int r) {
        if(n == temp.length) {
            for(int i = 0; i < temp.length; i++) {
                System.out.print(temp[i] + " ");
            }
            System.out.println();
            return ;
        }

        if(r == arr.length)  return ;

        // 선택 안하고 가기
        combination(arr, temp, n, r+1);

        //선택 하고 가기
        temp[n] = arr[r];
        combination(arr, temp, n+1, r+1);
    }
}
```

```java
3 4 5
2 4 5
2 3 5
2 3 4
1 4 5
1 3 5
1 3 4
1 2 5
1 2 4
1 2 3
```
