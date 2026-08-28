# Approach Summary

**Core idea:** model the rail network as a graph — stations as nodes, sections as edges — and use a spatio-temporal graph neural network (GCN/GAT + a temporal module such as GRU/LSTM or temporal attention) to predict per-section delay-change (Δ). Unlike a per-train chained model, the graph model's Δ prediction for one train's next section is informed by the current state of neighboring stations and other trains sharing nearby infrastructure, learned through message-passing rather than hand-built proxy features.

**Why this over the simpler chained GBT model:** delay propagation in dense networks is inherently a multi-train, multi-station phenomenon — a congested junction affects every train passing through it, not just the one train whose features happen to include "preceding train's delay." Graph models capture this structurally. The tradeoff is more data and engineering complexity, so this is positioned as the natural extension once the simpler per-train model is working and data volume supports it — see `04_comparison_with_chained_model.md`.

**Grounding:** the closest direct precedent is a 2025 paper (RSTGCN) that built a nationwide temporal delay dataset for the Indian Railway network specifically and found delay propagation strongest in dense, high-traffic zones — see `01_graph_neural_network_papers.md`.
