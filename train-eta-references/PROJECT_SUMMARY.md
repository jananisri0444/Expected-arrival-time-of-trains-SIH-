# Project Summary

**Goal:** Replace static schedule + current-delay + fixed recovery-time ETA estimation on Indian Railways coaching trains with a dynamic, data-driven prediction system that updates continuously using live running data, historical delay patterns, weather, and network/congestion signals.

**Core modeling approach:** section-wise delay-propagation regression (predict the change in delay over the *next* leg of the journey, chain forward station-by-station) using gradient-boosted trees (LightGBM/XGBoost) as the primary model, benchmarked against a naive persistence baseline (`scheduled_time + current_delay`).

**Data constraint driving the whole design:** Indian Railways does not publicly expose signal-level TMS, sectional occupancy, or speed-restriction data. The system is scoped around what's genuinely obtainable — NTES live running status, static schedule/station datasets, and weather APIs — with congestion modeled as a derived proxy (preceding-train delay) rather than a direct feed.

See `references/02_data_sources.md` for the full data feasibility list and `references/01_research_papers.md` for the modeling literature this design draws on.
