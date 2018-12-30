# Palindrome, the Longest Mirror Sequence, a Strange Performance VS an Ordinary Performance in Java                   
A sequence of characters can be shown as x = x[0] x[1] ... x[n].                


Suppose that my architect has been limited that I could only focus on the pair i and j with x[i] = x[j]. 
When using the dynamic programming, two basic factors we should figure out firstly: the initialized basic states and the 'induction relations'. The initialized basic states considered in my algorithm are the pair i and j with x[i] = x[j], between which    
