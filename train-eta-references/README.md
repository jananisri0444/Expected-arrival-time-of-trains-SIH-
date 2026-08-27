# References & Research — Real-Time ETA Prediction for Indian Railways Coaching Trains

This repository collects the research papers, public data sources, prior art/systems, and tools used as background for the **Real-Time ETA Prediction System for Indian Railways Coaching Trains** project (SIH-style problem statement: dynamic, ML-driven ETA prediction replacing static schedule + recovery-time estimates).

## Structure

```
train-eta-references/
├── README.md                              ← you are here
├── PROJECT_SUMMARY.md                     ← one-paragraph project context
└── references/
    ├── 01_research_papers.md              ← academic papers on train delay/ETA prediction
    ├── 02_data_sources.md                 ← public/free data sources actually usable for this project
    ├── 03_tools_and_libraries.md          ← ML/eng tools referenced in the model design
    ├── 04_prior_systems_case_studies.md   ← existing real-world systems (Amtrak, Dutch/Chinese rail, etc.)
    └── 05_glossary_and_concepts.md        ← key concepts (delay propagation, recovery time, etc.) with sources
```

## How to use this repo

- Each file in `references/` is a standalone, linkable reference list — cite these in your project report / PPT directly.
- `02_data_sources.md` is the most load-bearing file: it lists exactly what data was assessed as *actually* obtainable for this project (see the main project plan doc for the feasibility reasoning), as opposed to data that would be ideal but isn't public.
- Links were verified as of **August 2026**. Academic paywalled papers are linked via their publisher page; where a free/preprint version exists (e.g. arXiv), that link is included instead or in addition.

## Suggested citation format for the report

```
[Author(s)], "[Title]," [Venue/Journal, Year]. Available: [URL]
```

## License

Reference list compiled for educational/project use. Original papers and datasets remain under their respective publishers'/authors' licenses — check each source before redistribution.
