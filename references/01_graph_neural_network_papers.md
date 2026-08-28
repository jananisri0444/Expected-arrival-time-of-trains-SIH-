# Graph Neural Network Papers — Railway Delay Prediction

## Indian Railways–specific (directly relevant)

1. **"RSTGCN: Railway-centric Spatio-Temporal Graph Convolutional Network for Train Delay Prediction,"** arXiv:2510.01262, 2025.
   https://arxiv.org/abs/2510.01262 · https://arxiv.org/html/2510.01262 (HTML) · https://arxiv.org/pdf/2510.01262 (PDF)
   Builds a nationwide temporal railway delay dataset for the Indian Railway network, integrates train frequency into the spatial modeling, and reports the model outperforms existing baselines especially in dense, high-traffic zones where delay propagation is significant. This is the closest existing precedent for the graph-based design proposed here — it validates both the graph architecture choice and the "train frequency as an edge/node feature" idea used in the graph construction.

## Foundational Spatio-Temporal Graph Architectures for Train Delay

2. **D. Zhang, Y. Peng, Y. Zhang, D. Wu, H. Wang, H. Zhang**, "Train Time Delay Prediction for High-Speed Train Dispatching Based on Spatio-Temporal Graph Convolutional Network," *IEEE Trans. Intelligent Transportation Systems*, 23:2434–2444, 2021. (Introduces TSTGCN — Train Spatio-Temporal Graph Convolutional Network.)
   Referenced via: https://link.springer.com/chapter/10.1007/978-981-99-4626-6_54
   Core architecture reference for combining spatial graph convolution (stations/sections as graph structure) with temporal modeling of recent/daily/weekly delay patterns — directly informs the spatio-temporal module design in this project's graph approach.

3. **J.S. Heglund, P. Taleongpong, S. Hu, H.T. Tran**, "Railway Delay Prediction with Spatial-Temporal Graph Convolutional Networks," *2020 IEEE 23rd Intl. Conf. on Intelligent Transportation Systems (ITSC)*, 2020, pp. 1–6.
   Early foundational application of STGCN specifically to railway delay prediction — informs the base spatial-graph-convolution + temporal-sequence architecture pattern.

4. **P. Huang, J. Guo, S. Liu, F. Corman**, "Explainable Train Delay Propagation: A Graph Attention Network Approach," *Transportation Research Part E: Logistics and Transportation Review*, vol. 184, p. 103457, 2024.
   Uses Graph Attention Networks (GAT) specifically for train delay propagation, with an explainability angle (attention weights indicate which neighboring nodes/trains most influenced a given delay prediction) — directly relevant for choosing GAT over plain GCN when interpretability of "which station/train caused this delay" matters for operational dashboards.

5. **"An Interpretable Station Delay Prediction Model Based on Graph Community Neural Network and Time-Series Fuzzy Decision Tree,"** *IEEE Transactions on Fuzzy Systems*, vol. 31, no. 2, pp. 421–433, 2022.
   Referenced via: https://cse.iitkgp.ac.in/~abhijnan/papers/chowdhury_rail_network_delay_prediction.pdf
   Combines graph-community detection (identifying clusters of stations/sections that behave similarly) with interpretable decision-tree-style output — relevant if the project wants to cluster the network into sub-regions (e.g., by zone) before applying graph convolution, rather than treating the whole national network as one graph.

## Network-Feature Studies Supporting the Graph Framing

6. **"Predicting Delayed Trajectories Using Network Features: A Study on the Dutch Railway Network,"** arXiv:2507.11776, 2025.
   https://arxiv.org/abs/2507.11776 · https://arxiv.org/pdf/2507.11776
   Demonstrates that network-level features (not just single-train history) meaningfully improve delay prediction on a real European network — empirical support for the core premise of the graph-based approach, even using simpler models than full GNNs. Useful as a "does the network signal actually help" sanity-check reference before committing to full GNN architecture complexity.

7. **F. Corman, P. Kecman**, "Stochastic Prediction of Train Delays in Real-Time Using Bayesian Networks," *Transportation Research Part C: Emerging Technologies*, vol. 95, pp. 599–615, 2018.
   Bayesian-network (a different graphical-model family, not a GNN) approach to real-time delay prediction — useful as a lighter-weight graphical alternative if full GNN training data/compute isn't available, and directly informs the uncertainty-propagation logic across a network structure.

## Bibliography Entries Found via RSTGCN's Own Reference List

8. **J. Li, X. Xu, X. Ding, J. Liu, B. Ran**, "Bayesian Spatio-Temporal Graph Convolutional Network for Railway Train Delay Prediction," *IEEE Transactions on Intelligent Transportation Systems*, 2024.
   Combines Bayesian uncertainty estimation directly into a spatio-temporal GCN — a strong candidate architecture reference for this project's uncertainty-band requirement within a graph model (rather than bolting on separate quantile-regression models as in the non-graph approach).

9. **E. Jose, P. Agarwal, J. Zhuang, J. Swaminathan**, "A Multi-Criteria Decision Making Approach to Evaluating the Performance of Indian Railway Zones," *Annals of Operations Research*, vol. 325, no. 2, pp. 1133–1168, 2023.
   Not a GNN paper, but relevant for how to define zone/region boundaries within the graph (i.e., how to partition the national network into sub-graphs matching operational reality) if a full-network graph proves too large to train jointly.

10. **R. Pradhan, A. Kumar, M. Kumar, B. Sharma**, "Simulating and Analysing Delay in Indian Railways," *IOP Conference Series: Materials Science and Engineering*, vol. 1116, no. 1, 2021, p. 012127.
    (Also cited in the non-graph reference set.) Provides baseline understanding of Indian-network delay propagation patterns useful for validating whether a trained graph model's learned propagation behavior matches known operational reality.
