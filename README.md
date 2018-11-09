# Fundamental Performances of Statistical Methods via R/Python

- **Distribution Sampling**

Binomial Distribution: X->Bin(n, p), including the Bernouli distribution X->Bin(1, p);                
``` r
x <- rbinom(10000, 100, 0.1)
mean(x)
length(x)
table(x)

t <- c(1:1000)
#CDF:
pbinom(t, 100, 0.1)
#PDF:
pbinom(t, 100, 0.1)
#quantile:
qbinom(t, 100, 0.1)
```


- **Asymptotic Notation**                    
<a href="https://www.codecogs.com/eqnedit.php?latex=$2^n&space;=&space;o(n!)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$2^n&space;=&space;o(n!)$" title="$2^n = o(n!)$" /></a>                    
If one pen and a sheet of A4 paper are given, it can be written as:                
<a href="https://www.codecogs.com/eqnedit.php?latex=$\lim_{n&space;\to&space;\infty&space;}&space;\left&space;(&space;2^{n}/n!&space;\right&space;)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\lim_{n&space;\to&space;\infty&space;}&space;\left&space;(&space;2^{n}/n!&space;\right&space;)$" title="$\lim_{n \to \infty } \left ( 2^{n}/n! \right )$" /></a>                      
<a href="https://www.codecogs.com/eqnedit.php?latex=$\lim_{n&space;\to&space;\infty&space;}&space;log_{2}\left&space;(&space;2^{n}/n!&space;\right&space;)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\lim_{n&space;\to&space;\infty&space;}&space;log_{2}\left&space;(&space;2^{n}/n!&space;\right&space;)$" title="$\lim_{n \to \infty } log_{2}\left ( 2^{n}/n! \right )$" /></a>,
which we firstly formulate.           
<a href="https://www.codecogs.com/eqnedit.php?latex=$\log_{2}\left&space;(&space;2^{n}/n!&space;\right&space;)&space;=&space;n-log_{2}n&space;-log_2(n-1)-...-log_{2}(n-i)-&space;log_{2}1$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\log_{2}\left&space;(&space;2^{n}/n!&space;\right&space;)&space;=&space;n-log_{2}n&space;-log_2(n-1)-...-log_{2}(n-i)-&space;log_{2}1$" title="$\log_{2}\left ( 2^{n}/n! \right ) = n-log_{2}n -log_2(n-1)-...-log_{2}(n-i)- log_{2}1$" /></a>            
<a href="https://www.codecogs.com/eqnedit.php?latex=$\log_{2}\left&space;(&space;2^{n}/n!&space;\right&space;)&space;=&space;n-log_{2}2\cdot&space;(n/2)&space;-log_{2}2\cdot&space;[(n-1)/2]-...-$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\log_{2}\left&space;(&space;2^{n}/n!&space;\right&space;)&space;=&space;n-log_{2}2\cdot&space;(n/2)&space;-log_{2}2\cdot&space;[(n-1)/2]-...-$" title="$\log_{2}\left ( 2^{n}/n! \right ) = n-log_{2}2\cdot (n/2) -log_{2}2\cdot [(n-1)/2]-...-$" /></a>              
<a href="https://www.codecogs.com/eqnedit.php?latex=$&space;-&space;log_{2}2\cdot&space;[(n-i)/2]-&space;log_{2}2\cdot&space;[1/2]$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$&space;-&space;log_{2}2\cdot&space;[(n-i)/2]-&space;log_{2}2\cdot&space;[1/2]$" title="$ - log_{2}2\cdot [(n-i)/2]- log_{2}2\cdot [1/2]$" /></a>             
<a href="https://www.codecogs.com/eqnedit.php?latex=$&space;log_{2}(2^{n}/n!)&space;=&space;n-n-log_{2}(n/2)-log_{2}((n-1)/2)-...-log_{2}(1/2)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$&space;log_{2}(2^{n}/n!)&space;=&space;n-n-log_{2}(n/2)-log_{2}((n-1)/2)-...-log_{2}(1/2)$" title="$ log_{2}(2^{n}/n!) = n-n-log_{2}(n/2)-log_{2}((n-1)/2)-...-log_{2}(1/2)$" /></a>         
<a href="https://www.codecogs.com/eqnedit.php?latex=$&space;\lim_{n&space;\to&space;\infty&space;}log_{2}(2^{n}/n!)&space;=&space;-\sum_{k=0}^{n-1}log_{2}((n-k)/2)&space;\rightarrow&space;-\infty&space;$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$&space;\lim_{n&space;\to&space;\infty&space;}log_{2}(2^{n}/n!)&space;=&space;-\sum_{k=0}^{n-1}log_{2}((n-k)/2)&space;\rightarrow&space;-\infty&space;$" title="$ \lim_{n \to \infty }log_{2}(2^{n}/n!) = -\sum_{k=0}^{n-1}log_{2}((n-k)/2) \rightarrow -\infty $" /></a>                 
<a href="https://www.codecogs.com/eqnedit.php?latex=$&space;\lim_{n&space;\to&space;\infty&space;}(2^{n}/n!)&space;\rightarrow&space;0&space;$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$&space;\lim_{n&space;\to&space;\infty&space;}(2^{n}/n!)&space;\rightarrow&space;0&space;$" title="$ \lim_{n \to \infty }(2^{n}/n!) \rightarrow 0 $" /></a>                
**Simulation in Python**      

