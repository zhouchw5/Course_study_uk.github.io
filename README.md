# Support Vector Machine______Reading, Performance and Practice

Acknowledgement: Thanks for the coding instructions from _Python Data Science Handbook_ written by Jake VanderPlas                                 

Support Vector Machine is a machine learning method for data classification and prediction. For sake of simplicity, two-dimensional cases are a good beginning to introduce the decision-making by SVM. When mapping data into a two-dimensional diagram, we can see that different types of data tend to converge into different clusters. And the data classification needs to find a margin between different clusters with the maximum width so that the boundary of one data group can be away from the other one as far as possible. After finishing the classification map, the prediction process is to map a new data point into the diagram and see which group/cluster it would be located in, estimating that it has the same characteristic value as that of the data point in the same group. And a wider margin would inrease the accuracy of the prediction for the characteristic value of a new data point. The middle of the margin could be a line or curve in these two-dimensional cases. And with extension to higher dimensional space, a manifold would serve for dividing the classes from each other. More details in the contraint optimization problems on Support Vector Machine                    
                   
                   
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
                                 
                                 
               
Yours,                
Chuwei Zhou                   
2019.2.18              
