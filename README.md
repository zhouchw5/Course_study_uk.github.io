# Probability_My Notes and Performance in Data Analysis and Statistical Methods

In my bachelor career in Sun Yat-Sen University, Probability Theory and Statistics had different representatives of intersaction with my (Advanced) Quantum Mechanics, Complex System and Nonlinear Physics, Thermodynamics and Statistical Physics, Solid State Physics, etc. Quite interesting it is to start our story of Data Analysis and Statistical Methods with our Probability knowledge.

In the two weeks' courses storaged in the past, still some familiar concepts constructed the fundamentals, like the definition of Independence, the Conditional Probability, Law of Total Probability, Bayes' Formula, etc. And what I would like to mention in detail in this letter is some simple interesting techiques and some microscopic thinking about the Euler's Number.              
             
- _**Use the chocolates to generate the Euler's Number**_             

Considering a box of **n chocolates** with all of different shapes, your daughter dropped them all on the ground and you need to put them back in the box randomly. The probability that every chocolate goes back to the wrong spot is **p(n)**, when we take the limitation 
<a href="https://www.codecogs.com/eqnedit.php?latex=$n&space;\to&space;\infty$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$n&space;\to&space;\infty$" title="$n \to \infty$" /></a>
, we can obtain that the probability goes to **1/e**.             
             
<a href="https://www.codecogs.com/eqnedit.php?latex=$A_i$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$A_i$" title="$A_i$" /></a>: denotes the event that the i-th chocolate is put in the right spot.         
          
          
<a href="https://www.codecogs.com/eqnedit.php?latex=$1-P(\cup&space;A_i)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$1-P(\cup&space;A_i)$" title="$1-P(\cup A_i)$" /></a>
: The probability that every chocolate goes back to the wrong spot;          
           
Using the inclusive-exclusive principle:           
<a href="https://www.codecogs.com/eqnedit.php?latex=$P(\cup&space;A_i)&space;=&space;\sum_{i=1}^{n}P(A_i)&space;-&space;\sum_{1\leq&space;i<&space;j\leq&space;n}&space;P(A_{i}A_{j})&space;&plus;&space;...&plus;(-1)^{n-1}P(A_{1}...A_{n})$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$P(\cup&space;A_i)&space;=&space;\sum_{i=1}^{n}P(A_i)&space;-&space;\sum_{1\leq&space;i<&space;j\leq&space;n}&space;P(A_{i}A_{j})&space;&plus;&space;...&plus;(-1)^{n-1}P(A_{1}...A_{n})$" title="$P(\cup A_i) = \sum_{i=1}^{n}P(A_i) - \sum_{1\leq i< j\leq n} P(A_{i}A_{j}) + ...+(-1)^{n-1}P(A_{1}...A_{n})$" /></a>             
<a href="https://www.codecogs.com/eqnedit.php?latex=$P(\cup&space;A_i)&space;=&space;\sum_{i=1}^{n}(-1)^{i-1}\cdot&space;C_{n}&space;^{i}&space;\cdot&space;A_{n-i}&space;^&space;{n-i}&space;/&space;A_{n}&space;^{n}&space;$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$P(\cup&space;A_i)&space;=&space;\sum_{i=1}^{n}(-1)^{i-1}\cdot&space;C_{n}&space;^{i}&space;\cdot&space;A_{n-i}&space;^&space;{n-i}&space;/&space;A_{n}&space;^{n}&space;$" title="$P(\cup A_i) = \sum_{i=1}^{n}(-1)^{i-1}\cdot C_{n} ^{i} \cdot A_{n-i} ^ {n-i} / A_{n} ^{n} $" /></a>            
<a href="https://www.codecogs.com/eqnedit.php?latex=$P(\cup&space;A_i)&space;=&space;\sum_{i=1}^{n}(-1)^{i-1}&space;/&space;i!&space;$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$P(\cup&space;A_i)&space;=&space;\sum_{i=1}^{n}(-1)^{i-1}&space;/&space;i!&space;$" title="$P(\cup A_i) = \sum_{i=1}^{n}(-1)^{i-1} / i! $" /></a>          
           
