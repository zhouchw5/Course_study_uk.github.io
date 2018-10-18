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








我们可以通过simulation of random walk，结合泰勒展开，能够得到高斯分布和扩散方程的formula。现在亦然，我们有不同的方法可以定义自然数e，例如生日，例如女儿的fraction. 女儿的算法有两种；一种是fraction的数学期望值，另一种是先算各自的期望值，再求fraction；
                    
              

_Yours,_             
_Chuwei Zhou_             
_2018.10.16_
   




