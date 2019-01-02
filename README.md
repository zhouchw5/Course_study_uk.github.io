# MergeSort                                                                 
Modified by Julia Boettcher 2012, 2013, 2014, 2016 and Konrad Swanepoel 2018, the recursive version of the MergeSort algorithm (which is a divided and conquer algorithm) can be shown as below. It divides the array to be sorted in two sub-arrays and sorts each of them by dividing each into two sub-arrays and iterates this process inductively. Finally the two sorted sub-arrays can be merged into one sorted arrray.                  
                   
The first critical point to proceed is how we can divide the array to be sorted into two sub-arrays. Firstly we divide the array x[i] into two sub-array with the middle index (start+end)/2 in the following way:                 
                
                
&nbsp; &nbsp; &nbsp; &nbsp; int[] left = new int[middle-start];              
&nbsp; &nbsp; &nbsp; &nbsp; int[] right = new int[end-middle];          
&nbsp; &nbsp; &nbsp; &nbsp; for (int i=start; i < middle; i++) {left[i-start] = x[i];}                            
&nbsp; &nbsp; &nbsp; &nbsp; for (int i=middle; i < end; i++) {right[i-middle] = x[i];}                
   
   
Based on our induction analysis, the final step is to merge two sorted sub-arrays into one sorted array. The merging algorithm could be more straightforward when we decompose the problem into some sub-problems like: in terms of the first element right[0] in the right sub-array (which means that we have known there are (end-middle-1) elements that are greater or equal to right[0]), we can move this element right[0] to the left sub-array as long as we find one element in the left sub-array that is greater of equal to right[0]. **On another more structural thinking pattern, we can focus on assigning the entries with i smaller elements in the i-th site of the array.** And the two sorted sub-arrays in the increasing order can give us the convenience that if right[iright-1]<=left[ileft]<=right[iright], we can know that there are (ileft+iright) elements smaller or equal to left[ileft], meaning that the left[ileft] should be assigned in the site with index (start+ileft+iright). The key point is how can we reach the criticality **right[iright-1]<=left[ileft]<=right[iright]** or **left[ileft-1]<=right[iright]<=left[ileft]**.                  
&nbsp; &nbsp; &nbsp; &nbsp; int iLeft = 0; int iRight = 0; //where we   

                      
**Yours,**                
**Chuwei Zhou**                    
**2019.01.02**                                 
