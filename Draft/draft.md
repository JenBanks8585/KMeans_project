
## Steps
### 1. Initialized randomized centroids
####      The centroids represent the center-most locations among a group of points. It is also referred to as the center of gravity. The first step in this algorithm is to    initialize the centroids. This can be chosen randomly or at will. In this post we will randomly choose them. The number of centroids depend on the number of clusters, K. 
Below is one implementation of this:

``` 
def random_centroids(self, data):
  random_idx = np.random.permutation(data.shape[0])[:K]
  centroids = data[random_idx]
  return centroids
  ```
  
 This method takes in data and returns the coordinates of the initial centroids. The first line solves for randomized index from within the number of observations. For instance the dataset has a shape of 20 x 4. Then this line basically randomly chooses between 0- 19, `data.shape[0]` and from those choices, take the first K values, representing the initial centroids of the chosen K clusters.  The second line uses these indices on the data to grab their corresponding points or observations. 
