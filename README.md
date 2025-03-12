## Introduction
This repository implements image segmentation using two popular methods: **K-Means clustering** and the **Normalized Cut algorithm**. Image segmentation is the process of partitioning an image into meaningful regions for further analysis.

---

## Methodology
### 1. K-Means Clustering
K-Means is an unsupervised clustering algorithm that partitions an image into $K$ clusters by minimizing intra-cluster variance. The steps are as follows:

1. **Initialization**: Select $K$ cluster centroids randomly.
2. **Assignment Step**: Assign each pixel $x_i$ to the nearest cluster centroid:<br>
   $$C_j = \{ x_i \mid \arg \min_k || x_i - \mu_k ||^2 \},$$<br>
   where $\mu_k$ is the centroid of cluster $k$.
3. **Update Step**: Compute new centroids by taking the mean of all pixels assigned to each cluster:<br>
   $$\mu_k = \frac{1}{|C_k|} \sum_{x_i \in C_k} x_i.$$ <br>
4. Repeat steps 2 and 3 until convergence (i.e., centroids do not change significantly).

K-Means is computationally efficient but may not always produce the best segmentation since it does not consider spatial relationships between pixels.

### 2. Normalized Cut (N-Cut)
The **Normalized Cut** method formulates segmentation as a graph partitioning problem. The image is modeled as a graph $G = (V, E)$, where pixels are nodes, and edges encode similarity between pixels. Given a partition $(A, B)$, the N-cut is defined as:

$$\text{N-cut}(A, B) = \frac{W(A, B)}{W(A, A) + W(A, B)} + \frac{W(A, B)}{W(B, B) + W(A, B)}$$
where:
- $W(A, B)$ is the total weight of edges connecting regions A and B,
- $W(A, A)$ and $W(B, B)$ are the total weights of edges within A and B, respectively.

The algorithm follows these steps:
1. Construct a weighted graph based on pixel intensities or color features.
2. Compute the graph Laplacian and solve the generalized eigenvalue problem: <br>
   $(D - W) v = \lambda D v$ <br>
   where $W$ is the adjacency matrix and $D$ is the degree matrix.
4. Use the eigenvectors to find the optimal partition by minimizing the N-cut criterion.

N-cut provides better segmentation results compared to K-Means by incorporating spatial continuity but is computationally expensive.

---

## Results
refer to report.pdf for results


## References
- J. Shi and J. Malik, "Normalized Cuts and Image Segmentation," IEEE Transactions on Pattern Analysis and Machine Intelligence, 2000.
- A. K. Jain, "Data Clustering: 50 Years Beyond K-Means," Pattern Recognition Letters, 2010.

---


