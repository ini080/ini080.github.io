---
layout: post
title:  "자료구조"
subtitle:   "DataStructure"
categories: Study
tags: 자료구조
---

```
1. Map
2. List
3. Hash
4. 정렬
5. 이분탐색트리
6. 힙정렬 (힙트리)
7. 이진트리
8. 스택 & 큐 ( a-b-c-d- 순서로 Push했을 때, 나오는 순서)
9. Array, Linked List, HashMap, Vector .. ? (기억이 안남)
10. 시간복잡도
11. 피보나치
```



## LinkedList
Array의 문제점을 해결하기 위한 자료구조. 삽입과 삭제를 O(1) 만에 해결할 수 있다.

하지만 원하는 위치에 삽입을 하고자 하면 원하는 위치를 Search 과정에 있어서 첫번째 원소부터 확인해야한다.

원소를 찾기 위해서 O(n)의 시간이 발생하게 된다.

```java
Node{
   int value;
   Node nextNode; // 다음 위치
}
```



## Stack

- 리스트의 한쪽 끝으로만 자료의 삽입, 삭제 작업이 이 루어지는 자료 구조이다.
* 가장 나중에 삽입된 자료가 가장 먼저 삭제되는 후입 선출(LIFO; Last-In, First-Out) 방식으로 자료를 처 리한다.


```java
class Stack {

   int top;
   int[] stack;
   int size;

   public Stack(int size) {
      top = -1;
      stack = new int[size];
      this.size = size;
   }

   public int peek() {
      return stack[top]; // 가장 위에있는 원소 반환
   }

   public void push(int value) {
      stack[++top] = value;
      System.out.println(stack[top] + " PUSH !");
   }

   public int pop() {
      System.out.println(stack[top] + " POP !");
      return stack[top--];
   }

   public void printStack() {
      System.out.println("-- STACK LIST --");
      for (int i = top; i >= 0; i--)
         System.out.println(stack[i]);
      System.out.println("-- END OF LIST --");
   }
}
```



## Queue
* 선형 리스트의 한쪽에서는 삽입 작업이 이루어지고 다 른 한쪽에서는 삭제 작업이 이루어지도록 구성한 자료 구조이다.
* 시작(Front 또는 Head)과 끝(Rear 또는 Tail)을 표시 하는 두 개의 포인터가 있다.
* 가장 먼저 삽입된 자료가 가장 먼저 삭제되는 선입선 출(FIFO; First-In, First-Out) 방식으로 처리한다.
* 프런트(F, Front) 포인터 : 가장 먼저 삽입된 자료의 기억공 간을 가리키는 포인터로, 삭제 작업을 할 때 사용함
* 리어(R, Rear) 포인터 : 가장 마지막에 삽입된 자료가 위 치한 기억장소를 가리키는 포인터로, 삽입 작업을 할 때 사용함

#### Queue를 이용하는 예
* 창구 업무처럼 서비스 순서를 기다리는 등의 대기 행 렬의 처리에 사용한다.
* 운영체제의 작업 스케줄링에 사용한다.


```java
// 배열 이용
public class Queue {
    private int[] array;
    private int head;
    private int tail;

    public Queue(int size) {
        array = new int[size];
        head = -1;
        tail = -1;
    }

    public void enQueue(int number) {
        if (tail == array.length - 1) throw new RuntimeException("큐가 다 찼습니다.");
        array[++tail] = number;
    }

    public int deQueue() {
        if (tail == -1) throw new RuntimeException("큐에 데이터가 없습니다.");
        int temp = array[++head];
        array[head] = -1;

        if (head == tail) { head = -1; tail = -1; } return temp;
    }

```

```java
// 연결리스트 이용
public class ListQueue {

    private class Node{

        // 노드는 data와 다음 노드를 가진다.
        private Object  data;
        private Node nextNode;

        Node(Object data){
            this.data = data;
            this.nextNode = null;
        }
    }

    // 큐는 front노드와 rear노드를 가진다.
    private Node front;
    private Node rear;

    public ListQueue(){
        this.front = null;
        this.rear = null;
    }

    // 큐가 비어있는지 확인
    public boolean empty(){
        return (front==null);
    }

    // item을 큐의 rear에 넣는다.
    public void insert(Object item){

        Node node = new Node(item);
        node.nextNode = null;

        if(empty()){

            rear = node;
            front = node;

        }else{

            rear.nextNode = node;
            rear = node;

        }
    }

    // front 의 데이터를 반환한다.
    public Object peek(){
        if(empty()) throw new ArrayIndexOutOfBoundsException();
        return front.data;
    }

    // front 를 큐에서 제거한다.
    public Object remove(){

        Object item = peek();
        front = front.nextNode;

        if(front == null){
            rear = null;
        }

        return item;
    }
}

```


