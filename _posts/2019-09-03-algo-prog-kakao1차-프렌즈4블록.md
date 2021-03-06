---
layout: post
title:  "[2017 kakako 1차] 프렌즈4블록"
subtitle:   "프렌즈4블록"
categories: Algorithm
tags: programmers
---

## 프렌즈4블록
블라인드 공채를 통과한 신입 사원 라이언은 신규 게임 개발 업무를 맡게 되었다. 이번에 출시할 게임 제목은 프렌즈4블록.
같은 모양의 카카오프렌즈 블록이 2×2 형태로 4개가 붙어있을 경우 사라지면서 점수를 얻는 게임이다.


만약 판이 위와 같이 주어질 경우, 라이언이 2×2로 배치된 7개 블록과 콘이 2×2로 배치된 4개 블록이 지워진다. 같은 블록은 여러 2×2에 포함될 수 있으며, 지워지는 조건에 만족하는 2×2 모양이 여러 개 있다면 한꺼번에 지워진다.


블록이 지워진 후에 위에 있는 블록이 아래로 떨어져 빈 공간을 채우게 된다.

만약 빈 공간을 채운 후에 다시 2×2 형태로 같은 모양의 블록이 모이면 다시 지워지고 떨어지고를 반복하게 된다.

위 초기 배치를 문자로 표시하면 아래와 같다.

TTTANT
RRFACC
RRRFCC
TRRRAA
TTMMMF
TMMTTJ

각 문자는 라이언(R), 무지(M), 어피치(A), 프로도(F), 네오(N), 튜브(T), 제이지(J), 콘(C)을 의미한다

입력으로 블록의 첫 배치가 주어졌을 때, 지워지는 블록은 모두 몇 개인지 판단하는 프로그램을 제작하라.

### 입력 형식

입력으로 판의 높이 m, 폭 n과 판의 배치 정보 board가 들어온다.
2 ≦ n, m ≦ 30
board는 길이 n인 문자열 m개의 배열로 주어진다. 블록을 나타내는 문자는 대문자 A에서 Z가 사용된다.

### 출력 형식

입력으로 주어진 판 정보를 가지고 몇 개의 블록이 지워질지 출력하라.

### 입출력 예제
m	n	board	answer
4	5	[CCBDE, AAADE, AAABF, CCBBF]	14
6	6	[TTTANT, RRFACC, RRRFCC, TRRRAA, TTMMMF, TMMTTJ]	15

### 예제에 대한 설명
입출력 예제 1의 경우, 첫 번째에는 A 블록 6개가 지워지고, 두 번째에는 B 블록 4개와 C 블록 4개가 지워져, 모두 14개의 블록이 지워진다.
입출력 예제 2는 본문 설명에 있는 그림을 옮긴 것이다. 11개와 4개의 블록이 차례로 지워지며, 모두 15개의 블록이 지워진다.


## Solution

전체 맵을 순회하면서 터뜨릴 블록이 있는지 찾고, 있다면 터뜨릴 블록의 위치를 리스트에 담아
리스트를 순회하면서 한번에 터뜨리는데, 이렇게 하면 겹치는 부분이 생긴다. 겹치는 부분에 대해서는 이미 터뜨려서 0으로 되어있다면 그곳은 카운트를 하지않는 방법으로 구현하였다.
그 후 0으로 바뀐 터진칸들은 아래로 떨어뜨리고 루프를 마무리한다.
다음 루프에서 터뜨릴곳이 없다면 break하고 카운트값을 출력한다.

```java

public class 프렌즈4블록 {

	public static void main(String[] args) {
		int m = 4;
		int n = 5;
		String [] board = { "CCBDE", "AAADE", "AAABF", "CCBBF"};
		solution(m, n, board);
	}

	static int dx[] = {0,1,1};
	static int dy[] = {1,0,1};
	public static int solution(int m, int n, String[] board) {

		char map [][] = new char[m][n];
		for(int i = 0; i < m; i++) {
			String a = board[i];
			for(int j = 0 ; j < n; j++) {
				map[i][j] = a.charAt(j);
			}
		}
		int cnt = 0;
		boolean end = true;
		while(end)
		{
			boolean flag = true;
			List<Node> list = new ArrayList<>();
			for(int i = 0; i < m-1; i++)
			{
				flag = true;
				for(int j = 0; j < n-1; j++)
				{
					boolean isOk = true;  // 터뜨릴것이 있으면 true
					char a = map[i][j];
					if( a != '0') {
						for(int k = 0; k < 3; k++)
						{
							if( map[i + dx[k]][j + dy[k]] != a ) isOk = false;
						}

						if(isOk) {
							list.add(new Node(i,j));
						}
					}
				}
			}

			if( list.size() == 0 ) end = false;

			// 터뜨리기
			for(int i = 0 ; i < list.size(); i++)
			{
				Node location = list.get(i);
				if( map[location.x][location.y] != '0' ) {
					cnt++;
					map[location.x][location.y] = '0';
				}
				for(int j = 0; j < 3; j++) {
					if ( map[location.x + dx[j]][location.y + dy[j]] != '0' ) {
						cnt++;
						map[location.x + dx[j]][location.y + dy[j]] = '0';
					}
				}
			}

			// 떨어뜨리기

			for(int j = 0; j <  n; j++) {
				for(int i = m-1; i > 0; i--) {
					if ( map[i][j] == '0' ) {
						for(int k = i-1; k >= 0; k--) {
							if( map[k][j] != '0' ) {
								map[i][j] = map[k][j];
								map[k][j] = '0';
								break;
							}
						}
					}
				}
			}
		}
		System.out.println(cnt);
		return cnt;
	}
	static class Node{
		int x, y;
		public Node (int x ,int y) {
			this.x = x;
			this.y = y;
		}
		@Override
		public String toString() {
			return "Node [x=" + x + ", y=" + y + "]";
		}
	}

}

```
