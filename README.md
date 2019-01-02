# MergeSort                                                                 
Modified by Julia Boettcher 2012, 2013, 2014, 2016 and Konrad Swanepoel 2018, the recursive version of the MergeSort algorithm (which is a divided and conquer algorithm) can be shown as below. It divides the array to be sorted in two sub-arrays and sorts each of them by dividing each into two sub-arrays and iterates this process inductively. Finally the two sorted sub-arrays can be merged into one sorted arrray.                  
                   
The first critical point to proceed is how we can divide the array to be sorted into two sub-arrays. Firstly we divide the array x[i] into two sub-array with the middle index (start+end)/2 in the following way:                 
                
                
&nbsp; &nbsp; &nbsp; &nbsp; int[] left = new int[middle-start];              
&nbsp; &nbsp; &nbsp; &nbsp; int[] right = new int[end-middle];          
&nbsp; &nbsp; &nbsp; &nbsp; for (int i=start; i < middle; i++) {left[i-start] = x[i];}                            
&nbsp; &nbsp; &nbsp; &nbsp; for (int i=middle; i < end; i++) {right[i-middle] = x[i];}                
   
   
Based on our induction analysis, the final step is to merge two sorted sub-arrays into one sorted array. The merging algorithm could be more straightforward when we decompose the problem into some sub-problems like: in terms of the first element right[0] in the right sub-array (which means that we have known there are (end-middle-1) elements that are greater or equal to right[0]), we can move this element right[0] to the left sub-array as long as we find one element in the left sub-array that is greater of equal to right[0]. **On another more structural thinking pattern, we can focus on assigning the entries with i smaller elements in the i-th site of the array.** And the two sorted sub-arrays in the increasing order can give us the convenience that if right[iright-1]<=left[ileft]<=right[iright], we can know that there are (ileft+iright) elements smaller or equal to left[ileft], meaning that the left[ileft] should be assigned in the site with index (start+ileft+iright). The key point is how can we reach the criticality **right[iright-1]<=left[ileft]<=right[iright]** or **left[ileft-1]<=right[iright]<=left[ileft]**.             
                 
                 
&nbsp; &nbsp; &nbsp; &nbsp; int iLeft = 0; int iRight = 0;                
&nbsp; &nbsp; &nbsp; &nbsp; //we start the comparison fairly from the corresponding first elements of left sub-array and right sub-array         
&nbsp; &nbsp; &nbsp; &nbsp; for (int i=start; i<end ; i++)                 
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; // if done with left part, copy from right part            
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; if (iLeft >= left.length) {x[i] = right[iRight]; iRight++;}        
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; // if done with right part, copy from left part          
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; else if (iRight >= right.length) {x[i] = left[iLeft]; iLeft++;}           
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; else if ( left[iLeft] <= right[iRight] )              
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; //**meaning that right[irRight-1] has been 'beaten' by one of the current**      
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; //**entries, of wich the largest one is left[iLeft],**        
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; //**so left[iLeft] >= right[iRight-1] as well**                                
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **x[i] = left[iLeft]; iLeft++;**           
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; else // meaning left[iLeft] > right[iRight]                                
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **x[i] = right[iRight];iRight++;**            
                            
And the base is the merging operation of two elements. Here comes the completed code:                 
```java
class MergeSort {
   
    // sort the array x
    static void mergeSort (int[] x) {
        mergeSort(x,0,x.length);
    }

    // sort the elements  x[start], x[start+1], ... , x[end-1]
    static void mergeSort (int[] x, int start, int end) {
        if (start < end-1)  { // at least two elements to be sorted
            int middle = (start+end)/2;
            mergeSort (x, start, middle);
            mergeSort (x, middle, end);
            merge (x, start, middle, end);
        }
    }

    // merge the two sorted sequences
    // x[start],... , x[middle-1]   and   x[middle], ... , x[end-1]
    static void merge (int[] x, int start, int middle, int end) {
        int[] left = new int[middle-start];
        int[] right = new int[end-middle];
        // copy the first half to left, the second half to right
        for (int i=start; i < middle; i++) {
            left[i-start] = x[i];
        }
        for (int i=middle; i < end; i++) {
            right[i-middle] = x[i];
        }

        int iLeft = 0;  // index to left
        int iRight = 0; // index to right

        for (int i=start; i<end ; i++) {
            // if done with left part, copy from right part
            if (iLeft >= left.length) {
                x[i] = right[iRight];
                iRight++;
            // if done with right part, copy from left part
            } else if (iRight >= right.length) {
                x[i] = left[iLeft];
                iLeft++;
            // otherwise, if left element smaller than right, copy left
            } else if ( left[iLeft] <= right[iRight] ) {
                x[i] = left[iLeft];
                iLeft++;
             // otherwise, if right smaller than left, copy right
            } else {
                x[i] = right[iRight];
                iRight++;
            }
        }
    }

    // for test purposes only 
    public static void main (String[] args) {
        int[] A = {33, 5, 2, 1, 20, 15, 3, 9, 11, 7};
        outArray(A, "before sorting:");
        mergeSort (A) ;
        outArray(A, "after sorting:");
        test(100000);
        test(200000);
        test(400000);
        test(800000); 
    } 

    // print info, and the array
    static void outArray (int[] x, String info) {
        System.out.println(info);
        for (int i=0; i < x.length; i++)
            System.out.print(x[i] + "  ");
        System.out.println();
    }

    // test merge sort on a random array with n entries
    static void test (int n) {
        int[] x = new int[n];
        randomFill(x);
        long time = System.currentTimeMillis();
        mergeSort(x);
        time = System.currentTimeMillis() - time;
        System.out.println( "Sorting " + n + " numbers needed " + time + " ms.");
    }

    // fill the array x with random numbers
    static void randomFill (int[] x) { 
        for (int i=0; i < x.length; i++)
            x[i] = (int) ((double) x.length * Math.random());
    }

}
```
                  
                  
                    
                    

                      
**Yours,**                
**Chuwei Zhou**                    
**2019.01.02**                                 
