# The Geography of the Attack

An analysis of attacking performance in the Italian Women's Serie A2 using DataVolley scouting data from Brescia and Talmassons, the two teams promoted to Serie A1 during the 2025/26 season.

**Data Visualization Lab project**  
Francesca Michieletto (ID: 255371)

## Project overview

This project investigates how attacking performance changes according to three characteristics of an attack:
- attack zone;
- attack tempo;
- number of opposing blockers.

The analysis compares **Valsabbina Millennium Brescia** and **Talmassons**, the two teams promoted from the Italian Women's Serie A2 in the 2025/26 season. Talmassons achieved direct promotion, while Brescia reached Serie A1 through the playoffs. Since the two teams finished the regular season only one point apart, they provide a useful comparison.

## Dataset

The analysis is based on **63 DataVolley scouting files** (`.dvw`):
- 36 matches played by Brescia
- 29 matches played by Talmassons

including the two matches between the teams (36 + 29 = 65 team-match records across 63 distinct matches).

The dataset covers the regular season, the Playoff Pool, the Promotion Playoffs, and the Coppa Italia.

Overall, it contains:
- **69,943 logged actions** across all volleyball skills (serve, reception, set, attack, block, dig, and freeball)
- **16,301 attack actions** by all teams appearing in those matches, each matched to a valid attack zone and attack tempo using the corresponding `[3ATTACKCOMBINATION]` table
- of these, **8,312 attacks were played by Brescia or Talmassons** and form the basis of the zone, tempo, and blocker analyses

The original `.dvw` files were produced by the teams' coaching staff and are **not publicly available**. They are included here only for the purposes of this exam, in a private repository.

The files `matches.csv` and `actions.csv` are generated directly from the raw `.dvw` files during the parsing step. They are included so that the parsed data can be inspected without running the notebook.

## Repository structure

```text
.
├── README.md
├── project_proposal1.pdf           Deliverable 1 – Project Proposal
├── technical_report2.pdf           Deliverable 2 – Dataset Description & Exploratory Analysis
├── geography_of_the_attack3.ipynb  Deliverable 3 – Runnable notebook
├── geography_of_the_attack.html    Deliverable 3 – Bokeh application
├── development_report4.pdf         Deliverable 4 – Development Report
├── figures/                        Figures used in the Technical Report
└── dataset/
    ├── matches.csv                 One row per match (63 rows)
    ├── actions.csv                 One row per logged action (69,943 rows)
    ├── brescia/                    Raw scouting files, Brescia matches (36 files)
    ├── talmassons/                 Raw scouting files, Talmassons matches (29 files)
    └── all/                        Raw scouting files, all matches (63 files)
```

The two head-to-head matches appear in both `brescia/` and `talmassons/`, `all/` holds one copy of each of the 63 files and is the folder read by the notebook.

## Method

- The raw `.dvw` files are parsed with [`pydatavolley`](https://github.com/openvolley/pydatavolley).
- Attack tempo is recovered by reading the match-specific `[3ATTACKCOMBINATION]` table, since it is not provided as a structured field by the library.
- Derived variables were checked before the analysis. Attack zones obtained from `pydatavolley` (`start_zone`) matched the attack-combination table for all 8,312 focal-team attacks, confirming that the action codes were being read at the correct character positions. The `num_blockers` field was also verified: values from 0 to 3 represent the number of opposing blockers, while the additional value corresponds to the DataVolley *Hole block* category rather than to a literal blocker count.
- The figures in the Technical Report were created with Matplotlib and Seaborn. The interactive application was developed with Bokeh using `CDSView`, `GroupFilter`, `factor_cmap`, and linked interactive tools.

## Deliverables

| # | File | Description |
|---|------|-------------|
| 1 | `project_proposal1.pdf` | Project proposal, objectives, hypotheses, and planned visualizations |
| 2 | `technical_report2.pdf` | Dataset description, exploratory analysis, and data-quality assessment |
| 3 | `geography_of_the_attack3.ipynb` / `geography_of_the_attack3.html` | Complete parsing pipeline, exploratory analysis, and interactive Bokeh application |
| 4 | `development_report4.pdf` | Project development, changes from the proposal, and reflections |

## Running the project

**Interactive application.** Open `geography_of_the_attack3.html` in any web browser. No installation is required, but an **internet connection is needed**, because the page loads the Bokeh JavaScript library (3.8.2) from `cdn.bokeh.org`.

**Notebook.** `geography_of_the_attack3.ipynb` was written for Google Colab and mounts Google Drive to reach the `.dvw` files. 

Requirements: Python 3 with `pydatavolley`, `pandas`, `numpy`, `matplotlib`, `seaborn`, and `bokeh`. The installation commands are included in the notebook.
