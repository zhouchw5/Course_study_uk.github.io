# Some Convenient Notes on R Sessions            
## Vector
### Vector_basic computing
The product of two vectors with the same length: just the vector containing the elements equal to the products of the corresponding two elements with the same index;         
```r
x <- c(1, 2, 3)
y <- x*x
# y = (1,4,9)
```
If we try to add together vectors of different lengths, R uses a recycling rule; the smaller vector is repeated until the dimensions match.     
```r
small <- c(1,2)
large <- c(0,0,0,0,0,0)
y <- small + large
# y = (1,2,1,2,1,2)
```
To concatenate vectors:
```r
x <- c(small, large, small)
# x = (1 2 0 0 0 0 0 0 1 2)
```
Some useful operators with respect to the elements:             
```r
total <- sum(weight)
#        where weight is a vector
numobs <- length(weight)
meanweight <- total/numobs
x <- mean(weight)
#        where x=meanweight   
```
To remove all the objects:            
```r
rm(list=objects())
```





_Yours,_             
_Chuwei Zhou_             
_2018.12.13_
   




