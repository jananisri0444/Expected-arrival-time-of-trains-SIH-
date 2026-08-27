# Glossary & Key Concepts

Short definitions of terms used throughout the project plan and model logic, with the source that grounds each concept.

- **ETA (Expected/Estimated Time of Arrival):** predicted arrival time at a station, as opposed to the scheduled (timetabled) arrival time.

- **Delay propagation:** the phenomenon where a delay incurred at one point in a train's journey (or by a preceding train sharing the same track section) carries forward and affects arrival times at subsequent stations. Central to this project's chained, leg-by-leg prediction logic. See `01_research_papers.md` #1, #6, #8, #14.

- **Recovery time / running time supplement:** slack time built into the official schedule beyond the minimum technically required running time, allowing a delayed train to "recover" lost minutes over a section. Indian Railways' current static ETA approach relies on this margin, which is exactly what this project aims to replace with a dynamic, learned estimate. See `01_research_papers.md` #22 (Modeling Train Delays: A Study of Indian Railways).

- **Section / leg:** the stretch of track between two consecutive stops of a train; the base unit this project's model predicts delay-change over.

- **Quantile regression:** a regression technique that predicts a range (e.g., 10th–90th percentile) rather than a single point estimate, used here to produce the ETA uncertainty band. See `01_research_papers.md` #13 (Corman & Kecman, Bayesian real-time delay prediction).

- **Spatio-temporal graph model:** a model architecture (e.g., graph convolutional or graph attention networks) that represents the rail network as a graph (stations/sections as nodes/edges) and learns how delay spreads across it over time — the "Phase 2 / stretch goal" architecture referenced as a future extension beyond this project's MVP gradient-boosted-trees model. See `01_research_papers.md` #6, #8, #14, #16.

- **NTES (National Train Enquiry System):** Indian Railways' official real-time train-status platform, and this project's primary live-data source. See `02_data_sources.md`.

- **TMS (Train Management System):** Indian Railways' internal, non-public system handling signal-level and interlocking data — the data source this project explicitly cannot access, and the reason congestion/speed-restriction effects are modeled as proxies rather than direct features.
