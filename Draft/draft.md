# K Means Clustering

#### Point distribution 
![Scatter Plot](https://raw.githubusercontent.com/JenBanks8585/KMeans_project/main/Pics/scatter_data.png)

## Steps
### 1. Create a class object
  K Means Clustering is one of the most popular algorithm used in dealing with unsupervised data. Unsupervised data are not labeled therefore the model is unable to predict a certain value similar to a regression problem or a class as in a classification problem.  In unsupervised data, the idea is to cluster observations together based on shared commonality across its features.  This is an iterative process which means the process of fitting the model is done a few times until optimized.  
  In this post, we will create a KMeans Clustering algorith from scratch. 

```
class KMClusters:
  def __init__(self, data, K, max_iter = 100):
    self.K = K
    self.plot_figure = True
    self.max_iter = max_iter
    self.rows = data.shape[0]
    self.columns = data.shape[1]
  
```
For illustration purposes, a two- dimensional dataset will be used in this post along with the following detail as listed below:

**data:
```
X = np.array([[1,5], [2,9], [5,2], [6,5], [7,1], [3,4], [9,2], [3, 9]
              [1,7], [6,4], [3,7], [2,4], [6,3], [8,7], [1,2], [4,5]
              ])
              
K = 4
```


### 2. Initialized randomized centroids

  The centroids represent the center-most locations among a group of points. It is also referred to as the center of gravity. The first step in this algorithm is to    initialize the centroids. This can be chosen randomly or at will. In this post we will randomly choose them. The number of centroids depend on the number of clusters, K. 
Below is one implementation of this:

``` 
  def random_centroids(self, data):
    random_idx = np.random.permutation(self.rows)[:self.K]
    centroids = data[random_idx]
    return centroids
  ```
  
 This method takes in data and returns the coordinates of the initial centroids. The first line solves for randomized index from within the number of observations. For instance the dataset has a shape of 20 x 4. Then this line basically randomly chooses between 0- 19, `data.shape[0]` and from those choices, take the first K values, representing the initial centroids of the chosen K clusters.  The second line uses these indices on the data to grab their corresponding points or observations. 
 
 For instance, using clusters, K = 4, initial centroids using this method would be: 
 
 ```
 KM_instance.random_centroids(X)
 
 centroids = array([[1, 2], [9, 2], [5, 2], [6, 4]])
 
 ```
 
 ![initial centroids](https://raw.githubusercontent.com/JenBanks8585/KMeans_project/main/Pics/scatter_initial_centroids2.png)
 
 
### 3. Cluster the data points based on closest centroid

  The centroids represent the center-most locations among a group of points. It is also referred to as the center of gravity. The first step in this algorithm is to    initialize the centroids. This can be chosen randomly or at will. In this post we will randomly choose them. The number of centroids depend on the number of clusters, K. 
Below is one implementation of this:

