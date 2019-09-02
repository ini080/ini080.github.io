---
layout: post
title:  "순열(Permutation)"
subtitle:   "Permutation"
categories: Algorithm
tags: theory
---

### 부분집합 :  n 개의 값 중에서 r 개의 숫자를  다른 순서로 뒤섞는 연산을 말합니다.

예) [1, 2, 3] 이란 숫자 배열이 있을 때, 출력은 다음과 같습니다.

[1,2,3]
[1,3,2]
[2,1,3]
[2,3,1]
[3,2,1]
[3,1,2]

기준점(pivot)이 되는 배열의 인덱스를 제공하면,
해당 인덱스의 뒤쪽에 있는 값들과 위치를 변경후 기준점을 다음의 위치로 옮겨 다시 호출하는 순서로 진행한다.

* 순열은 문자열의 길이이 따라 n! 로 시간이 걸리게 된다.
  문자열의 길이가 20, 30 개가 된다면 시간이 굉장히 오래 걸리게 된다.

출처 : [https://118k.tistory.com/267 ](https://118k.tistory.com/267)
```java
public class Permutation {
    public static void main(String[] args) {
      int[] arr2 = {1,2,3};
      permutation(arr2, 0);
  }

  static void permutation(int[] arr, int idx) {
      if(idx == arr.length) {
          for(int i = 0; i < arr.length; i++) {
              System.out.print(arr[i] + " ");
          }
          System.out.println();
          return ;
      }

      for(int i = idx; i< arr.length; i++) {
          swap(arr, i, idx);
          permutation(arr, idx+1);
          swap(arr, i, idx);
      }
  }

  static void swap(int[] arr, int a, int b) {
      int tmp = arr[a];
      arr[a] = arr[b];
      arr[b] = tmp;
  }
}
```

```java
1 2 3
1 3 2
2 1 3
2 3 1
3 2 1
3 1 2
```
