# Community Detection in a GitHub Developer Network

![KL_sample](images/kl_sample.png)

## Summary

- Analysis of a 37k-node GitHub developer network.
- Compares graph partitioning with embedding based clustering.
- Visually demonstrates how modelling choices shape the communities we observe in complex networks.

---

## What is the project about?

Social platforms such as GitHub, Instagram, and LinkedIn are built on networks of connections. We often talk about “communities,” “influence groups,” or “clusters” of users. But what exactly is a community?

There is rarely a single answer. This project shows that the way we define and detect communities can fundamentally change how we interpret a network.

Using a large GitHub developer network, we compare two approaches:

- A **connectivity-based method**, which partitions the graph by minimizing cross-group links.
- An **embedding-based method**, which groups developers based on structural similarity within the network.

Although both methods operate on the same data, they produce meaningfully different groupings and therefore yield different narratives about how the network is organized.

The central question:

> How closely do connectivity-based communities align with structural similarity learned through graph embeddings?

Understanding this distinction matters because it affects how we approach real-world tasks such as user segmentation, recommendation systems, and influence detection.

---

## Dataset

Source: UCI Machine Learning Repository  
https://archive.ics.uci.edu/dataset/588/github+musae

The dataset contains:

- 37,700 developers (nodes)
- 289,003 mutual follower relationships (edges)
- Binary label: Web vs Machine Learning developer

Nodes represent developers who have starred at least 10 repositories.  
Edges represent mutual follower relationships.

---

## Methods

The analysis combines classical network science with modern representation learning:

### Graph Analysis
- Degree distribution
- Clustering coefficients
- Eigenvector centrality
- Robustness to hub removal

### Community Detection
- Kernighan–Lin bisection
- Modularity evaluation

### Graph Embeddings and Unsupervised Learning
- Node2Vec (64-dimensional structural embeddings)
- PCA and t-SNE visualization
- K-Means clustering in embedding space

---

## Key Findings

This GitHub network is densely interconnected, with overlapping follower communities rather than sharply separated groups. Highly connected developers share large portions of their follower base, creating gradual transitions between regions of the network.

Key takeaways:

- The network is strongly hub-driven: a small number of developers account for a disproportionate share of mutual follower connections.
- Even after removing the two most influential nodes, the overall network remains largely intact, indicating structural robustness.
- Connectivity-based partitioning (Kernighan–Lin or KL) forces a clean two-way split of the graph. However, this split does not align cleanly with developer type (Web vs Machine Learning).
- When we look at the KL partition through another structural lens, the two groups are not as clearly separated as the initial split might suggest. Many developers placed into different KL communities still occupy similar structural similarities across the broader network.
- By contrast, grouping developers based on their overall pattern of connections produces clusters that appear more clearly distnguishiable. In other words, developers who “sit” in similar parts of the network tend to be grouped together, even if they are assigned to different communities under a connectivity-based split.

*Connectivity-Based Partition (Kernighan–Lin)*

![PCA KL Overlay](images/pca_kl_overlay.png)

*Embedding-Based Clustering (KMeans on Node2Vec)*

![PCA KMeans](images/pca_kmeans.png)


### So what does it all mean?

This comparison highlights a simple but important idea: community membership depends on how we choose to define it.

One approach focuses on drawing clean boundaries by reducing connections between groups. Another approach focuses on grouping users who occupy similar structural positions within the network.

Which approach is more useful depends on the question we are trying to answer:
- If the goal is to divide a network into clearly separated groups, for example, to identify factions or detect polarization, a connectivity-based method may be more appropriate.
- If the goal is to understand which users play similar roles, behave similarly, or occupy comparable positions within the broader structure, an embedding-based approach may be more informative.

Ultimately, meaningful network analysis begins with a clear objective. Different methods reveal different patterns, and **the choice of method should follow the question we care about.**

---

## Repository Structure

- `data/` — raw dataset files  
- `outputs/` — generated embeddings (intermediate CSV file)  
- `images/` — visualizations used in the README  
- `github_network_analysis.ipynb` — main analysis notebook  
- `README.md`

---

## How to Run

1. Create a Python environment (e.g., conda)
2. Install dependencies `pip install pandas numpy networkx matplotlib scikit-learn node2vec`

3. Run the notebook from top to bottom.
