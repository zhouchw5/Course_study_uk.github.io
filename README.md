# Some Simple Practices on R Session5_Linear Regression              
This letter is mainly to simulate some simple examples in Linear Regression, and to figure out the algorithms for some outputs of the function 'lm'. The first data set we use contains various measures of IQ (Intelligence Quotient) and brain size measurements for 38 psychology students, along with their height, weight and gender. More information is available at http://lib.stat.cmu.edu/DASL/Datafiles/Brainsize.html.                
          
To read the dataframe and visualize part of it for sampling:           
```r
BrainSize <- read.csv("BrainSize.csv")
> BrainSize[1:5,]
  Gender FSIQ VIQ PIQ Weight Height MRI_Count
1 Female  133 132 124    118   64.5    816932
2   Male  139 123 150    143   73.3   1038437
3   Male  133 129 128    172   68.8    965353
4 Female  137 132 134    147   65.0    951545
5 Female   99  90 110    146   69.0    928799
# where we have visualized the first five rows of the data frame in Console.
```
Basically, we just utilize the linear regression model considering the dependent variable PIQ related to one type of regressor, MRI_Count.       
```r
attach(BrainSize)
BrainSizeLM1 <- lm(PIQ ~ MRI_Count)
```
When assigning the summary function, we can witness the output of the linear regression model in this data set shown as below:         
```r
summary(BrainSizeLM1)
Call:
lm(formula = PIQ ~ MRI_Count)

Residuals:
    Min      1Q  Median      3Q     Max 
-40.079 -17.508  -2.096  17.100  41.574 

Coefficients:
             Estimate Std. Error t value Pr(>|t|)  
(Intercept) 4.660e+00  4.371e+01   0.107   0.9157  
MRI_Count   1.176e-04  4.806e-05   2.448   0.0194 *
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 21.21 on 36 degrees of freedom
Multiple R-squared:  0.1427,	Adjusted R-squared:  0.1189 
F-statistic: 5.993 on 1 and 36 DF,  p-value: 0.01937
```
From the summary above, we know that in the linear regression model 
<a href="https://www.codecogs.com/eqnedit.php?latex=y&space;=&space;\beta&space;_{0}&plus;\beta&space;_{1}x&space;&plus;&space;\varepsilon" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y&space;=&space;\beta&space;_{0}&plus;\beta&space;_{1}x&space;&plus;&space;\varepsilon" title="y = \beta _{0}+\beta _{1}x + \varepsilon" /></a>, 
the estimate for the intercept is 
<a href="https://www.codecogs.com/eqnedit.php?latex=\beta&space;_{0}&space;=&space;4.660" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\beta&space;_{0}&space;=&space;4.660" title="\beta _{0} = 4.660" /></a>, 
the estimate for 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\beta&space;_{1}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\beta&space;_{1}$" title="$\beta _{1}$" /></a> 
is 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\beta&space;_{1}&space;=&space;1.17\times&space;10^{-4}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\beta&space;_{1}&space;=&space;1.17\times&space;10^{-4}$" title="$\beta _{1} = 1.17\times 10^{-4}$" /></a>.             
Then we need to the compute the standard deviation of the estimated 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\beta&space;_{i}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\beta&space;_{i}$" title="$\beta _{i}$" /></a>, 
we know that the variance for the LSE    
<a href="https://www.codecogs.com/eqnedit.php?latex=$\widehat{\beta&space;}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\widehat{\beta&space;}$" title="$\widehat{\beta }$" /></a> 
can be formulated as 
<a href="https://www.codecogs.com/eqnedit.php?latex=$Var\left&space;(&space;\widehat{\beta&space;}&space;\right&space;)=\sigma&space;^{2}\left&space;(&space;X^{T}X&space;\right&space;)^{-1}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$Var\left&space;(&space;\widehat{\beta&space;}&space;\right&space;)=\sigma&space;^{2}\left&space;(&space;X^{T}X&space;\right&space;)^{-1}$" title="$Var\left ( \widehat{\beta } \right )=\sigma ^{2}\left ( X^{T}X \right )^{-1}$" /></a>. For the learning purpose, we can verify whether the standard deviation is               
<a href="https://www.codecogs.com/eqnedit.php?latex=$std(\beta_{0}&space;)&space;=&space;4.371*10^{1}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$std(\beta_{0}&space;)&space;=&space;4.371*10^{1}$" title="$std(\beta_{0} ) = 4.371*10^{1}$" /></a>, 
<a href="https://www.codecogs.com/eqnedit.php?latex=$std(\beta_{1}&space;)&space;=&space;4.806*10^{-5}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$std(\beta_{1}&space;)&space;=&space;4.806*10^{-5}$" title="$std(\beta_{1} ) = 4.806*10^{-5}$" /></a>.          
- **Construct the matrix of regressors**             
```r
x_1 <- c(BrainSize$MRI_Count)
x_0 <- x1 <- c(rep(1, times = 38))
matrix_x <- cbind(x1, test)
```
- **Compute the matrix <a href="https://www.codecogs.com/eqnedit.php?latex=$\left&space;(&space;X^{T}X&space;\right&space;)^{-1}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\left&space;(&space;X^{T}X&space;\right&space;)^{-1}$" title="$\left ( X^{T}X \right )^{-1}$" /></a>**          
```r
matrix_xT <- t(matrix_x)
product_xx <- matrix_xT%*%matrix_x 
reverse_x <- solve(product_xx)
```
- **Compute the variance for the residuals, by using the unbiased estimator <a href="https://www.codecogs.com/eqnedit.php?latex=$\widehat{\sigma&space;}^{2}=\left&space;\|&space;y-X\widehat{\beta&space;}&space;\right&space;\|^{2}/\left&space;(&space;n-p-1&space;\right&space;)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\widehat{\sigma&space;}^{2}=\left&space;\|&space;y-X\widehat{\beta&space;}&space;\right&space;\|^{2}/\left&space;(&space;n-p-1&space;\right&space;)$" title="$\widehat{\sigma }^{2}=\left \| y-X\widehat{\beta } \right \|^{2}/\left ( n-p-1 \right )$" /></a>**            
```r
Beta_vector <- as.matrix(c(4.660e+00, 1.176e-04))
vector_XB <- matrix_x%*%Beta_vector
vector_XB <- c(vector_XB)
y <- c(BrainSize$PIQ) 
residual_vector <- y - vector_XB
residual_vector <- residual_vector*residual_vector
sigma_sample <- sum(residual_vector)/(38-2)
std_beta0 <- sqrt(sigma_sample*reverse_x[1][1])
std_beta1 <- sqrt(sigma_sample*reverse_x[2][2])
# Actually I have made a naive mistake here, the last statement should be revised as 
# std_beta1 <- sqrt(sigma_sample*reverse_x[2,2])
```
We can find that std_beta0 = 43.7129977495838, which is consistent with the corresponding data in the summary above, but std_beta1 = NA_real_, we can compute the std_beta1 more 'manually'. But when you revise the statement as 'std_beta1 <- sqrt(sigma_sample*reverse_x[2,2])', the error can be fixed.                       
```r
> View(reverse_x)
# we can find that reverse_x[2][2] = 5.133137e-12
>sigma_sample*5.133137e-12
# the result of sigma_sample*5.133137e-12 is 2.309631e-09
>sqrt(2.309631e-09)
# the result is 4.805862e-05, which is also consistent with the std.error of the coefficient for the variable 'MRI_Count' shown in the summary above. 
```

