# Simple Practice in LeetCode_Longest Substring Without Repeating Characters        

- The first idea comes into my mind is the recursive method.                
- Two cases: one case is the substring without the first character, the other one is the substring containing the first character. Then for the next iteration, the second character would act as the first character.                 
- Can I firstly define a method that can output the index of a repeated character within the given substring?                  

```java
public class nonrepeatedString {
	static int repeatedIndex (String x, int start, int end) {
		int repeatIndex = end;
		for (int i=start+1; i<=end; i++) {
			if (x.charAt(i) == x.charAt(start)) {
				repeatIndex = i;
				break;
			}
		}
		if ((repeatIndex == end)&&(x.charAt(repeatIndex)!=x.charAt(start))) {
			return repeatIndex;
		}else {
			return (repeatIndex-1);
		}
	}
	public static void main(String[] args) {
		if (args.length < 1) {
			return;
		}
		if (args[0].length() == 1) {
			System.out.println("The answer is '" + args[0] +"', with the length of 1.");
			return;
		}
		
		String test = args[0];
		int[] lengthSub = new int[test.length()];
		
		for(int i = 0; i < test.length(); i++) {
			int end = test.length()-1;
			end = repeatedIndex(test, i, end);
			for (int j = i+1; j<end; j++) {				
				end = repeatedIndex(test, j, end);				
			}
			lengthSub[i] = end - i + 1;
		}
		
		int maxlength = lengthSub[0];
		int maxIndex = 0;
		for (int i=0; i < test.length(); i++) {
			if (lengthSub[i]>maxlength) {
				maxlength = lengthSub[i];
				maxIndex = i;
			}
		}
		System.out.print("The answer is '");
		for (int j = maxIndex; j<maxIndex + maxlength; j++) {
			System.out.print(test.charAt(j));
		}
		System.out.print("', with the length of " + maxlength + ".");
	}
}
```


