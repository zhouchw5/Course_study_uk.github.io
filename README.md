# Some Convenient Notes on R Sessions_Vector, Data Frame            
## Vector         
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
               
## Data Frame        
To construct the data frame, combine the different variables (each variable is a vector, because in the data frame you have observations, the number of observations is the length of a vector.)           
```r
weight <- c(135, 165.6, 123, 122, 189)
height <- c(86.5, 71.8, 77.2, 84.9, 75.4)
combining <-  data.frame(weight, height)
sheep <- data.frame(weight, height)
# calculate the mean of the column 'height':
mean(sheep$height)
```
To add another column with the variable named backlength:             
```r
sheep$backlength <- c(130.4, 100.2, 109.4, 140.6, 101.4)
```

## Descriptive Analysis             
```r
summary(sheep$weight)
summary(sheep)
IQR(sheep$height)  #interquartile range
sd(sheep$backlength)  
```

#Two way for system help: ?+object   or   help.start()                  

## Session Management and visibility               
we can execute the statement objects() to to visualize all the variables we have initialized. But generally some variables have been encapsulated in a data frame. So we can tide up our workspace by removing some variables, and we can still get access to them via the data frame.                
```r
rm(height, weight)
sheep$weight
```
Thanks for Dr.Chen from Cambridge University leading us in data analysis and statistical methods.             


_Yours,_             
_Chuwei Zhou_             
_2018.12.13_
   




