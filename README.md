# Support Vector Machine______Reading, Performance and Practice

Acknowledgement: Thanks for the coding instructions from _Python Data Science Handbook_ written by Jake VanderPlas                                 

Support Vector Machine is a machine learning method for data classification and prediction. For sake of simplicity, two-dimensional cases are a good beginning to introduce the decision-making by SVM. When mapping data into a two-dimensional diagram, we can see that different types of data tend to converge into different clusters. And the data classification needs to find a margin between different clusters with the maximum width so that the boundary of one data group can be away from the other one as far as possible. After finishing the classification map, the prediction process is to map a new data point into the diagram and see which group/cluster it would be located in, estimating that it has the same characteristic value as that of the data point in the same group. And a wider margin would inrease the accuracy of the prediction for the characteristic value of a new data point. The middle of the margin could be a line or curve in these two-dimensional cases. And with extension to higher dimensional space, a manifold would serve for dividing the classes from each other. More details in the contraint optimization problems on Support Vector Machine can be shown in another letter of mine for more theoretical and mathematical stories like Karush-Kuhn-Tucker Condition ([Easy Access to that letter](https://github.com/zhouchw5/Course_study_uk.github.io/blob/support-vector-machine/APPENDIX_mathpart1.0.pdf)).                            
                   
                   
Firstly we construct two classes of well separated points to perform a simple case for classification task.            
To begin with the standard imports:             
```python
# matplotlib inline
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats

# use Seaborn plotting defaults
import seaborn as sns; sns.set()
```
                  
Generate two clusters of data points:              
We utilize the make_blobs function to generate two clusters, where X is an array of two-dimensional vectors (data points) converging to different centers, with the array y listing "0" or "1" notating the different clusters of data points. And len(X) == len(y). Hence in the scatter plotting, "c=y" means that if y==0, the data points would have color A, else if y==1, the data points would have color B.               

```python
# we can adjust the parameters like the standard deviation cluster_std to obtain different distribution of dots with different levels of randomness
from sklearn.datasets.samples_generator import make_blobs
X, y = make_blobs(n_samples=50, centers=2,
random_state=0, cluster_std=0.60)
plt.scatter(X[:, 0], X[:, 1], c=y, s=50, cmap='spring')
```
![dataclusters](https://github.com/zhouchw5/Course_study_uk.github.io/blob/support-vector-machine/dataclusters.png)                                  
It can be shown in the figure above that we could have more than one possible dividing line that can perfectly discriminate between the two classes.            
```python
xfit = np.linspace(-1, 3.5)
plt.scatter(X[:, 0], X[:, 1], c=y, s=50, cmap='spring')
plt.plot([0.6], [2.1], 'x', color='red', markeredgewidth=2, markersize=10)
for m, b in [(1, 0.65), (0.5, 1.6), (-0.2, 2.9)]:
    plt.plot(xfit, m * xfit + b, '-k')
plt.xlim(-1, 3.5);
```
![discriminate](https://github.com/zhouchw5/Course_study_uk.github.io/blob/support-vector-machine/discriminative.png)        
These are three different separators that, nevertheless, perfectly discriminate between these samples. And we can see that depending on which we choose, a new data point marked as "X" in the figure could be assigned a different label. That's why we need an optimal solution for the division avoiding the uncertainty of predication for a data point.             
                     
To add a margin for each line, in which the line is the midline.              
```python
xfit = np.linspace(-1, 3.5)
plt.scatter(X[:, 0], X[:, 1], c=y, s=50, cmap='spring')

for m, b, d in [(1, 0.65, 0.33), (0.5, 1.6, 0.55), (-0.2, 2.9, 0.2)]:
    yfit = m * xfit + b
    plt.plot(xfit, yfit, '-k')
    plt.fill_between(xfit, yfit - d, yfit + d, edgecolor='none', color='#AAAAAA',
                     alpha=0.4)
plt.xlim(-1, 3.5)
```
![line with margin](https://github.com/zhouchw5/Course_study_uk.github.io/blob/support-vector-machine/line%20with%20margin.png)
As we have mentioned at the very beginning, the division line with the widest margin is what we should choose for data classification. Support vector machines are an example of such a maximum margin estimator.                  
                    
we can use the Scikit-Learn's support vector classfier to train an SVM model on our data, by selecting one of different kernels corresponding to different types of classfiers.            
               
Yours,                
Chuwei Zhou                   
2019.2.18              
