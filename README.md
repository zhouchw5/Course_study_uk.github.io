# Fundamentals of Operations Research & Analytics_20181105

- **Any two states in the same class of a Markov chain have the same period**            
The key point to conclude it is that we should formula the communication between states A and B:            
<a href="https://www.codecogs.com/eqnedit.php?latex=$p_{AA}^{n_{1}&plus;n_{2}&plus;n_{3}}&space;=&space;\sum_{i}p_{AB}^{(i)}&space;p_{BB}^{(n_{2})}&space;p_{BA}^{(n_{1}-i)}p_{AA}^{(n_{3})}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$p_{AA}^{n_{1}&plus;n_{2}&plus;n_{3}}&space;=&space;\sum_{i}p_{AB}^{(i)}&space;p_{BB}^{(n_{2})}&space;p_{BA}^{(n_{1}-i)}p_{AA}^{(n_{3})}$" title="$p_{AA}^{n_{1}+n_{2}+n_{3}} = \sum_{i}p_{AB}^{(i)} p_{BB}^{(n_{2})} p_{BA}^{(n_{1}-i)}p_{AA}^{(n_{3})}$" /></a>                    
where we know that
 <a href="https://www.codecogs.com/eqnedit.php?latex=$(n_1&space;&plus;&space;n_2&space;&plus;&space;n_3)$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$(n_1&space;&plus;&space;n_2&space;&plus;&space;n_3)$" title="$(n_1 + n_2 + n_3)$" /></a>
 should be the multiple of the period of A.         
And then we can reformula the equation as:                
<a href="https://www.codecogs.com/eqnedit.php?latex=$p_{AA}^{n_{1}&plus;n_{2}&plus;n_{3}}&space;=&space;\sum_{i}&space;p_{AB}^{(i)}&space;p_{BB}^{(n_{2})}&space;p_{BA}^{(n_{1}-i)}&space;p_{AA}^{(n_{3})}&space;=&space;\sum_{i}&space;p_{BA}^{(n_{1}-i)}p_{AA}^{(n_{3})}&space;p_{AB}^{(i)}&space;p_{BB}^{(n_{2})}&space;=&space;p_{BB}^{n_{1}&plus;n_{2}&plus;n_{3}}&space;$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$p_{AA}^{n_{1}&plus;n_{2}&plus;n_{3}}&space;=&space;\sum_{i}&space;p_{AB}^{(i)}&space;p_{BB}^{(n_{2})}&space;p_{BA}^{(n_{1}-i)}&space;p_{AA}^{(n_{3})}&space;=&space;\sum_{i}&space;p_{BA}^{(n_{1}-i)}p_{AA}^{(n_{3})}&space;p_{AB}^{(i)}&space;p_{BB}^{(n_{2})}&space;=&space;p_{BB}^{n_{1}&plus;n_{2}&plus;n_{3}}&space;$" title="$p_{AA}^{n_{1}+n_{2}+n_{3}} = \sum_{i} p_{AB}^{(i)} p_{BB}^{(n_{2})} p_{BA}^{(n_{1}-i)} p_{AA}^{(n_{3})} = \sum_{i} p_{BA}^{(n_{1}-i)}p_{AA}^{(n_{3})} p_{AB}^{(i)} p_{BB}^{(n_{2})} = p_{BB}^{n_{1}+n_{2}+n_{3}} $" /></a>                   
That means the
 <a href="https://www.codecogs.com/eqnedit.php?latex=$n_1&space;&plus;&space;n_2&space;&plus;&space;n_3$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$n_1&space;&plus;&space;n_2&space;&plus;&space;n_3$" title="$n_1 + n_2 + n_3$" /></a>
 should also be the multiple of the period of B.               
And obviously
 <a href="https://www.codecogs.com/eqnedit.php?latex=$n_2$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$n_2$" title="$n_2$" /></a>
 and
 <a href="https://www.codecogs.com/eqnedit.php?latex=$n_1$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$n_1$" title="$n_1$" /></a>
 should both be the multiples of the period of B. Thus
 <a href="https://www.codecogs.com/eqnedit.php?latex=$n_3$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$n_3$" title="$n_3$" /></a>
 should also be the mutiple of the period of B. It means that for all n with:                
<a href="https://www.codecogs.com/eqnedit.php?latex=$p_{AA}^{(n)}>0$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$p_{AA}^{(n)}>0$" title="$p_{AA}^{(n)}>0$" /></a>                          
n should be the multiple of the period of B. So A and B should have the same period.                        



 




                    
              

_**Yours,**_             
_**Chuwei Zhou**_             
_**2018.11.05**_
   


       

