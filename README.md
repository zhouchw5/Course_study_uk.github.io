# Fundamental Performances of Statistics Methods via R/Python

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










 











                    
              

_**Yours,**_             
_**Chuwei Zhou**_             
_**2018.11.04**_
   


       

