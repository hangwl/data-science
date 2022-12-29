How do we perform clustering in practice?\
K-Means Clustering is the most popular clustering method

How it works (imagine 2D scatterplot):
1. Choose k number of clusters
2. Specify the cluster seeds (a starting centroid chosen at random or specified by the data scientist based on prior knowledge on the data)
3. Assign each point to a centroid (colour all points based on their euclidean distance)
4. Adjust the centroids
5. Repeat iterations of steps 3-4 if necessary

Basics of Cluster Analysis:
- Import relevant libraries
- Load the Data
- Plot the Data
- Select the Features
- Clustering
- Clustering Results

For Categorical Features, use map method to assign numerical values before clustering.

How to decide the optimal number of clusters?
- we want WCSS (within-cluster sum of squares) to be as low as possible, with a small number of clusters so that we can interpret them
- use the Elbow method (plot WCSS against number of clusters to see a visual representation of an optimal 'elbow')

Pros and Cons of K-Means Clustering\
Pros:
- Simple to understand
- Fast to cluster
- Widely Available
- Easy to implement
- Always yield a result* (possibly also a con)
Cons + Remedy:
- We need to pick K > Elbow method
- K-means is sensitive to initialization (initial centroids(seeds)) > K-means++ chooses the most appropriate seeds 
- Sensitive to outliers > Remove outliers
- Produces spherical solutions
- Standardization

Note on Standardization\
Depending on the data, standardization of data can change how k-means clusters are chosen.\
It is usually good practice to standardize data before clustering. (But not necessarily all the time)

Clustering can help us identify OVB.

Market Segmentation

How is clustering actually useful?\
Types of Analysis:
1. Exploratory
    - Get acquainted with data
    - Search for patterns
    - Plan and determine which methods may be useful to investigate further
    - Techniques: DataViz, Descriptive Statistics, Clustering

2. Confirmatory and Explanatory
    - Explain a phenomenon, Confirm a hypothesis, or Validate a previous research


