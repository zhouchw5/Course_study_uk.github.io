# Basic Curiosity_My Notes and Performance of Fundamentals of Operations Research & Analytics

Two weeks' courses have been storaged in the past. As I used to do in physics, I should be intuitively curious about the most simple fundamental of a new course (connecting to my past) and the most frugal orientation of the story (connecting to my future), like the 
principle of least action in physics. The elementary fundamental of the course Operations is our familiar linear programming. And a frugal curiosity is that when I transfer a primal problem into the standard form, whether I can formula the objective function directly by the linear combination of all the constraints, which can obtain the objective value instantly. But the actual cases are more complicated than the our frugal expectations. Firstly when the n(coefficients in the objective function) is greater than the n(constraints), it meas that in the method of undetermined coefficients to compute the weight of each constraint, it would happen that n(equations) > n(variables), in most general cases which would have no solutions. What if n(equations) > n(variables)?     
   

为什么我们需要duality，其实是源于一个最朴素的想法，即化成standard form之后，如果objective function能够写成是constraint的linear combination，那就最好了。但是情况不会有那么理想的。比如目标函数的系数个数大于constraint数，亦即待定系数求constraint的线性组合系数时，方程个数大于变量数，一般情况下是无解的。如果方程个数等于变量数就一定有解了吗？不一定。这个就是下面的描述。所以更一般而言，我们需要讨论constraint的线性相关性，当我们找不到一个set的系数使得constraint线性组合为目标函数时，难道我们就没办法求最优解了吗？当然不是，我们很强大的。这个时候就需要系统学习duality的知识，这个就是学习的真正目的。

虽说一般而言，n个方程解m个未知数，when n<m, generally解不唯一，但也有例外。比如两个方程解三个变量，如果其中是一条直线，那很可能只有唯一解或者没有解。即使是两个平面，也有可能是两个平行平面而导致没有解。


有很多未竟的逻辑模块，比如strong duality的证明，以及all possible cases的证明；等等。

我能不能把原来infeasible problem的最后一个constraint写成目标函数呢？


