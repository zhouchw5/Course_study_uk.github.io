# Palindrome, the Longest Mirror Sequence, a Strange Performance VS an Ordinary Performance in Java                   
A sequence of characters can be shown as x = x[0] x[1] ... x[n].                


Suppose that my architect has been limited that I could only focus on the pair i and j with x[i] = x[j].                
When using the dynamic programming, two basic factors we should figure out firstly: the initialized basic states and the 'induction relations'. The initialized basic states considered in my algorithm are the pair i and j with x[i] = x[j], between which there is no another pair m and k(
<a href="https://www.codecogs.com/eqnedit.php?latex=$k\neq&space;m$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$k\neq&space;m$" title="$k\neq m$" /></a>
) with x[m] = x[k]. It means that when I construct the matrix[i][j] to recognize whether x[i] = x[j] or not, I should assign different values to matrix[i][j] for different cases, x[i] = x[j] or x[i] != x[j].              
               
For each pair of initialized basic states, I would detect the adjacent pair x[p] = x[q] that can wrap up the inner pair x[i] = x[j] and iterate it till no other outer pair can wrap up the current mirror sequence. Centering on different initialized basic state x[i] = x[j], the longest mirror sequences starting from x[start] and ending at x[end] would have different lengths, and the dynamic programming would help me find out the longest one and the corresponding adjacent inner pair, all of these information would be stored in another two matrices.                   
