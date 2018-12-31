# Palindrome, the Longest Mirror Sequence, a Strange Performance VS an Ordinary Performance in Java                   
A sequence of characters can be shown as x = x[0] x[1] ... x[n]. A subsequence 
<a href="https://www.codecogs.com/eqnedit.php?latex=$x[i_1],&space;x[i_2],&space;...,&space;x[i_l]$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$x[i_1],&space;x[i_2],&space;...,&space;x[i_l]$" title="$x[i_1], x[i_2], ..., x[i_l]$" /></a> 
of x is called a palindrome if it equals to 
<a href="https://www.codecogs.com/eqnedit.php?latex=$x[i_l],&space;x[i_{l-1}],&space;...,&space;x[i_1]$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$x[i_l],&space;x[i_{l-1}],&space;...,&space;x[i_1]$" title="$x[i_l], x[i_{l-1}], ..., x[i_1]$" /></a>. 
We should determine in time 
<a href="https://www.codecogs.com/eqnedit.php?latex=$O\left&space;(&space;n^2&space;\right&space;)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$O\left&space;(&space;n^2&space;\right&space;)$" title="$O\left ( n^2 \right )$" /></a> 
a longest mirror sequence in x with the help of a dynamic programming approach.            


Suppose that my architect has been limited that I could only focus on the pair i and j with x[i] = x[j].                
When using the dynamic programming, two basic factors we should figure out firstly: the initialized basic states and the 'induction relations'. The initialized basic states considered in my algorithm are the pair i and j with x[i] = x[j], between which there is no another pair m and k(
<a href="https://www.codecogs.com/eqnedit.php?latex=$k\neq&space;m$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$k\neq&space;m$" title="$k\neq m$" /></a>
) with x[m] = x[k]. It means that when I construct the matrix[i][j] to recognize whether x[i] = x[j] or not, I should assign different values to matrix[i][j] for different cases, x[i] = x[j] or x[i] != x[j].              
               
For each pair of initialized basic states, I would detect the adjacent pair x[p] = x[q] that can wrap up the inner pair x[i] = x[j] and iterate it till no other outer pair can wrap up the current mirror sequence. Centering on different initialized basic state x[i] = x[j], the longest mirror sequences starting from x[start] and ending at x[end] would have different lengths, and the dynamic programming would help me find out the longest one and the corresponding adjacent inner pair, all of these information would be stored in another two matrices. More details can be shown in my following code:                   
```java
public class LongestMirrorSequence {
	private final int previous_start, previous_end;
	
	public LongestMirrorSequence (int start, int end) {
		previous_start = start;
		previous_end = end;
	}
	
	public int previous_start() { return previous_start;}
	public int previous_end() {return previous_end;}
	
	public static void main(String[] args) {
		
		if (((args == null)||(args.length == 0))||(args.length>1)) {
			System.out.println("please input formative one command line argument");
			return;
		}
		
        // initializing the character array, matrix[i][j] (max-length starting in label i and ending in label j) ;
		char[] c = new char[args[0].length()];	
		if (c.length == 1) {
			System.out.println("length of longest mirror sequence: 1");
			System.out.println("corresponding sequence: " + args[0]);
			return;
		}
		// to guarantee the following processes are based on c.length>=2
		
		// initializing the previousLabel matrix previousLabel[i][j], storing the starting point and ending point of the max-length subsequence inside  the the interval i and j; 
		int[][] longestLength = new int[c.length][c.length]; 	
		LongestMirrorSequence[][] previousLabel = new LongestMirrorSequence[c.length][c.length];
		int[][] equality = new int[c.length][c.length];
		// if the interval between the equality pair c[i] and c[j] has no other pair with the same character, equality[i][j] = 1, otherwise equality[i][j] = 2;  
		// for example, ABCA, equality[0][3] = 1; but for ACBFCA, equality[0][5] = 2;
```
              
```java
		for (int i=0; i<c.length; i++) {
			c[i] = args[0].charAt(i);
			LongestMirrorSequence r = new LongestMirrorSequence(i,i);
			previousLabel[i][i] = r;
			longestLength[i][i] = 1;
		}		
		
		for (int i=0; i<c.length-1; i++) {
			for (int j=i+1; j<c.length; j++) {
				if (c[i]==c[j]) {
					if ((j-i)<=2) {
						equality[i][j] = 1;
					} else {
						boolean containing = false;
						for (int l=i+1; l<j-1; l++) {
							for (int h=l+1; h<j; h++) {
								if(c[l] == c[h]) {
									containing = true;
								}
							}
						}
						if (containing) {
							equality[i][j] = 2;
						}else if(!containing) {
							equality[i][j] = 1;
						}
					}
				}
			}
		}

```                  
                
```java
		for (int i=0; i<c.length-1; i++) {
			for (int j=i+1; j<c.length; j++) {
				if (equality[i][j]==1) {
					if(j==i+1) {
						longestLength[i][j] = 2;
						LongestMirrorSequence r1 = new LongestMirrorSequence(i,j);
						previousLabel[i][j] = r1;
						
					}else {
						longestLength[i][j] = 3;
						LongestMirrorSequence r2 = new LongestMirrorSequence(i+1,i+1);
						previousLabel[i][j] = r2;
					}
					if ((i!=0)&&(j!=c.length-1)) {
						for (int a=0; a<i; a++) {
							for (int b=j+1; b<c.length; b++) {
								if (c[a]==c[b]) {
									int max_previous = longestLength[i][j];
									int previous_a = i;
									int previous_b = j;
									for (int a1=a+1;a1<=i; a1++) {
										for (int b1=b-1; b1>=j; b1--) {
											if ((c[a1]==c[b1])&&(longestLength[a1][b1]>=max_previous)) {
												max_previous = longestLength[a1][b1];
												previous_a = a1;
												previous_b = b1;
											}
										}
									}
									if ((max_previous+2) > longestLength[a][b]) {
										longestLength[a][b] = max_previous+2;
										LongestMirrorSequence r3 = new LongestMirrorSequence(previous_a, previous_b);
										previousLabel[a][b] = r3; 
									}
									
								}
							}
						}
					}
				}
			}
		}
```            
               
