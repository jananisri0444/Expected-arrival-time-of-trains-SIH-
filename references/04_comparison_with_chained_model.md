# Graph-Based vs. Chained Per-Train Model — When to Use Which

| Dimension | Chained GBT model (`train-eta-references/`) | Graph-based GNN model (this repo) |
|---|---|---|
| Unit of prediction | One train, one leg at a time, chained forward | Whole network snapshot; multiple trains/sections informed jointly |
| Congestion modeling | Proxy feature (preceding train's reported delay) | Learned structurally via message-passing between neighboring nodes/edges |
| Data volume needed | Works reasonably with a few weeks of polling on a single corridor | Needs denser, longer historical coverage to learn meaningful graph structure — best attempted after the chained model's data pipeline has been running longer |
| Implementation complexity | Lower — tabular ML, standard libraries (LightGBM/XGBoost) | Higher — graph construction, temporal snapshot management, GNN training loop |
| Interpretability | High — feature importances are directly readable | Lower by default, though GAT-style attention weights can partially recover "which neighbor mattered" interpretability (see reference #4 in `01_graph_neural_network_papers.md`) |
| Best fit | MVP / hackathon timeline, first working system, single busy corridor | Phase 2 extension once chained model is validated and more historical data has accumulated; strongest value in dense, high-traffic zones (per RSTGCN findings) |

## Recommended Path

1. Ship the chained GBT model first (see `train-eta-references/`) — it's the fastest path to a working, benchmarkable system with the data realistically available in a project timeline.
2. Once the polling pipeline has accumulated sufficient historical depth (weeks-to-months) and the MVP corridor is validated, evaluate whether a graph-based model measurably improves accuracy over the chained baseline **specifically in the dense/high-traffic sections** where RSTGCN found graph propagation matters most — this is the honest place to expect a graph model to earn its added complexity, rather than assuming it will help uniformly everywhere.
3. Report both models' MAE side by side in any final writeup — the chained model's number is your credible floor; the graph model's number (if pursued) is the stretch-goal ceiling.
