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
 
 centroids = array([[1, 5], [2, 9], [5, 2], [6, 5]])
 
 ```
 
 ![initial centroids](https://raw.githubusercontent.com/JenBanks8585/KMeans_project/main/Pics/centroid0.png)
 
 
### 3. Cluster the data points based on closest centroid

  Once the centroids are initialized, The distance of each point in the dataset will be computed from each of the initialized centroids.  For the purposes of this post, I will use Euclidean distance.  Each point will be assigned a cluster group based on proximity. The `create_clusters` method takes in the dataset and outputs the list of clusters where each cluster is also a list of indices of the points that belong to that group. 
  
 ```
   def create_clusters(self, data):
 (a)   clusters = [[] for _ in range(self.K)]

 (b)   for point_idx, point in enumerate(data):
 (c)     closest_idx =np.argmin([np.linalg.norm(data-centroid) for centroid in self.random_centroids(data)])
 (d)     clusters[closest_idx].append(point_idx)
    
 (e)   return clusters
```

In line (a), a list of empty list is instantiated and assigned a variable name called `clusters`.
In line (b), a `for loop` is created to iterate over indices of the dataset and their corresponding points. 
In line (c), calling `linalg.norm()` computes the distance of two points, this is iterated across all points, againts all K number of centroids, in this case 4. The index of the smallest distance from each centroid is then saved to variable `closest_idx`.
In line (d), each corresponding index of the datapoints is appended to the cluster where the centroid they are closest to is a part of.
In line (e), the function returns a list of clusters.

In this example, when this method is called, the following indices are grouped into their corresponding clusters as also shown in the figure above.

```
KM_instance.create_clusters(X)
clusters = [[14, 8, 11, 5, 0], [1, 7, 10], [2, 12, 4], [15, 9, 3, 13]]
```

 ![initial centroids](https://raw.githubusercontent.com/JenBanks8585/KMeans_project/main/Pics/centroid1.png)