Based on the Taylor series of
 <a href="https://www.codecogs.com/eqnedit.php?latex=$e^x$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$e^x$" title="$e^x$" /></a> we can know that:              
<a href="https://www.codecogs.com/eqnedit.php?latex=$\lim_{n&space;\to&space;\infty&space;}&space;P(\bigcup_{i=1}^{n}&space;A_i)&space;=&space;1-e^{-1}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$\lim_{n&space;\to&space;\infty&space;}&space;P(\bigcup_{i=1}^{n}&space;A_i)&space;=&space;1-e^{-1}$" title="$\lim_{n \to \infty } P(\bigcup_{i=1}^{n} A_i) = 1-e^{-1}$" /></a>                          
p(n-> infinite chocolates all go to the wrong spots) =
 <a href="https://www.codecogs.com/eqnedit.php?latex=$e^{-1}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$e^{-1}$" title="$e^{-1}$" /></a>             
           
Thus we can see that when n -> infinite in this case, the probability of all chocolate returning to the right spots can generate the reciprocal of the Eular's Number. I think this's also another way to define the value of the Euler's Numer. It is enlightening that we can obtain/find some macroscopic formulas/principles/theorems by integrating a great deal of microscopic processes based on rules of inconspicuous certainty, like what we did in Complex Systems and Nonlinear Physics, generating the formulas of Gaussian Distribution and diffusion equation by random walk simulation.                    
           
                      
                       
                       
- _**Daughter helps you generate the Eular's Number**_

In a society one couple would stop having more kids until they have daughter (supposing that each child have a probability 1/2 to be a girl), what will happen eventually to the fraction of girls in this society? Initially I calculated the expectation of fraction directly.                           
<a href="https://www.codecogs.com/eqnedit.php?latex=$E(p)&space;=&space;1\cdot(1/2)&plus;(1/2)\cdot&space;(1/2)^2&space;&plus;&space;(1/3)\cdot&space;(1/2)^3&plus;...$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$E(p)&space;=&space;1\cdot(1/2)&plus;(1/2)\cdot&space;(1/2)^2&space;&plus;&space;(1/3)\cdot&space;(1/2)^3&plus;...$" title="$E(p) = 1\cdot(1/2)+(1/2)\cdot (1/2)^2 + (1/3)\cdot (1/2)^3+...$" /></a>             
<a href="https://www.codecogs.com/eqnedit.php?latex=$E(p)&space;=&space;\sum_{i=1}^{\infty}&space;(1/i)&space;\cdot&space;(1/2)^i$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$E(p)&space;=&space;\sum_{i=1}^{\infty}&space;(1/i)&space;\cdot&space;(1/2)^i$" title="$E(p) = \sum_{i=1}^{\infty} (1/i) \cdot (1/2)^i$" /></a>                        
<a href="https://www.codecogs.com/eqnedit.php?latex=$E(p)&space;=&space;\sum_{i=1}^{\infty}&space;\int_{0}^{1/2}x^{i-1}dx$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$E(p)&space;=&space;\sum_{i=1}^{\infty}&space;\int_{0}^{1/2}x^{i-1}dx$" title="$E(p) = \sum_{i=1}^{\infty} \int_{0}^{1/2}x^{i-1}dx$" /></a>                     




 











我们可以通过simulation of random walk，结合泰勒展开，能够得到高斯分布和扩散方程的formula。现在亦然，我们有不同的方法可以定义自然数e，例如生日，例如女儿的fraction. 女儿的算法有两种；一种是fraction的数学期望值，另一种是先算各自的期望值，再求fraction；
                    
              

_Yours,_             
_Chuwei Zhou_             
_2018.10.16_
   




