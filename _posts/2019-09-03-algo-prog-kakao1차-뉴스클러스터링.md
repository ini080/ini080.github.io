```java
package Programers;

import java.util.ArrayList;
import java.util.List;
import java.util.regex.Pattern;

public class 뉴스클러스터링 {

	public static void main(String[] args) {
		String str1 = "FRANCE";
		String str2 = "french";
		solution(str1, str2);
	}
	
	public static int solution(String str1,String str2) {
		str1 = str1.toLowerCase();
		str2 = str2.toLowerCase();
		
		
		StringBuilder sb1 = new StringBuilder();
		StringBuilder sb2 = new StringBuilder();
		sb1.append(str1);
		sb2.append(str2);
		
		String pattern = "^[a-zA-Z]*$";
		
		List<String> list1 = new ArrayList<>();
		List<String> list2 = new ArrayList<>();
		
		for(int i = 0; i < str1.length()-1; i++) {
			String st = sb1.substring(i,i+2);
			boolean other = Pattern.matches(pattern, st);
			if(other) {
				list1.add(st);
			}
		}
		
		for(int i = 0; i < str2.length()-1; i++) {
			String st = sb2.substring(i,i+2);
			boolean other = Pattern.matches(pattern, st);
			if(other) {
				list2.add(st);
			}
		}
		
		System.out.println(list1.toString());
		System.out.println(list2.toString());
		double count = 0;
		
		for(int i = 0 ; i < list1.size(); i++) {
			if( list2.contains(list1.get(i))) {
				count += 1;
			}
		}
		
		List<String> 교집합 = new ArrayList<>();
		
		for(int i = 0; i < list1.size(); i++) {
			String first = list1.get(i);
			for(int j = 0 ; j < list2.size(); j++) {
				String second = list2.get(j);
				if( first.equals(second)) {
					교집합.add(second);
					list2.remove(list2.get(j));
					break;
				}
			}
		}
		
		for(int i = 0; i < list2.size(); i++) {
			list1.add(list2.get(i));
		}
		System.out.println(list1.size());
		double answer = 0;
		if( list1.size() <= 0 ) {
			answer = 1;
		}else {
			answer = (double)교집합.size() / (double)list1.size();
		}
		System.out.println((int)Math.floor( answer * 65536 ));
		return (int)Math.floor( answer * 65536 );
	}

}

```
