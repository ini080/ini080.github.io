```java
package Programers;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

public class 실패율 {

	public static void main(String[] args) {
		int N = 5;
		int [] stages = { 2,1,2,6,2,4,3,3};
		solution(N,stages);
	}
	
	public static int[] solution(int N, int[] stages) {
		float [] clear = new float[N+2];  
	      float sum = 0;
	      for(int i = 0; i < stages.length; i++) {
	         clear[stages[i]]++;
	      }
	      for(int i = 1; i < clear.length; i++) {
	         sum += clear[i];
	      }
	      float fail[] = new float[N+2];
	      System.out.println(Arrays.toString(clear));
	      for(int i = 1; i < clear.length; i++) {
	          if( clear[i] != 0 ) {
	             fail[i] = clear[i] / ( sum - clear[i-1] );
	          }else {
	             fail[i] = 0;
	          }
	          sum -= clear[i-1];
	       }
	      System.out.println(Arrays.toString(fail));
	   
	      List<Float> order = new ArrayList<>();
	      for(int i = 1; i < fail.length -1; i++) {
	         order.add(fail[i]);
	      }
	      
	      Collections.sort(order,Collections.reverseOrder());
	      System.out.println("페일 : " + Arrays.toString(fail));
	      System.out.println("오더 : " + order.toString());
	      
	      List<Integer> ans_order = new ArrayList<>();
	      int[] answer = new int[N];
	      for(int i = 0; i< order.size(); i++) {
	         for(int j = 1 ; j < fail.length-1; j++) {
	            if( order.get(i) == fail[j]) {
	               ans_order.add(j);
	               fail[j] = -1;
	            }
	         }
	      }
	      
	      for(int i = 0 ; i < ans_order.size(); i++) {
	         answer[i] = ans_order.get(i);
	      }
	        return answer;
	    }



}
```
