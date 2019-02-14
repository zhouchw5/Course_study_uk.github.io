# Linear Programming and the Iteration Allocation Model                
## Introduction                 
### The Standard Form of Linear Programming               
<a href="https://www.codecogs.com/eqnedit.php?latex=\left\{\begin{matrix}&space;max&space;\begin{matrix}&space;&&space;C^T&space;x\end{matrix}\\&space;Ax\leq&space;b\\&space;x\geq&space;0&space;\end{matrix}\right." target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left\{\begin{matrix}&space;max&space;\begin{matrix}&space;&&space;C^T&space;x\end{matrix}\\&space;Ax\leq&space;b\\&space;x\geq&space;0&space;\end{matrix}\right." title="\left\{\begin{matrix} max \begin{matrix} & C^T x\end{matrix}\\ Ax\leq b\\ x\geq 0 \end{matrix}\right." /></a>            
Utilizing R programming to solve a simple LP example:              
<a href="https://www.codecogs.com/eqnedit.php?latex=\left\{\begin{matrix}&space;max&space;\begin{matrix}&space;&&space;x_1&space;&plus;&space;x_2\end{matrix}\\&space;x_1\leq&space;1,&space;x_2\leq1\\&space;x_1,x_2\geq&space;0&space;\end{matrix}\right." target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left\{\begin{matrix}&space;max&space;\begin{matrix}&space;&&space;x_1&space;&plus;&space;x_2\end{matrix}\\&space;x_1\leq&space;1,&space;x_2\leq1\\&space;x_1,x_2\geq&space;0&space;\end{matrix}\right." title="\left\{\begin{matrix} max \begin{matrix} & x_1 + x_2\end{matrix}\\ x_1\leq 1, x_2\leq1\\ x_1,x_2\geq 0 \end{matrix}\right." /></a>                
```r
library(Rsymphony)
obj <- c(1,1)

mat <- matrix(c(1,0,0,1), nrow = 2) 
dir <- c("<=", "<=")

rhs <- c(1,1)
max <- T
```
Actually we should have used the Integer Programming in our model, with some simple revises changing the variables type within the library Rsymphony. But as the extension of the feasible region, we keep using linear programming here.               
                      
                      
In order for the convenience to merge different data frames and assign different sub-set of a data frame, I just set that each data frame would have its own matrix form. And for uniformity, in the BOM (bill of materials) data set, the order of the parent items corresponding to a son item would be the same to that of the parent items in forecast demand, and the order of the son items corresponding to a parent item would be the same to that of the son items in supply data set.           
               
## Read the Data and Data Processing               
```r
library(readxl)
test <- read_excel('test.xlsx', sheet = "demand_forecast")
test_matrix <- as.matrix(test) # the matrix form of the demand data of the parent items
```                
The form of the demand data can be simplified as:                     
![LP_demand](https://github.com/zhouchw5/Course_study_uk.github.io/blob/master/LP_demand.png)                  
```r
bom <- read_excel('test.xlsx', sheet = "BOM")
bom_matrix <- as.matrix(bom) # the matrix form of the bill of materials
```
The form of the bill of materials (BOM) can be simplified as:              
![LP_BOM](https://github.com/zhouchw5/Course_study_uk.github.io/blob/master/LP_BOM%E5%9B%BE%E7%89%871.png)                  
                    
```r
supply <- read_excel('test.xlsx', sheet = "supply")
supply[is.na(supply)] <- 0
supply_matrix <- as.matrix(supply) # the matrix form of the supply data set
```
                
                
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
                     
Best Regards!                              
Chuwei Zhou                
2019.2.8                  
