# Research Papers — Train Delay & ETA Prediction

Organized roughly from most India-specific / most directly relevant, to general international literature on the same problem. Notes describe what each paper contributes to this project's design, in our own words (not quoted from the papers).

---

## Indian Railways–specific

1. **R. Pradhan, A. Kumar, M. Kumar, B. Sharma**, "Simulating and Analysing Delay in Indian Railways," *IOP Conference Series: Materials Science and Engineering*, vol. 1116, no. 1, 2021, p. 012127.
   Relevant for: baseline understanding of how delay accumulates and propagates across the Indian rail network — informs the "delay propagation" framing used in this project's chained-prediction logic.

2. **M. Arshad, M. Ahmed**, "Prediction of Train Delay in Indian Railways through Machine Learning Techniques," *International Journal of Computer Science and Engineering*, 7:405–411, 2019.
   Relevant for: one of the earliest India-focused ML delay-prediction studies; useful as a baseline comparison point for classical ML approaches (KNN, decision trees, logistic regression, random forest) on Indian data.

3. **M. Arshad, M. Ahmed**, "Train Delay Estimation in Indian Railways by Including Weather Factors Through Machine Learning Techniques," *Recent Advances in Computer Science and Communications*, 14(4):1300–1307, 2021.
   Relevant for: directly supports including weather (a data source this project also uses) as a delay-prediction feature; compares linear regression, gradient boosting, decision tree, and random forest on combined delay + weather data.

4. **R.C. Sharma, I. Hossain, A. Kumar**, "Improving On-Time Performance: Predicting Train Delays with Machine Learning Techniques," in *Proc. [Conference]*, Springer, 2024.
   Relevant for: recent (2024) Indian-context study using a Random Forest Classifier for delay prediction; useful as an up-to-date benchmark.

