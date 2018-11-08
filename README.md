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
In my leetCode submission, limited to the given format, I give up the method 'repeatedIndex' outside the main method and integrate all the coding process into one method that would return an integer variable, shown as below, from which we could see that defining methods in advanced and assigning them in the main method would make our coding more structured and readable.             


```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] lengthSub = new int[s.length()];
        int end = s.length()-1;
        for(int i = 0; i < s.length(); i++) {
            for (int j = i+1; j<=end; j++) {
                if (s.charAt(j) == s.charAt(i)) {
                    end = j;
                    break;
                }
            }
            if ((end == s.length()-1)&&(s.charAt(end) !=s.charAt(i))) {
                for (int k=i+1; k<end; k++) {
                    int end_T = end;
                    for (int h=k+1; h<=end; h++) {
                        if (s.charAt(h) == s.charAt(k)) {
                            end_T = h;
                        }
                    }
                    if ((end_T== end)&&(s.charAt(end_T)!=s.charAt(k))){
                        end = end_T;
                    }else {
                        end = end_T-1;
                    }
                }    
            }else {
                end = end-1;
                for (int k=i+1; k<end; k++) {
                    int end_T = end;
                    for (int h=k+1; h<=end; h++) {
                        if (s.charAt(h) == s.charAt(k)) {
                            end_T = h;
                        }
                    }
                    if ((end_T== end)&&(s.charAt(end_T)!=s.charAt(k))){
                        end = end_T;
                    }else {
                        end = end_T-1;
                    }
                }  
            }
            lengthSub[i] = end - i + 1;
	}
        int maxlength = lengthSub[0];
        int maxIndex = 0;
        for (int i=0; i < s.length(); i++) {
            if (lengthSub[i] > maxlength) {
                maxlength = lengthSub[i];
                maxIndex = i;
            }
        }
        return maxlength;
	}
}
```

