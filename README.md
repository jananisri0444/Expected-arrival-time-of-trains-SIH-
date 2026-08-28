# References & Research — Graph-Based ETA Prediction for Indian Railways Coaching Trains

Companion repository to `train-eta-references/`, focused specifically on the **graph-based (GNN / spatio-temporal graph) approach** to delay/ETA prediction, where the rail network is modeled as a graph (stations as nodes, sections as edges) rather than each train being predicted in isolation.

## Structure

```
train-eta-graph-based/
├── README.md                                    ← you are here
├── APPROACH_SUMMARY.md                          ← one-paragraph summary of the graph-based design
└── references/
    ├── 01_graph_neural_network_papers.md        ← GCN/GAT/spatio-temporal GNN papers for railway delay
    ├── 02_graph_construction_and_data.md        ← how to build the graph from the same public data sources
    ├── 03_tools_and_libraries.md                ← GNN-specific libraries (PyG, DGL, etc.)
    └── 04_comparison_with_chained_model.md       ← when/why to use graph vs. per-train chained model
```

## Relationship to the other repo

This repo assumes the same public data sources documented in `train-eta-references/references/02_data_sources.md` (NTES, data.gov.in, `datameet/railways`, weather APIs) — the graph-based approach is a different **model architecture** over the same data, not a different data-collection pipeline. Read that file first if starting from scratch.

## Suggested citation format

```
[Author(s)], "[Title]," [Venue/Journal, Year]. Available: [URL]
```