Next, based on the estimators and the standard deviations, we can proceed the hypothesis testing. We know that the Wald Tests are generally comfortable with a premise that n is large enough. When n is small, the Student's t distribution would give us finer (and more accurate non-asymptotic) result. But no matter for the Wald Tests or the t-statistic, we should compute 
<a href="https://www.codecogs.com/eqnedit.php?latex=$T=\left&space;(&space;\widehat{\beta&space;}_{j}-\beta&space;_{j0}&space;\right&space;)/SE\left&space;(&space;\widehat{\beta&space;}_{j}&space;\right&space;)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$T=\left&space;(&space;\widehat{\beta&space;}_{j}-\beta&space;_{j0}&space;\right&space;)/SE\left&space;(&space;\widehat{\beta&space;}_{j}&space;\right&space;)$" title="$T=\left ( \widehat{\beta }_{j}-\beta _{j0} \right )/SE\left ( \widehat{\beta }_{j} \right )$" /></a>, 
where we test the null hypotheses 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\beta&space;_{j}=0$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\beta&space;_{j}=0$" title="$\beta _{j}=0$" /></a> 
against the alternatives 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\beta&space;_{j}\neq&space;0$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\beta&space;_{j}\neq&space;0$" title="$\beta _{j}\neq 0$" /></a>.            
For the intercept 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\beta&space;_{0}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\beta&space;_{0}$" title="$\beta _{0}$" /></a>,           
```r
T_statistic_0 <- Beta_vector[1,1]/std_beta0
```
and the value of the t-statistic for the coefficient related to MRI_Count        
```r
T_statistic_1 <- Beta_vector[2,1]/std_beta1
```
And the output is            
```r
> T_statistic_0
[1] 0.1066044
> T_statistic_1
[1] 2.447012
```
which is consistent with the summary above. Then compared with t-distribution with the freedom 
<a href="https://www.codecogs.com/eqnedit.php?latex=$n-p=38-2=36$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$n-p=38-2=36$" title="$n-p=38-2=36$" /></a>, 
we can obtain the probabilities for 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\left&space;|T&space;\right&space;|>\left&space;|&space;T_{statistic_0}&space;\right&space;|$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\left&space;|T&space;\right&space;|>\left&space;|&space;T_{statistic_0}&space;\right&space;|$" title="$\left |T \right |>\left | T_{statistic_0} \right |$" /></a> 
and 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\left&space;|T&space;\right&space;|>\left&space;|&space;T_{statistic_1}&space;\right&space;|$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\left&space;|T&space;\right&space;|>\left&space;|&space;T_{statistic_1}&space;\right&space;|$" title="$\left |T \right |>\left | T_{statistic_1} \right |$" /></a> 
respectively. In this hypotheses testing process, the variables satisfying the normal distribution are 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\widehat{\beta&space;}_{i}/\left&space;(&space;\widehat{\sigma&space;}^{2}\left&space;[&space;X^{T}X&space;\right&space;]^{-1}_{j&plus;1,j&plus;1}&space;\right&space;)^{1/2}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\widehat{\beta&space;}_{i}/\left&space;(&space;\widehat{\sigma&space;}^{2}\left&space;[&space;X^{T}X&space;\right&space;]^{-1}_{j&plus;1,j&plus;1}&space;\right&space;)^{1/2}$" title="$\widehat{\beta }_{i}/\left ( \widehat{\sigma }^{2}\left [ X^{T}X \right ]^{-1}_{j+1,j+1} \right )^{1/2}$" /></a>. 
And the t-distribution with the freedom of (n-p) can be formulated as 
<a href="https://www.codecogs.com/eqnedit.php?latex=$Z=X/\sqrt{Y/(n-p)}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$Z=X/\sqrt{Y/(n-p)}$" title="$Z=X/\sqrt{Y/(n-p)}$" /></a>, 
where X satisfies the normal distribution, Y is the Chi-square distribution 
<a href="https://www.codecogs.com/eqnedit.php?latex=$\chi&space;^{2}\left&space;(&space;n-p&space;\right&space;)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\chi&space;^{2}\left&space;(&space;n-p&space;\right&space;)$" title="$\chi ^{2}\left ( n-p \right )$" /></a>. So when we compare these two formulas:               





                      
![white](https://github.com/zhouchw5/Course_study_uk.github.io/blob/Fundamental-Algorithms-Practice_20181107/white.png)                          
Thanks for Dr.YN.Chen leading us to explore the statistical world                                        
**_Yours,_**                         
**_Chuwei Zhou_**                 
**_2018.12.19_**                     
 

       
