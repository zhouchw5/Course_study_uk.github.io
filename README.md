# Palindrome, the Longest Mirror Sequence, a Strange Performance VS an Ordinary Performance in Java                   
A sequence of characters can be shown as x = x[0] x[1] ... x[n]. A subsequence 
<a href="https://www.codecogs.com/eqnedit.php?latex=$x[i_1],&space;x[i_2],&space;...,&space;x[i_l]$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$x[i_1],&space;x[i_2],&space;...,&space;x[i_l]$" title="$x[i_1], x[i_2], ..., x[i_l]$" /></a> 
of x is called a palindrome if it equals to 
<a href="https://www.codecogs.com/eqnedit.php?latex=$x[i_l],&space;x[i_{l-1}],&space;...,&space;x[i_1]$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$x[i_l],&space;x[i_{l-1}],&space;...,&space;x[i_1]$" title="$x[i_l], x[i_{l-1}], ..., x[i_1]$" /></a>. 



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
               
Yours,             
Chuwei Zhou             
2018.12.30             
