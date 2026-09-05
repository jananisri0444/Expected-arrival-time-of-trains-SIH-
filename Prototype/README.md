# MAS–SBC Corridor Suite — README

A single-file, self-contained prototype for the Chennai Central (MAS) ⇄ KSR Bengaluru City (SBC) rail corridor. It models 84 stations and 83 track sections from real timetable, distance, and platform/loop-line data, and uses a hand-tuned delay-propagation rule (documented in the app itself) to simulate how a delay at one point spreads across the network.

Open `mas-sbc-corridor-suite.html` in any modern browser — no server, build step, or install required. It loads Leaflet (maps) and Chart.js (charts) from a CDN, so an internet connection is needed the first time it renders.

---

## Getting oriented

The page has two fixed pieces at the top and six tabs below them:

- **Header bar** — corridor name and a strip of live corridor-wide stats.
- **Tab bar** — switches between the six modules described below.
- **Scenario bar** — appears under the tab bar on every tab *except* Section Simulator. It holds the shared simulated clock and the list of injected congestion events that the other five tabs all read from.

### The scenario bar (shared state)

This is the control center for everything except Tab 1:

| Control | What it does |
|---|---|
| **Clock face** | Shows the current simulated time of day (24-hour). |
| **▶ / ⏸ button** | Auto-advances the clock so you can watch the corridor evolve without dragging the slider. |
| **Time slider** | Manually jump to any minute of the day (00:00–23:59). |
| **Speed selector** | 1×, 4×, 12×, or 30× — how fast the clock runs when playing. |
| **Inject congestion** | Pick a station, set a delay in minutes (1–90), click **Add**. This creates a disruption event at that station which then propagates outward to every train scheduled through it. |
| **Chips row** | Shows every active disruption as a removable chip (✕ to delete it). |

The app seeds one example disruption on load so tabs 2–6 aren't empty on first view — remove it or add your own to build a different scenario.

**Tip:** everything downstream (departure board, tracker, overview, congestion view, section drilldown) is computed live from the current clock position + the active disruption list. Move the clock or add/remove a disruption and every open tab updates.

---

## Module 1 — Section Simulator

The original single-train "what-if" tool. This tab does **not** use the scenario bar; it has its own self-contained controls in the left panel.

**How to use it:**
1. **Train on line** — choose any scheduled train on the corridor.
2. **Position report** — pick the station where you're observing a delay.
3. **Observed delay (minutes)** — drag the slider to set how late the train is at that station.
4. **Model shared-section congestion** toggle — when on, a second train is factored in; a disruption on a section they both pass through will bleed a portion of the delay onto it too.
5. **Nearby train sharing the section** — auto-picked (most overlapping stops with your primary train) but overridable.
6. Click **Run graph forward pass →** to propagate the delay down the rest of the route. **Reset to schedule** clears back to the original timetable.

**Reading the output:**
- The map plots the corridor and colour-codes each upcoming station by predicted severity (green/amber/red).
- The chart shows predicted delay by station with a shaded uncertainty band.
- The table lists every remaining station with scheduled arrival, predicted arrival, Δ delay, and ± uncertainty.
- Expand **"How this prototype works"** in the sidebar for the exact propagation rules (delay chaining, congestion bump, uncertainty growth, cross-train coupling).

---

## Module 2 — Departure Board

A "yellow board on the platform" view, driven by the scenario bar's clock and disruption list.

**How to use it:**
- Pick a **Station** and a **Direction** (both / MAS→SBC / SBC→MAS).
- The table lists every train due at that station — scheduled time, predicted time, train name, direction, and live status — updating automatically as you move the simulated clock or add/remove disruptions.

---

## Module 3 — Train Tracker

A passenger-style "where's my train" view.

**How to use it:**
- Pick a **Train** from the dropdown.
- The hero panel shows its next stop, big ETA, time-to-arrival, and a status badge (on time / moderate / severe).
- Below it, a full stop-by-stop table shows scheduled vs. predicted time and delay at every station on its route, with the upcoming stop highlighted.

---

## Module 4 — Corridor Overview

A bird's-eye dashboard of every train on the line at once.

**How to use it:**
- No controls needed — just watch. The stat row summarises how many trains are on time, moderately delayed, severely delayed, and how many disruptions are active.
- The map colour-codes every station by the worst nearby delay (within a 60-minute window of the simulated clock).
- The card grid below lists every train with its current predicted delay, colour-coded to match.
- Move the clock or add a disruption in the scenario bar to watch the whole corridor shift in real time.

---

## Module 5 — Station Congestion

Flips the question around: instead of "where's this train," it asks "what's converging on this station."

**How to use it:**
- Pick a **Station** and a **Look-ahead window** (1 / 3 / 6 / 12 hours from the simulated clock).
- The stat row shows how many trains are converging, their average predicted delay, and how many are severely delayed.
- The table lists each of those trains with ETA, direction, and delay — useful for spotting platform/junction bottlenecks building up.

---

## Module 6 — Section Drilldown

Zooms into a single stretch of track between two consecutive stations.

**How to use it:**
- Pick a **Section** from the dropdown (listed as *Station A → Station B*).
- The stat row shows the section's length, scheduled trains/day (density), and median running time.
- Below it, any train currently modelled as being on that section (based on the simulated clock) is listed with its direction, departure time, ETA at the next stop, and whether it lost or recovered time crossing the section.
- If nothing is on the section right now, try moving the clock or picking a busier section — the app will tell you this directly.

---

## Quick workflow suggestions

- **Explore a single "what-if":** stay on Tab 1, pick a train and station, drag the delay slider, run it.
- **Watch a disruption spread across the whole corridor:** go to any tab 2–6, add a congestion event in the scenario bar, then press ▶ and watch the clock advance.
- **Find a bottleneck station:** use Tab 5 (Station Congestion) with a wide look-ahead window on a station you suspect is busy (e.g. a junction).
- **Check if a specific section is a chokepoint:** use Tab 6 (Section Drilldown) and compare density/running time against how many trains are losing time there.

---

## Notes

- All data (stations, distances, platform counts, loop lines, timetables) comes from the corridor's real datasets; there's no live/actual delay feed behind it — predicted delays are generated by the propagation rule described in Tab 1, not a trained model (see the in-app "How this prototype works" panel for why, and what the next step would be).
- Requires internet access on first load (Leaflet, Chart.js, and OpenStreetMap tiles are fetched from CDNs).
- Everything runs client-side in the browser — no data is sent anywhere, and nothing is saved between page reloads.
