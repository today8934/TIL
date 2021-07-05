# String 뒤집기

1.

```java
public class Ex01{
    public static void main(String[] args) {
        String str = "Reverse this Strings";        
        String new_str = "";
 
        for (int i = str.length()-1; i > -1; i--) {
            new_str += str.charAt(i);
        }
        System.out.println(new_str);
    }   
}
```

2.

```java
public class Ex01{
    public static void main(String[] args) {
        String str = "Reverse this Strings";        
        String new_str = "";
 
        String[] str1 = str.split("");
        for (int i = str1.length-1; i > -1; i--) {
            new_str += str1[i];
        }
        System.out.println(new_str);
    }   
}
```

3.

```java
public class Ex01{
    public static void main(String[] args) {
        String str = "Reverse this Strings";
         
        StringBuffer reverse = new StringBuffer(str);
        System.out.println(reverse.reverse());
    }   
}
```

4.

```java
public class Ex01{
    public static void main(String[] args) {
        String str = "Reverse this Strings";
         
        StringBuffer reverse = new StringBuffer();
        reverse.append(str);
        System.out.println(reverse.reverse());
    }   
}
```

5.

```java
public class String_Reverse_Practice { 
		public static void main(String[] args) { 
				String str = "abcde"; 
				char[] arr = str.toCharArray(); // String -> char[] 
				char[] reversedArr = new char[arr.length];
 
				for(int i=0; i<arr.length; i++){ 
						reversedArr[arr.length-1-i] = arr[i]; 
				} 

				String reversedStr = new String(reversedArr); 
				System.out.println(reversedStr); // edcba 
		} 
}
```

6.

```java
public class String_Reverse_Practice { 
		public static void main(String[] args) { 
				String str = "abcde"; 
				char[] arr = str.toCharArray(); // String -> char[] 
				List<Character> list = new ArrayList<>(); 
				
				for(char each : arr){ // char[] -> List 
						list.add(each); 
				} // reverse 

				Collections.reverse(list);
				ListIterator li = list.listIterator(); 

				while(li.hasNext()){ 
						System.out.print(li.next()); // edcba 
				} 
		}
 }
```