## 트리(Tree)
-  정점(Node, 노드)과 선분(Branch, 가지)을 이용하여 사 이클을 이루지 않도록 구성한 Graph의 특수한 형태로 가족의 계보(족보), 연산 수식, 회사 조직 구조도, 히프 (Heap) 등을 표현하기에 적합하다.
![image](/assets/img/study/datastructure/1.png)
![image](/assets/img/study/datastructure/2.png)



### 운행법
![image](/assets/img/study/datastructure/3.png)
![image](/assets/img/study/datastructure/4.png)


## 이진트리

루트 노드를 중심으로 두 개의 서브 트리로 나뉘어진다. 트리에서는 각 층별로 숫자를 매겨서 이를 트리의 레벨이라고 한다.

레벨의 값은 0부터 시작하고 따라서 루트 레벨은 0이다. 그리고 트리의 최고 레벨을 가리켜 해당 트리의 높이라고 한다.



## Binary Search Tree

이진 탐색 트리의 연산은 O(log n)의 시간 복잡도를 갖는다.

규칙

1. 이진 탐색 트리의 노드에 저장된 키는 유일하다.
2. 루트 노드의 키가 왼쪽 서브 트리를 구성하는 어떠한 노드의 키보다 크다.
3. 루트 노드의 키가 오른쪽 서브 트리를 구성하는 어떠한 노드의 키보다 작다.
4. 왼쪽과 오른쪽 서브트리도 이진 탐색 트리이다.

https://swalloow.tistory.com/35

```java
public class Node {
    private int data;
    private Node left;
    private Node right;    

    public Node(int data){
        this.setData(data);
        setLeft(null);
        setRight(null);
    }

    public int getData() {
      return data;
    }

    public void setData(int data) {
      this.data = data;
    }

    public Node getLeft() {
      return left;
    }

    public void setLeft(Node left) {
      this.left = left;
    }

    public Node getRight() {
      return right;
    }

    public void setRight(Node right) {
      this.right = right;
    }
}
```

```java
public class BinarySearchTree {
    public Node root;
    public BinarySearchTree(){
        this.root = null;
    }
    //탐색 연산
    public boolean find(int id){
        Node current = root;
        while(current!=null){
            //현재 노드와 찾는 값이 같으면
            if(current.getData()==id){
                return true;
                //찾는 값이 현재 노드보다 작으면
            } else if(current.getData()>id){
                current = current.getLeft();
                //찾는 값이 현재 노드보다 크면
            } else{
                current = current.getRight();
            }
        }
        return false;
    }

  	//삽입 연산
  	public void insert(int id){
        Node newNode = new Node(id);
        if(root==null){
            root = newNode;
            return;
        }
        Node current = root;
        Node parent = null;
        while(true){
            parent = current;
            if(id < current.getData()){                
                current = current.getLeft();
                if(current==null){
                    parent.setLeft(newNode);
                    return;
                }
            }else{
                current = current.getRight();
                if(current==null){
                    parent.setRight(newNode);
                    return;
                }
            }
        }
    }
  	// 삭제 연산
    public boolean delete(int id){
          Node parent = root;
          Node current = root;
          boolean isLeftChild = false;
          while(current.getData()!=id){
              parent = current;
              if(current.getData()>id){
                  isLeftChild = true;
                  current = current.getLeft();
              }else{
                  isLeftChild = false;
                  current = current.getRight();
              }
              if(current==null){
                  return false;
              }
          }
          //Case 1: 자식노드가 없는 경우
          if(current.getLeft()==null && current.getRight()==null){
              if(current==root){
                  root = null;
              }
              if(isLeftChild==true){
                  parent.setLeft(null);
              }else{
                  parent.setRight(null);
              }
          }

      		//Case 2 : 하나의 자식을 갖는 경우
          else if(current.getRight()==null){
              if(current==root){
                  root = current.getLeft();
              }else if(isLeftChild){
                  parent.setLeft(current.getLeft());
              }else{
                  parent.setRight(current.getLeft());
              }
          } else if(current.getLeft()==null){
              if(current==root){
                  root = current.getRight();
              }else if(isLeftChild){
                  parent.setLeft(current.getRight());
              }else{
                  parent.setRight(current.getRight());
              }
          }

          //Case 3 : 두개의 자식을 갖는 경우
          else if(current.getLeft()!=null && current.getRight()!=null){
              // 오른쪽 서브트리의 최소값을 찾음
              Node successor = getSuccessor(current);
              if(current==root){
                  root = successor;
              }else if(isLeftChild){
                  parent.setLeft(successor);
              }else{
                  parent.setRight(successor);
              }            
              successor.setLeft(current.getLeft());
          }        
    }

  	// 오른쪽 서브트리의 최소 값을 찾는다.
  	public Node getSuccessor(Node deleleNode){
        Node successsor =null;
        Node successsorParent =null;
        Node current = deleleNode.getRight();
        while(current!=null){
            successsorParent = successsor;
            successsor = current;
            current = current.getLeft();
        }
        if(successsor!=deleleNode.getRight()){
            successsorParent.setLeft(successsor.getRight());
            successsor.setRight(deleleNode.getRight());
        }
        return successsor;
    }
}
```