```java
		int maxlongestMirror = 1;
		int longestStart = 0;
		int longestEnd = 0;
		for (int i=0; i<c.length; i++) {
			for (int j=0; j<c.length; j++) {
				if (longestLength[i][j] > maxlongestMirror) {
					maxlongestMirror = longestLength[i][j];
					longestStart = i;
					longestEnd = j;
				}
			}
		}
		System.out.println("length of longest mirror sequence: " + maxlongestMirror);
		
		char[] out = new char[maxlongestMirror];
		int printCount = 0;
		while (printCount<=((maxlongestMirror-1)/2)) {
			out[printCount] = c[longestStart];
			out[out.length-1-printCount] = c[longestEnd];
			int start, end;
			start = previousLabel[longestStart][longestEnd].previous_start();
			end = previousLabel[longestStart][longestEnd].previous_end();
			longestStart = start;
			longestEnd = end;
			printCount++;
		}
		
		System.out.print("corresponding sequence: ");
		for (int i=0; i<out.length; i++) {
			System.out.print( out[i] + " ");
		}
		System.out.println("");
	}
}
```                  
                        
			
We can see that this solution can be simplified in many ways, as long as we liberate ourselves from the the shackles of only considering the pairs i and j with x[i] = x[j]. We can consider all the pairs i and j, and store the information including the the length of the longest padindrome within a pair i and j, and the corresponding staring/ending points. The following is the solution from Dr Konrad Swanepoel.                               
                        
We construct a matrix mirror[i][j] containing the length of a longest mirror sequence starting from x[i] and ending with x[i]. And the initialized states are mirror[i][i] = 1, for i = 0,1,...,n-1. And the matrix start[i][j] denotes the index of the starting element for this mirror sequence. The matrix end[i][j] denotes the index of the ending element for this mirror sequence. And the corresponding initialized states are start[i][i] = end[i][i] = i for i = 0,1,...,n-1.                            			
```java
class LongestMirrorSequence {

    public static void main(String[] args) {
        if (args.length == 0)
            return;
        char[] x = args[0].toCharArray();
        int n = x.length;
        int[][] mirror = new int[n][n];
        int[][] start = new int[n][n];
        int[][] end = new int[n][n];
```
After constructing the initialized states, we should figure out the relation between a current problem and its sub-problem, as what we used to do in dynamic programming.               
- if ((i<j)&&(x[i] != x[j]))        
&nbsp; &nbsp; &nbsp; mirror[i][j] = max{ mirror[i+1][j], mirror[i][j-1]}  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; if (mirror[i+1][j] is larger)                   
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; start[i][j] = start[i+1][j] and end[i][j] = end[i+1][j]              
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; if (mirror[i][j-1] is larger)                  
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; start[i][j] = start[i][j-1] and end[i][j] = end[i][j-1]                   
                
- if ((i<j)&&(x[i] = x[j]))        
&nbsp; &nbsp; &nbsp; if ((i+1)<=(j-1))         
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; mirror[i][j] = mirror[i+1][j-1] + 2;               
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; start[i][j] = i;              
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; end[i][j] = j;             
&nbsp; &nbsp; &nbsp; else (i+1 = j)                   
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; mirror[i][j] = 2;             
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; start[i][j] = i;            
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; end[i][j] = j;                   
                 
With these inductions, the final value maximum length would be stored in mirror[0][n-1].                       
```java
        for (int j = 0; j < n; j++) {
            for (int i = j; i >= 0; i--) {
                if (i == j) {
                    mirror[i][j] = 1;
                    start[i][j] = i;
                    end[i][j] = j;
                } else { // i < j
                    if (x[i] == x[j]) {
                        start[i][j] = i;
                        end[i][j] = j;
                        if (i+1 == j) {
                            mirror[i][j] = 2;
                        } else { // i+1 < j
                            mirror[i][j] = mirror[i+1][j-1] + 2;
                        }
                    } else { // x[i] != x[j]
                        if (mirror[i+1][j] > mirror[i][j-1]) {
                            mirror[i][j] = mirror[i+1][j];
                            start[i][j] = start[i+1][j];
                            end[i][j] = end[i+1][j];
                        } else {
                            mirror[i][j] = mirror[i][j-1];
                            start[i][j] = start[i][j-1];
                            end[i][j] = end[i][j-1];
                        }
                    }       
                }
            }
        }
        System.out.println("Length of longest mirror sequence: " + mirror[0][n-1]);
        int s = start[0][n-1];
        int e = end[0][n-1];
        String forward = "";
        String backward = "";
        while (e-s > 1) {
            forward = forward + x[s];
            backward = x[e] + backward;
            int sTemp = s;
            int eTemp = e;
            s = start[sTemp+1][eTemp-1];
            e = end[sTemp+1][eTemp-1];
        }
```
We have stopped before e==s, which can avoid taking the middle character twice if the number of characters is odd.           
```java
        forward = forward + x[s];
        if (e-s==1) { // There are exactly two characters left
            backward = x[e] + backward;
        }
        System.out.println("Corresponding sequence: " + forward + backward);
    }
}
```
	    
Yours,             
Chuwei Zhou             
2018.12.30             