``` python
x = np.array(np.arange(1000))
y1 = [0 for i in range(1000)]
for i in range(1000):    
    y1[i] = np.math.factorial(x[i])
y2 = 2**x
x_y = figure()
x_y.line(x, y2, line_width = 2)
x_y.circle(x, y1, fill_color = 'red', size = 8)
output_file('x_t.html')
show(x_y)
```                 
![n5](https://github.com/zhouchw5/Course_study_uk.github.io/blob/Data-Analysis_R_review_20181104/n5.png)
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; n=5, with red dots representing factorials, blue line representing the exponential of 2              
             
![white](https://github.com/zhouchw5/Course_study_uk.github.io/blob/Data-Analysis_R_review_20181104/white.png)                  
![n10](https://github.com/zhouchw5/Course_study_uk.github.io/blob/Data-Analysis_R_review_20181104/n10.png)             
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; n=10, with red dots representing factorials, blue line representing the exponential of 2                      
             
![white](https://github.com/zhouchw5/Course_study_uk.github.io/blob/Data-Analysis_R_review_20181104/white.png)             
![n1000](https://github.com/zhouchw5/Course_study_uk.github.io/blob/Data-Analysis_R_review_20181104/n1000.png)                       
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; n=1000, with red dots representing factorials, blue line representing the exponential of 2              
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **It means that for a large n, the event count of the permutation and combination would far more than that**               
 &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; **of filling n digits with binary numbers 0 or 1.**                
                    
                    
![white](https://github.com/zhouchw5/Course_study_uk.github.io/blob/Data-Analysis_R_review_20181104/white.png)              
- **Tossing Game with R**                
```R
x <- c(sample(1:6, 100000, replace = T))
y <- as.data.frame(table(x))
names(y) <- c("Toss", "Frequency")
y.probability <- data.frame(Probability = y$Frequency/100000, y[,])
attach(y.probability)
plot(Toss, Probability)
A = (y.probability$Toss == 1)                
           
A = subset(y.probability, Toss == 2, select = Probability)+ subset(y.probability, Toss == 4, select = Probability)+ subset(y.probability, Toss == 6, select = Probability)
B = subset(y.probability, Toss == 1, select = Probability)+ subset(y.probability, Toss == 2, select = Probability)+ subset(y.probability, Toss == 3, select = Probability) + subset(y.probability, Toss == 4, select = Probability)
C = subset(y.probability, Toss == 2, select = Probability)+ subset(y.probability, Toss == 4, select = Probability)           
```
                    











 











                    
              

_**Yours,**_             
_**Chuwei Zhou**_             
_**2018.11.04**_
   


       

