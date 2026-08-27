# Prior Systems & Case Studies

Real-world precedents for dynamic, ML-driven train delay/ETA prediction — useful for the report's "existing approaches" / competitive-landscape section.

- **Amtrak (USA)** — real-time passenger train delay prediction studied using Random Forest, Gradient Boosting Machine, and Multi-Layer Perceptron models, comparing real-time-only vs. real-time-plus-historical feature structures. See reference #9 in `01_research_papers.md`.

- **Chinese high-speed rail** — short-term delay prediction studied using a hybrid wavelet-transform + LSTM deep learning model, benchmarked against random forest, GBRT, XGBoost, and SVR on real operational data from two distinct high-speed lines. See reference #7 in `01_research_papers.md`.

- **Dutch railway network (Netherlands)** — delay-trajectory prediction using network-level features (not just single-train history), demonstrating that incorporating neighboring-train and section-level network features improves prediction over single-train models. See reference #17 in `01_research_papers.md`.

- **Tunisian railway (SNCFT)** — two-level LightGBM approach (classify delay bucket, then regress exact delay in minutes) as an alternative modeling strategy to direct regression. See reference #10 in `01_research_papers.md`.

- **Shenzhen Metro (China)** — downstream use case: predicting how passengers change travel choices in response to predicted/announced delays, using large language models on delay logs plus fare-collection data. Relevant context for "passenger communication" goals beyond pure ETA prediction. See reference #11 in `01_research_papers.md`.

- **Indian Railways — nationwide delay dataset & graph-based model (RSTGCN, 2025)** — the most directly relevant prior work: builds a nationwide temporal delay dataset for the Indian Railway network and shows delay propagation is most significant in dense, high-traffic zones — directly informing this project's decision to scope its MVP to one busy corridor. See reference #6 in `01_research_papers.md`.

## Takeaway for this project

Across these case studies, the common pattern is: (1) gradient-boosted trees or random forest as a strong, practical baseline before reaching for deep learning, (2) combining real-time state with historical/statistical features consistently outperforms real-time-only, and (3) network/neighboring-train features add meaningful signal over single-train history alone — all of which directly shaped this project's model logic (see `PROJECT_SUMMARY.md`).
