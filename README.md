# Network_Clustering
CheckPoint's home assignment for data scientist position.

## Approach
This project involves generating a synthetic dataset of network connections (5-tuples) and clustering them based on similarities in their attributes. The dataset includes features such as:
  * Source IP
  * Source Port
  * Protocol (TCP/UDP)
  * Destination IP
  * Destination Port

The clustering process helps to identify potential patterns in the data, such as identifying frequent connections.
The clustering algorithm is influenced by a scale factor that controls the tightness or looseness of the clusters. This parameter determines how closely related the network connections should be grouped.

### Steps:

1. Data Generation: 

    A synthetic dataset is generated with 100,000 unique network connection records.
    The records are designed to represent real-world network traffic.
    Variability in the dataset is ensured by incorporating:
    A mix of common and uncommon ports.
    Connections between private and public IP addresses.
    Distribution across small and large networks.


2. Preprocessing:

    A precomputed distance matrix is used to capture the dissimilarities between connections.
    This distance matrix takes into account not just the numeric differences between IP addresses and ports, but also the protocols and the network types (small, big, public) of the source and destination involved in each connection.


3. Clustering:

    Two clustering algorithms were explored:
    K-Medoids algorithm, clusters were defined by minimizing distances between a representative medoid and the rest of the points.
    Agglomerative Clustering, a hierarchical approach to cluster the same dataset by successively merging the most similar data points.


4. Visualization:

    The results are visualized using network graphs, with clusters represented by edge colors, nodes reflecting IP addresses, and specific attributes (e.g., protocol, common/uncommon ports) influencing the visualization.


## Decisions Made
1. Clustering Algorithm:

    K-Medoids was selected as the main clustering method due to its robustness with non-Euclidean data. It uses actual data points (medoids) to represent clusters, making it more suitable for the 5-tuple connection data.
    
    Agglomerative Clustering was also applied to compare the results. This algorithm uses a hierarchical approach, merging data points into clusters based on predefined linkages (e.g., single, complete, average).


2. Distance metric was defined for clustering:
    * IP address similarity: IP addresses were converted to integers, and the distance between them was normalized.
    * Port differences: The difference between source and destination ports was scaled and         incorporated.
    * Protocol differences: TCP and UDP were treated differently, with mismatches contributing to the distance.
    * Network Type: When the network type (private, public) matched between two connections for their source and destination ip's.


3. Visualization:

    To ensure clarity in the visualization:
    Node shapes/colors reflect whether they belong to public, large, or small networks.
    Edge styles (dashed or solid) indicate whether the protocol is UDP or TCP.
    Common ports are visually distinguished from uncommon ports by node fill styles.


## Assumptions

1. There are 2 private networks
2. Small private network has 50 devices 10.0.0.[1,50]
3. Big private network has 100 devices 192.168.0.[1,100]
4. ~30% of records are within small private network
5. ~50% of records are within big private network
6. ~10% of records are between the 2 private networks
7. ~10% of records are between outside source to a private network
8. ~80% of the records are TCP and ~20% are UDP
9. ~80% of the records has common ports and ~20% has ports from [1,65535]
10. If the protocol is TCP, there is 95% chance of adding the same packet with reversed direction
11. If the protocol is UDP, there is 1% chance of adding the same packet with reversed direction
