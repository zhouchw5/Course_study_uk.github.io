# Support Vector Machine______Reading, Performance and Practice

Acknowledgement: Thanks for the instructions from _Python Data Science Handbook_ written by Jake VanderPlas                                 

Support Vector Machine is a machine learning method for data classification and prediction. For sake of simplicity, two-dimensional cases are a good beginning to introduce the decision-making by SVM. When mapping data into a two-dimensional diagram, we can see that different types of data tend to converge into different clusters. And the data classification needs to find a margin between different clusters with the maximum width so that the boundary of one data group can be away from the other one as far as possible. After finishing the classification map, the prediction process is to map a new data point into the diagram and see which group/cluster it would be located in, estimating that it has the same characteristic value as that of the data point in the same group. And a wider margin would inrease the accuracy of the prediction for the characteristic value of a new data point. The middle of the margin could be a line or curve in these two-dimensional cases. And with extension to higher dimensional space, a manifold would serve for dividing the classes from each other.            
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


