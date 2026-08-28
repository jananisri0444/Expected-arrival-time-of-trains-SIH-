# Tools & Libraries — Graph Neural Network Implementation

## GNN Frameworks

- **PyTorch Geometric (PyG)** — most widely used library for implementing GCN, GAT, and custom message-passing layers on top of PyTorch.
  https://pytorch-geometric.readthedocs.io/

- **Deep Graph Library (DGL)** — alternative GNN framework, strong support for heterogeneous and dynamic/temporal graphs.
  https://www.dgl.ai/

- **PyTorch Geometric Temporal** — extension of PyG specifically for spatio-temporal graph models (combines graph convolution with recurrent/temporal layers) — closest match to the architecture needed here (temporal graph snapshots feeding a GCN/GAT + GRU pipeline).
  https://pytorch-geometric-temporal.readthedocs.io/

## Supporting Infrastructure (shared with non-graph approach)

- **PostgreSQL / TimescaleDB** — for storing time-indexed graph snapshots.
  https://www.postgresql.org/ · https://www.timescale.com/
- **Apache Airflow** — scheduling snapshot construction and periodic retraining.
  https://airflow.apache.org/
- **NetworkX** — useful for graph construction/validation/visualization during development before feeding structures into PyG/DGL.
  https://networkx.org/
- **FastAPI** — same API serving layer as the non-graph approach; the graph model simply replaces what's behind the endpoint.
  https://fastapi.tiangolo.com/
