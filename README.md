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
including the two matches between the teams.

The dataset covers the regular season, the Playoff Pool, the Promotion Playoffs, and the Coppa Italia.

Overall, it contains:
- **69,943 logged actions** across all volleyball skills (serve, reception, set, attack, block, dig, and freeball);
- **16,301 attack actions**, each matched to a valid attack zone and attack tempo using the corresponding `[3ATTACKCOMBINATION]` table.

The original `.dvw` files were produced by the teams' coaching staff and are **not publicly available**. They are included in this repository only for the exam purpose.

The files `matches.csv` and `actions.csv` are generated directly from the raw `.dvw` files during the parsing step. They are included so that the parsed data can be inspected without running the notebook.

## Repository structure

```text
.
├── README.md
├── project_proposal1.pdf          Deliverable 1 – Project Proposal
├── technical_report2.pdf        Deliverable 2 – Dataset Description & Exploratory Analysis
├── notebook.pdf                 Deliverable 3 – Notebook (PDF export)
├── notebook.ipynb               Deliverable 3 – Runnable notebook
├── geography_of_the_attack.html Deliverable 3 – Standalone Bokeh application
├── development_report.pdf       Deliverable 4 – Development Report
├── figures/                     Figures used in the Technical Report
└── dataset/
    ├── matches.csv              One row per match
    ├── actions.csv              One row per logged action
    ├── *.dvw                    Raw DataVolley scouting files (matches of Brescia)
    ├── *.dvw                    Raw DataVolley scouting files (matches of Talmassons)
    └── *.dvw                    Raw DataVolley scouting files (all the matches)
```

## Method

- The raw `.dvw` files are parsed with [`pydatavolley`](https://github.com/openvolley/pydatavolley).
- Attack tempo is recovered by reading the match-specific `[3ATTACKCOMBINATION]` table, since it is not provided as a structured field by the library.
- Derived variables were checked before the analysis. Attack zones obtained from `pydatavolley` (`start_zone`) matched the attack-combination table for every focal-team attack. The `num_blockers` field was also verified: values from 0 to 3 represent the number of opposing blockers, while the additional value corresponds to the DataVolley *Hole block* category rather than to a literal blocker count.
- The figures in the Technical Report were created with Matplotlib and Seaborn. The interactive application was developed with Bokeh using `CDSView`, `GroupFilter`, `factor_cmap`, and linked interactive tools.

## Deliverables

| # | File | Description |
|---|------|-------------|
| 1 | `project_proposal1.pdf` | Project proposal, objectives, hypotheses, and planned visualizations |
| 2 | `technical_report2.pdf` | Dataset description, exploratory analysis, and data-quality assessment |
| 3 | `notebook.ipynb` / `notebook.pdf` / `geography_of_the_attack.html` | Complete parsing pipeline, exploratory analysis, and interactive Bokeh application |
| 4 | `development_report.pdf` | Project development, changes from the proposal, and reflections |

## Requirements

Python 3 with:
- `pydatavolley`
- `pandas`
- `numpy`
- `matplotlib`
- `seaborn`
- `bokeh`

See `notebook.ipynb` for the complete installation and execution steps.
The file `geography_of_the_attack.html` is self-contained and can be opened directly in any web browser.
