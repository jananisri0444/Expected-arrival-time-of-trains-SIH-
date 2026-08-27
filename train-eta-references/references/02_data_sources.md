# Data Sources — Verified Public / Free Access Points

These are the concrete sources this project's data-collection pipeline is built on. See `PROJECT_SUMMARY.md` and the main project plan document for the feasibility reasoning behind excluding non-public data (signal aspects, speed restrictions, TMS internals).

## Live / Real-Time Train Running Status

- **National Train Enquiry System (NTES)** — official Indian Railways real-time train running status, schedules, and enquiry platform, operated by CRIS (Centre for Railway Information Systems).
  https://enquiry.indianrail.gov.in/ntes/
  - Wikipedia overview (agency background, scope of services): https://en.wikipedia.org/wiki/National_Train_Enquiry_System
  - Community documentation of usable underlying JSON endpoints (train search by number, station-on-map data): https://groups.google.com/g/datameet/c/imBhXjArgRA/m/b_ZLaN-OCgAJ

- **Third-party wrapper APIs built on Indian Railways data** (freemium/registration-based — useful as a fallback or for cross-checking NTES scraping):
  - `api-railway-api` (npm package wrapping indianrailapi.com): https://github.com/rachitgupta98/api-railway-api
  - "Train Running Status Indian Railways" API on RapidAPI: https://rapidapi.com/shivesh96/api/train-running-status-indian-railways

## Static Reference Data (schedules, stations, routes)

- **Open Government Data (OGD) Platform India — Railways sector**: catalog of datasets, APIs, and services shared by Indian Railways-related ministries/departments.
  https://www.data.gov.in/sector/railways
  https://www.data.gov.in/keywords/indian-railways

- **`datameet/railways` (GitHub)** — community-collected Indian Railways dataset: GeoJSON station master (code, name, coordinates, state, zone, address) and train route line geometries (with class availability flags: sleeper, AC tiers, chair car, etc.).
  https://github.com/datameet/railways

- **"Indian Railways Dataset" (Kaggle)** — schedule-level dataset (train number, name, station code, arrival/departure time, day-of-journey) collected by community contributors.
  https://www.kaggle.com/datasets/sripaadsrinivasan/indian-railways-dataset

## Weather Data

- Free-tier weather APIs (OpenWeatherMap, Visual Crossing, or equivalent) queried by station lat/long for current conditions and short-range forecasts — used for the fog/visibility and rainfall-intensity features described in the model logic. (Pick one based on free-tier rate limits at implementation time; not pinned here since offerings/pricing change.)
- India Meteorological Department (IMD) public data/API access, for authoritative India-specific weather and visibility bulletins where available.

## Track / Geographic Data

- **OpenStreetMap** — rail layer geometry, usable for section distance computation and map-based visualization in the dashboard.
  https://www.openstreetmap.org

## What's explicitly NOT available (and why it's out of scope for the MVP)

| Data type | Status |
|---|---|
| Signal aspect / interlocking data | Internal to IR's Train Management System (TMS); not public |
| Temporary speed restrictions (TSR) bulletins | Distributed internally to loco pilots/control offices; not a public feed |
| Track occupancy / block section status | Internal signaling data; not public |
| Maintenance block schedules | Published in limited, non-machine-readable form (if at all) to the public |
| Historical delay dataset (ready-made, large-scale) | Does not exist publicly at scale — must be self-collected by polling NTES over the project timeline (see `01_research_papers.md` #5 for a precedent of doing exactly this at small scale) |

These gaps are the reason the project's "Phase 2 / production path" explicitly requires a data-sharing arrangement with Indian Railways / CRIS rather than assuming they can be scraped.