## 힙

우선순위를 위해 만들어진 자료구조

우선순위 큐란?

데이터들이 우선순위를 가지고 있고 우선순위가 높은 데이터가 먼저 나간다.

힙이란 완전 이진 트리의 일종으로 우선순위 큐를 위하여 만들어진 자료구조이다. 여러개의 값들 중에서 최댓값이나 최솟값을 빠르게 찾아내도록 만들어진 자료구조이다.

힙은 반정렬 상태를 유지한다.

최대 힙 : 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진트리

최소 힙 : 부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진트리



힙에서의 부모 노드와 자식 노드의 관계

- 왼쪽 자식의 인덱스 = (부모의 인덱스) * 2
- 오른쪽 자식의 인덱스 = (부모의 인덱스) * 2 + 1
- 부모의 인덱스 = (자식의 인덱스) / 2

힙 삽입 : 힙에 데이터를 삽입하려고 하면 가장 마지막 자리에 공간을 생성하고 데이터를 넣는다. 하지만 넣어야 하는 데이터가 부모 노드보다 크다면 위치를 바꾸어 줘야 한다.

힙 삭제 : 힙에서의 원소의 삭제는 원소를 제거하고 마지막 노드 원소를 루트원소로 올리고 두 서브 트리를 비교하여 더 큰 원소와 교환한다.



```java
// 힙 삽입
public static void insertHeap(int[] heap, int size, int item) { // heap의 배열과, size는 현 heap의 원소의 개수, item은 삽입 원소
  if(size == heap.length-1) { // 힙이 만원이 상태라면 종료
    System.out.println("heep size 초과");
    return;
  }
  int i = ++size; // 다음 item이 들어갈 원소 위치
  while(true) {
    if(i == 1) {
      break;
    } // 힙의 원소가 하나도 없었다면 반복문 탈출
    if(item < heap[i/2]) {
      break;
    } // 아이템이 부모 노드보다 작다면 반복문 탈출
    heap[i] = heap[i/2]; // 부모노드의 키값을 자식노드로 이동 i /= 2; // i의 위치를 즉 원소가 들어갈 자리를 부모노드로 변경
  }
  heap[i] = item; // 정해진 i위치에 item 삽입
}

```



```java
// 힙 삭제
	public static int deleteHeap(int[] heap, int size) { //히프로부터 원소 삭제
			// heap은 배열, size는  원소의 개수

		int n = size; // Heap안에 있는 마지막 원소의 다음 위치

		if(n == 0) {return 999;} // 삭제할 원소가 없다면  에러

		int item = heap[1]; // 삭제 노드를 item에 저장
		int temp = heap[n]; // 마지막 원소를 temp에 저장

		n--; // 마지막 원소의 삭제
		int i = 1; // 원소를 가르키는 변수 최초는 삭제하는 루트
		int j = 2; // j변수는 i변수의 왼쪽 서브트리를 가르키는 변수

		while(j <= n) { //서브트리의 위치가 현 원소의 수보다 커진다면 힙의 크기를 초과 하니까 종료

			if(j= heap[j]) { // temp가 현 서브트리보다 크다는 것은 현 i위치가 원소의 위치가 맞다는 것이다.
				break;
			}

			heap[i] = heap[j]; // 서브트리를 한 레벨 위로 이동
			i = j; // 비교를 할 노드의 위치를 바꿔줌
			j *=2; // j의 서브트리 위치를 이동한다.
		}

		heap[i] = temp; //마지막 원소를 i위치에 넣어준다.
		return item;
	}


출처: https://kingpodo.tistory.com/30 [킹포도의 코딩]
```



## 그래프

그래프 탐색

DFS : 깊이 우선 탐색

BFS : 너비 우선 탐색



## 선택 정렬
![image](/assets/img/study/datastructure/12.png)

첫번째 자료를 두번째 자료부터 마지막 자료까지 차례대로 비교하여 가장 큰 값을 찾아 첫 번째에 놓고,

