# Integer Programming and the Iteration Allocation Model                
## Introduction                 
### The Standard Form of Linear Programming               

                
In order for the convenience to merge different data frames and assign different sub-set of a data frame, I just set that each data frame would have its own matrix form. And for uniformity, in the BOM (bill of materials) data set, the order of the parent items corresponding to a son item would be the same to that of the parent items in forecast demand, and the order of the son items corresponding to a parent item would be the same to that of the son items in supply data set.                                     
## Constraint Matrix          

No.0 constraint: the number of each complete machine would not exceed the forecast demand;      
```r
constraint_0 <- c(rep(0, times = nrow(test)*nrow(test)))
constraint_matrix_0 <- matrix(constraint_0, nrow = nrow(test))
for (i in 1:nrow(test)) {
  constraint_matrix_0[i,i] <- 1
}
```
No.1 constraint: the maximum supply of each son item;
```r
constraint_matrix <- constraint_matrix_0
for (j in 1:nrow(supply)) {
  vector_ratio <- bom$Ratio[bom$`Son Item`== bom_matrix[j,2]]
  constraint_matrix <- rbind(constraint_matrix, vector_ratio)
}
rownames(constraint_matrix) <- NULL
```

