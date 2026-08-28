# Graph Construction & Data Mapping

How the same public data sources (see `train-eta-references/references/02_data_sources.md`) map onto the graph structure needed for the GNN approach.

## Node Construction (Stations)

- **Source:** `datameet/railways` GeoJSON station master (code, name, lat/long, zone) + data.gov.in station datasets.
  https://github.com/datameet/railways
- **Node features per snapshot:** current aggregate delay of trains present/passing through, historical average dwell time, platform/junction complexity (approximated from number of distinct routes passing through, derivable from the schedule dataset), current weather (fog/visibility/rain) from weather API.

## Edge Construction (Sections)

- **Source:** consecutive-station pairs from the static schedule dataset (Kaggle "Indian Railways Dataset" or NTES `SearchTrain` schedule responses) define which stations are directly connected by a scheduled leg; distances from `datameet/railways` line geometries or OpenStreetMap rail layer.
- **Edge features per snapshot:** scheduled running time for the section, historical actual-vs-scheduled running time ratio (computed from accumulated NTES polling history — same self-collected historical dataset used in the non-graph approach), number of trains scheduled through the section in the current time window (computed directly from the static schedule).

## Temporal Snapshots (Dynamic Graph)

- Each NTES poll cycle (recommended every 5-10 minutes) produces a new snapshot: update the delay/position state of every node/edge currently carrying live traffic, leaving historical/static features unchanged between snapshots.
- Store snapshots in a time-indexed structure (e.g., a sequence of graph states in the same PostgreSQL/TimescaleDB structured layer used for the non-graph approach) so the temporal module (GRU/LSTM/temporal attention) has a window of recent snapshots to learn from.

## Practical Scoping Note

A full national-network graph (thousands of stations) is likely too large/sparse-data to train jointly within a project timeline. Recommended scoping: build the graph for one zone or one busy corridor first (same MVP scoping principle as the non-graph approach — see `train-eta-references/PROJECT_SUMMARY.md`), which also keeps the graph dense enough that message-passing has meaningful neighboring signal to learn from.
