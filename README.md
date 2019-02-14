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
The form of the son item's supply data can be simplified as:             
![LP_supply](https://github.com/zhouchw5/Course_study_uk.github.io/blob/master/LP_supply.png)                   
                
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
## Iteration of Linear Programming Models by Week                                     
```r
for (k in 1:12) {
  if (k==1) {
    rhs <- c(as.numeric(test_matrix[,2]), as.numeric(supply_matrix[,2]))
    obj <- c(rep(1, times = nrow(test)))
    mat <- constraint_matrix
    dir <- c(rep("<=" ,times = nrow(constraint_matrix)))
    max <- T
    order <- Rsymphony_solve_LP(obj, mat, dir, rhs, max = max)$`solution`
    parent_name <- as.character(bom$`Parent Item`[bom$`Son Item` == bom_matrix[1,2]])
    
    order <- cbind(parent_name, order)
    order <- as.data.frame(order)
    names(order) <- c("Parent Item","Demand")
    order_byWeek <- merge(order, bom, by.x = 'Parent Item')
    order_son_item <- as.numeric(as.vector(order_byWeek$Demand))*as.numeric(as.vector((order_byWeek$Ratio)))
    order_byWeek <- cbind(order_byWeek, order_son_item)
    
    # the rest demand of complete machines:
    order_rest_parent_item <- test$Week1 - Rsymphony_solve_LP(obj, mat, dir, rhs, max = max)$`solution`
    order_newWeek_parent_item <- order_rest_parent_item + as.numeric(test_matrix[,3])
    
    # the next supply source in the next week:
    for (t in 1:nrow(supply_matrix)) {
      son_item_demand <- order_byWeek$order_son_item[order_byWeek$`Son Item`==bom_matrix[t,2]]
      sum_son_item_demand <- sum(son_item_demand)
      if (t==1) {
        order_per_son_item <- c(sum_son_item_demand)
      } else {
        order_per_son_item <- c(order_per_son_item, sum_son_item_demand)
      }
    }
    supply_newWeek_supply_item <- as.numeric(supply_matrix[,2]) - order_per_son_item + as.numeric(supply_matrix[,3])
    
    
    # the final order for thw parent items and the son items this week
    order_all_parent_item <- Rsymphony_solve_LP(obj, mat, dir, rhs, max = max)$`solution`
    order_all_son_item <- order_per_son_item
  } else {
    rhs <- c(order_newWeek_parent_item, supply_newWeek_supply_item)
    obj <- c(rep(1, times = nrow(test)))
    mat <- constraint_matrix
    dir <- c(rep("<=" ,times = nrow(constraint_matrix)))
    max <- T
    order <- Rsymphony_solve_LP(obj, mat, dir, rhs, max = max)$`solution`
    parent_name <- as.character(bom$`Parent Item`[bom$`Son Item` == bom_matrix[1,2]])
    
    order <- cbind(parent_name, order)
    order <- as.data.frame(order)
    names(order) <- c("Parent Item","Demand")
    order_byWeek <- merge(order, bom, by.x = 'Parent Item')
    order_son_item <- as.numeric(as.vector(order_byWeek$Demand))*as.numeric(as.vector((order_byWeek$Ratio)))
    order_byWeek <- cbind(order_byWeek, order_son_item)
    
    # the rest demand of complete machines:
    order_rest_parent_item <- as.numeric(test_matrix[,k+1]) - Rsymphony_solve_LP(obj, mat, dir, rhs, max = max)$`solution`
    if (k<12) {
      order_newWeek_parent_item <- order_rest_parent_item + as.numeric(test_matrix[,k+2])
    }
    
    
    # the next supply source in the next week:
    for (t in 1:nrow(supply_matrix)) {
      son_item_demand <- order_byWeek$order_son_item[order_byWeek$`Son Item`==bom_matrix[t,2]]
      sum_son_item_demand <- sum(son_item_demand)
      if (t==1) {
        order_per_son_item <- c(sum_son_item_demand)
      } else {
        order_per_son_item <- c(order_per_son_item, sum_son_item_demand)
      }
    }
    if (k<12) {
      supply_newWeek_supply_item <- as.numeric(supply_matrix[,k+1]) - order_per_son_item + as.numeric(supply_matrix[,k+2])
    }
    
    
    # the final order for thw parent items and son items this week
    order_all_parent_item <- cbind(order_all_parent_item, Rsymphony_solve_LP(obj, mat, dir, rhs, max = max)$`solution`)
    order_all_son_item <- cbind(order_all_son_item, order_per_son_item)
  }
}
```
Best Regards!                              
Chuwei Zhou                
2019.2.8                  