두번째 자료를 세번째 자료부터 마지막 자료까지 차례대로 비교하여 가장 큰 값을 찾아 두번째에 놓는작업을 반복한다.

시간 복잡도 : O(n^2)

```java
import java.util.Arrays;

public class ChoiceSort {
	public static void main(String[] args) {
		int[] arr = {5,6,1,9,4};
		int temp;

		for(int i = 0; i < arr.length; i++) {
			int max = Integer.MIN_VALUE;
			int index = 10;
			for(int j = i; j < arr.length; j++) {
				if(max < arr[j]) {
					max = arr[j];
					index = j;
				}
			}

			temp = arr[i];
			arr[i] = max;
			arr[index] = temp;
		}

		System.out.println(Arrays.toString(arr));
	}
}
```



## 버블 정렬
![image](/assets/img/study/datastructure/6.png)

서로 인접한 두 원소를 비교하여 정렬하는 알고리즘

- 인접한 2개의 레코드를 비교하여 크기가 순서대로 되어있지 않으면 서로 교환

  - 1번째와 2번째 비교, 교환

  - 2번째 3번째 비교, 교환

  - 3번째 4번째 비교, 교환

  - 4번째 5번째 비교, 교환

  - 다시 처음으로 돌아와서 1번째 2번째 비교, 교환

  - 마지막은 빼고 3번째 4번째 비교, 교환 작업

  - 반복



- 시간복잡도

  - 최상, 평균, 최악 모두 일정
  - O(n^2)

```java
import java.util.Arrays;

public class BubbleSort {
	public static void main(String[] args) {
		int[] arr = {5,6,1,9,4};

		int temp;

		for(int i = 0; i < arr.length; i++) {
			for(int j = 0; j < arr.length -1 -i; j++) {
				if(arr[j] < arr[j+1]) {
					temp = arr[j];
					arr[j] = arr[j+1];
					arr[j+1] = temp;
				}
			}
		}

		System.out.println(Arrays.toString(arr));
	}
}
```


## 삽입 정렬
![image](/assets/img/study/datastructure/5.png)

새로운 인덱스를 기존의 정렬된 카드 카드 사이의 올바른 자리를 찾아 삽입한다.

자료 배열의 모든 요소를 앞에서부터 차례대로 이미 정렬된 배열 부분과 비교 하여, 자신의 위치를 찾아 삽입함으로써 정렬을 완성

두번째 자료부터 시작하여 그 앞의 자료들과 비교하여 삽입할 위치를 지정한 후 자료를 뒤로 옮기고 지정한 자리에 자료를 삽입한다.

자료가 삽입될 위치를 찾았다면 그 위치에 자료를 삽입 하기 위해 자료를 한 칸씩 이동시킨다.

장점

- 안정한 정렬 방법이다.
- 대부분의 레코드가 이미 정렬되어 있는 경우 매우 효율적일 수 있다.

단점

- 비교적 많은 레코드들의 이동이 포함된다.
- 레코드 수가 많고 레코드 크기가 클 경우에 적합하지 않다.

시간복잡도

- 최선의 경우
  - 이동 없이 1번의 비교만 이루어진다.
  - O(n)
- 최악의 경우
  - O(n^2)


```java
import java.util.Arrays;

public class InsertSort {
	public static void main(String[] args) {
		int[] arr = {5,6,1,9,4};
		int temp;

		for(int i = 1; i < arr.length; i++) {
			int key = arr[i];
			int index = 0;

			for(int j = i-1; j >= 0; j—) {
				if(arr[j] < key) {
					arr[j+1] = arr[j];
				}else {
					index = j+1;
					break;
				}
			}

			arr[index] = key;
		}
		System.out.println(Arrays.toString(arr));
	}
}
```




## 시간 복잡도
![image](/assets/img/study/datastructure/7.png)

### 빅오 표기법

![image](/assets/img/study/datastructure/8.png)


![image](/assets/img/study/datastructure/9.png)
![image](/assets/img/study/datastructure/10.png)

### 성능비교
![image](/assets/img/study/datastructure/11.png)

## 피보나치 수열

```java
public class Fibonacci {

	public static void main(String[] args) {
		int input = 8; // 8개 출력

		for (int i = 1; i <= input; i++) {
			System.out.println(fibo(i));
		}
	}

	public static int fibo(int n) {
		if (n <= 1)
			return n;
		else
                        return fibo(n-2) + fibo(n-1);
	}
}
```


## 출처
[강의노트 25. 자료구조, 알고리즘 - 성능측정 (Big-O) · 초보몽키의 개발공부로그](https://wayhome25.github.io/cs/2017/04/20/cs-26-bigO/)
