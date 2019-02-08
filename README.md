# Integer Programming and the Iteration Allocation Model                
## Introduction               

## Constraint Matrix          

No.0 constraint: the number of each complete machine would not exceed the forecast demand;      
```r
constraint_0 <- c(rep(0, times = nrow(test)*nrow(test)))
constraint_matrix_0 <- matrix(constraint_0, nrow = nrow(test))
for (i in 1:nrow(test)) {
  constraint_matrix_0[i,i] <- 1
}
```