5. **[Anonymized/2025] Study on Modeling Train Delays: A Study of Indian Railways**, *Applied Energy / ScienceDirect*, 2025.
   Collected delay data at destination for 20 trains across different Indian Railways zones over a multi-month period. Relevant for: validates that even small-sample, self-collected delay datasets (similar in spirit to this project's own NTES-polling approach) are a viable basis for delay-pattern modeling in the Indian context.

6. **[2025] "RSTGCN: Railway-centric Spatio-Temporal Graph Convolutional Network for Train Delay Prediction,"** arXiv:2510.01262, 2025.
   Builds a nationwide temporal railway delay dataset for the Indian Railway network and reports that delay propagation is especially significant in dense, high-traffic zones. Relevant for: supports this project's MVP decision to scope to a single busy corridor/zone first (where delay propagation signal is strongest and most learnable), and supports including "preceding train delay" / train-frequency features as this project's congestion proxy.

---

## General / International Train Delay & ETA Prediction Literature

7. **[2023]** "A Novel Deep Learning Model for Short-Term Train Delay Prediction," *ScienceDirect*, 2023. Integrates wavelet transform, a fully connected neural network, and LSTM; benchmarked against random forest, GBRT, XGBoost, and SVR on real high-speed rail data from China.
   Relevant for: confirms gradient-boosted trees (this project's primary model choice) are a standard, competitive baseline against more complex deep-learning approaches — supporting the project's staged approach (start with GBTs, treat sequence models as a stretch goal).

8. **D. Zhang et al.**, "Train Delay Prediction Using Machine Learning" (introducing TSTGCN — Train Spatio-Temporal Graph Convolutional Network), *IEEE Trans. Intelligent Transportation Systems*, 23:2434–2444, 2021.
   Relevant for: the "spatial + temporal" framing (delay depends on both distance/spacing between trains and time) directly informs this project's leg-chaining logic and preceding-train feature.

9. **[2022]** "Real-Time Passenger Train Delay Prediction Using Machine Learning: A Case Study With Amtrak Passenger Train Routes," *IEEE Xplore*, 2022. Compares Random Forest, Gradient Boosting Machine, and Multi-Layer Perceptron, using both real-time-only and real-time-plus-historical feature structures.
   Relevant for: directly supports this project's feature design of combining live state (current delay/position) with historical/statistical features — the paper found the combined (real-time + historical) approach outperformed real-time-only.

10. **[2022]** "Predicting Trains Delays using a Two-level Machine Learning Approach," *ICAART 2022 Proceedings*, SciTePress. Proposes a two-level LightGBM approach (classify delay bucket, then regress exact minutes) on Tunisian railway data.
    Relevant for: an alternative to this project's direct-regression approach — useful as a documented alternative modeling strategy (classify-then-regress) if straight regression underperforms.

11. **[2024]** "DelayPTC-LLM: Metro Passenger Travel Choice Prediction under Train Delays with Large Language Models," arXiv:2410.00052, 2024.
    Relevant for: downstream/adjacent use case (how predicted delays affect passenger behavior) — useful context for the "passenger communication" goal in the original problem statement, though outside this project's core ETA-model scope.

12. **[2024]** "Prediction of Rail Transit Delays with Machine Learning: How to Exploit Open Data Sources," *ScienceDirect*, 2024.
    Directly relevant: focuses specifically on building delay-prediction models from *open/public* data sources (including GTFS-style feeds), which mirrors this project's core constraint of working only with publicly available Indian Railways data rather than internal TMS feeds.

13. **F. Corman, P. Kecman**, "Stochastic Prediction of Train Delays in Real-Time Using Bayesian Networks," *Transportation Research Part C: Emerging Technologies*, vol. 95, pp. 599–615, 2018.
    Relevant for: foundational real-time delay-prediction methodology; supports the uncertainty-band approach in this project's inference logic (quantile predictions rather than point estimates only).

14. **P. Huang, J. Guo, S. Liu, F. Corman**, "Explainable Train Delay Propagation: A Graph Attention Network Approach," *Transportation Research Part E: Logistics and Transportation Review*, vol. 184, p. 103457, 2024.
    Relevant for: graph-based framing of delay propagation across a rail network; a natural "Phase 2" extension beyond this project's simpler leg-chaining MVP if a network-wide (not just per-train) model is pursued later.

15. **R. Gaurav, B. Srivastava**, "Estimating Train Delays in a Large Rail Network Using a Zero-Shot Markov Model," *2018 21st IEEE Intl. Conf. on Intelligent Transportation Systems (ITSC)*, 2018.
    Relevant for: an alternative lightweight statistical (Markov-chain) approach to delay propagation — a useful non-ML baseline/comparison method beyond the naive persistence baseline.

16. **J.S. Heglund, P. Taleongpong, S. Hu, H.T. Tran**, "Railway Delay Prediction with Spatial-Temporal Graph Convolutional Networks," *2020 IEEE 23rd Intl. Conf. on Intelligent Transportation Systems*, 2020.
    Relevant for: further supports the spatio-temporal graph modeling direction as a stretch-goal architecture beyond gradient-boosted trees.

17. **"Predicting Delayed Trajectories Using Network Features: A Study on the Dutch Railway Network,"** arXiv:2507.11776, 2025.
    Relevant for: European (Dutch) case study validating that network-level features (not just single-train history) meaningfully improve delay prediction — supports this project's inclusion of "count of trains scheduled through this section" as a network feature.

---

## How these map to this project's model logic

| Project design choice | Supported by |
|---|---|
| Gradient-boosted trees (LightGBM/XGBoost) as primary model | #7, #9, #10 |
| Chained, section-wise delay-propagation prediction | #6, #8, #15 |
| Preceding-train-delay as congestion proxy | #6, #8, #17 |
| Weather as a feature | #3 |
| Quantile/uncertainty-band output | #13 |
| Scoping MVP to one busy corridor/zone first | #6 |
| Building on open/public data only (project's core constraint) | #12 |
