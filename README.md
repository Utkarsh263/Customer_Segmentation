# 🛒 SmartCart – Customer Segmentation using Machine Learning

SmartCart is an unsupervised machine learning project that segments retail customers based on their demographics, purchasing behavior, and marketing interactions.

The project performs data preprocessing, feature engineering, dimensionality reduction using PCA, and customer segmentation using **K-Means Clustering**. An additional **Agglomerative Clustering** model is implemented for comparison.

---

# Dataset

The dataset contains marketing information for **2,240 customers** with **22 raw features**.

It includes:

### Customer Information
- Year of Birth
- Education
- Marital Status
- Income
- Number of Children
- Customer Enrollment Date

### Customer Behavior
- Recency
- Number of Web Purchases
- Number of Store Purchases
- Number of Catalog Purchases
- Number of Web Visits
- Campaign Responses

### Product Spending
- Wines
- Fruits
- Meat Products
- Fish Products
- Sweet Products
- Gold Products

---

# Project Workflow

## 1. Data Preprocessing

### Missing Value Handling

- Income contains **24 missing values**
- Missing values are replaced using the **median** income.

---

### Feature Engineering

Several new customer-level features are created.

| New Feature | Description |
|-------------|-------------|
| Age | 2026 − Year_Birth |
| Customer_Tenure_Days | Days since customer enrollment |
| Total_Spending | Sum of spending across all six product categories |
| Total_Children | Kidhome + Teenhome |
| Education | Reduced to Undergraduate / Graduate / Postgraduate |
| Living_With | Reduced to Partner / Alone |

After feature creation, redundant columns are removed:

- ID
- Year_Birth
- Dt_Customer
- Marital_Status
- Kidhome
- Teenhome
- Individual spending columns

---

## 2. Outlier Removal

Potential outliers are first inspected using pairplots.

Two filtering rules are then applied:

- Age < 90
- Income < 600,000

These thresholds remove unrealistic customer records while preserving the overall data distribution.

---

## 3. Encoding

Categorical features:

- Education
- Living_With

are transformed using **One-Hot Encoding**.

---

## 4. Feature Scaling

All features are standardized using **StandardScaler**.

Scaling is essential because K-Means relies on Euclidean distance, making it sensitive to feature magnitude.

---

## 5. Dimensionality Reduction

Principal Component Analysis (PCA) reduces the dataset to **3 principal components**.

Benefits:

- Removes feature redundancy
- Speeds up clustering
- Enables 3D visualization
- Preserves approximately **45% of the dataset variance**

---

# Selecting the Optimal Number of Clusters

## Elbow Method

K-Means is trained for:

```
k = 1 → 10
```

For each value of k, the **Within Cluster Sum of Squares (WCSS)** is calculated.

The optimal value is automatically detected using **KneeLocator** instead of selecting the elbow manually.

---

## Silhouette Score

To validate the Elbow Method, the Silhouette Score is computed for:

```
k = 2 → 10
```

The silhouette score evaluates:

- Cluster cohesion
- Cluster separation

Higher values indicate better-defined clusters.

---

## Final Choice

Both evaluation methods indicate:

```
Optimal Number of Clusters = 4
```

---

# Customer Segmentation

## K-Means Clustering (Primary Model)

```python
kmeans = KMeans(
    n_clusters=4,
    random_state=42
)

labels_kmeans = kmeans.fit_predict(X_pca)
```

K-Means partitions customers into four groups by iteratively:

1. Initializing centroids
2. Assigning customers to the nearest centroid
3. Updating centroid locations
4. Repeating until convergence

The model is trained on the PCA-transformed feature space.

---

## Agglomerative Clustering (Comparison Model)

```python
agg_clf = AgglomerativeClustering(
    n_clusters=4,
    linkage="ward"
)

labels_agg = agg_clf.fit_predict(X_pca)
```

Ward linkage merges clusters by minimizing within-cluster variance.

This model is included only to compare clustering behavior with K-Means.

---

# Cluster Characteristics

| Cluster | Avg Income | Avg Spending | Web Purchases | Catalog Purchases | Store Purchases | Campaign Response |
|---------|------------|--------------|---------------|-------------------|-----------------|-------------------|
| 0 | ~39,680 | ~222 | 3.15 | 0.97 | 4.14 | 7.6% |
| 1 | ~72,808 | ~1,237 | 5.69 | 5.50 | 8.66 | 16.7% |
| 2 | ~36,960 | ~166 | 2.71 | 0.84 | 3.62 | 14.2% |
| 3 | ~70,723 | ~1,190 | 5.79 | 5.01 | 8.43 | 32.0% |

---

# Customer Insights

### Cluster 0

- Moderate income
- Low spending
- Mostly store shoppers
- Low campaign response

---

### Cluster 1

- High income
- High spending
- Active across all purchasing channels
- Good campaign engagement

---

### Cluster 2

- Lowest income
- Lowest spending
- Limited purchasing activity
- Primarily offline shoppers

---

### Cluster 3

- High income
- High spending
- Most responsive to marketing campaigns
- Valuable target customers

---

# Visualizations

The project includes:

- Pairplots
- Correlation Heatmap
- PCA 3D Projection
- Elbow Curve
- Silhouette Score Curve
- K-Means 3D Clusters
- Agglomerative 3D Clusters
- Cluster Count Plot
- Income vs Spending Scatter Plot
- Cluster Summary Statistics

---

# Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- PCA
- K-Means
- Agglomerative Clustering
- StandardScaler
- OneHotEncoder
- KneeLocator

---

# Future Improvements

- DBSCAN for density-based clustering
- Gaussian Mixture Models (GMM)
- Customer Lifetime Value (CLV) estimation
- RFM-based customer segmentation
- Interactive dashboard using Streamlit or Power BI
- Automated cluster labeling and business recommendations

---
