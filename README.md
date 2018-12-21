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
Basically, we just utilize the linear regression model considering the dependent variable PIQ related one type of regressor, MRI_Count.       
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
We know that the estimate for the intercept is 



Thanks for Dr.YN.Chen leading us to explore the statistical world                                        
**_Yours,_**                         
**_Chuwei Zhou_**                 
**_2018.12.19_**                     
 

       
