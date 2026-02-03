# KMeans Customer Segmentation – Mall Customers

## Problem Overview
Customer segmentation is an unsupervised learning task aimed at grouping customers based on similar purchasing behavior. This project uses KMeans clustering to segment mall customers using their annual income and spending score, helping businesses understand customer types and improve marketing strategies.

## Dataset Description
The dataset contains customer information collected from a shopping mall. Only behavior-related features are used for clustering.

Features used:
- Annual Income (k$)
- Spending Score (1–100)

Feature removed:
- CustomerID (identifier, not useful for clustering)

## Model Used
KMeans Clustering is a centroid-based unsupervised learning algorithm that partitions data into K clusters by minimizing within-cluster variance.

Reason for choosing KMeans:
- Efficient for numerical data
- Works well for customer segmentation
- Simple and interpretable

## Feature Scaling
StandardScaler is applied before clustering to normalize features. This ensures that income and spending score contribute equally to distance calculations.

## Selecting Number of Clusters
The Elbow Method is used to determine the optimal number of clusters. Inertia is calculated for different values of K, and the point where the decrease in inertia slows down indicates the optimal cluster count. Based on the elbow curve, K = 5 is selected.

## Model Configuration
- Algorithm: KMeans
- Number of Clusters: 5
- Initialization: k-means++
- Distance Metric: Euclidean
- Random State: 42

## Cluster Visualization
Clusters are visualized using a scatter plot with:
- X-axis: Annual Income (k$)
- Y-axis: Spending Score (1–100)

Each color represents a different customer segment.

## Cluster Interpretation
The clusters generally represent:
- High income, high spending customers
- High income, low spending customers
- Low income, high spending customers
- Low income, low spending customers
- Average income and average spending customers

## Output
The final dataset includes an additional column:
- Cluster: Indicates the customer segment assigned by KMeans

This segmented dataset can be used for targeted marketing, customer profiling, and business decision-making.

## Conclusion
This project demonstrates the application of unsupervised learning for customer segmentation. KMeans clustering successfully identifies distinct customer groups based on spending behavior, enabling data-driven marketing strategies.
