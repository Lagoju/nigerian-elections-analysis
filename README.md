# How Has Voting Behaviour in Nigeria Changed? (2015–2023)

A data analytics portfolio project exploring changes in voter participation, party competition, state-level voting patterns and electoral outcomes across Nigeria's 2015, 2019 and 2023 presidential elections.

> **Core question:** How has voting behaviour in Nigeria changed between the 2015, 2019 and 2023 presidential elections?

This project combines Python-based data preparation and analysis with an interactive Power BI report. It moves beyond national vote-share comparisons to examine participation, geographic variation, electoral volatility, the emergence of new political parties and a deeper look at available 2023 polling-unit records.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Project Objectives](#project-objectives)
- [Key Findings](#key-findings)
- [Tools and Technologies](#tools-and-technologies)
- [Data Sources and Scope](#data-sources-and-scope)
- [Analytical Approach](#analytical-approach)
- [Power BI Dashboard](#power-bi-dashboard)
- [Repository Structure](#repository-structure)
- [Running the Project](#running-the-project)
- [Important Definitions](#important-definitions)
- [Data Quality and Limitations](#data-quality-and-limitations)
- [Further Questions](#further-questions)

---

## Project Overview

Nigeria's presidential elections in 2015, 2019 and 2023 provide an opportunity to examine how voter participation and political competition have evolved over time.

A simple comparison of the national results would not fully capture these changes. The project therefore analyses election results at multiple levels:

- **National:** voter registration, accreditation, turnout, votes cast, party vote shares and winning margins.
- **State/FCT:** differences in party support, turnout, winning parties and changes between elections across Nigeria's 37 state/FCT units.
- **Geopolitical zones:** broader geographic patterns in participation and party support.
- **Polling units (2023):** party wins, distribution of available polling-unit records, comparison with official state-level winners and selected data-quality checks.
- **Statistical analysis:** electoral volatility, exploratory regression and K-means clustering.

The Python work contains more than 270 notebook cells, covering data inspection, harmonisation, validation, analysis and robustness checks. The resulting findings were presented in a multi-page Power BI report.

## Project Objectives

1. Compare voter registration and participation across the three presidential elections.
2. Examine how APC, PDP and other parties performed over time.
3. Identify state/FCT units with substantial changes in party support and winning parties.
4. Explore differences in voter participation and party support across geopolitical zones.
5. Measure election-to-election changes in party support using electoral volatility.
6. Examine the 2023 election beyond state-level totals using the available polling-unit records.
7. Explore state-level associations and group states with similar electoral changes.
8. Communicate the findings through an interactive Power BI report.

---

## Key Findings

The figures below summarise the main patterns identified in the analysis. Percentages and definitions should be interpreted in the context of the analytical datasets and comparability decisions described later in this README.

### 1. The electorate grew, but participation declined

| Indicator | 2015 | 2019 | 2023 |
|---|---:|---:|---:|
| Registered voters | 67.4 million | 82.3 million | 93.2 million |
| Accredited voters | 31.7 million | 29.4 million | 25.3 million |
| Turnout | 47.09% | 35.66% | 27.13% |

Between 2015 and 2023, the registered electorate increased by approximately **25.8 million**, while turnout declined from **47.09% to 27.13%**. This represents a relative decline of approximately **42.39%** in turnout.

The central participation finding is that a larger registered electorate did not translate into higher voter participation.

### 2. APC and PDP dominance weakened in 2023

For the longitudinal comparison, party support was harmonised into three categories: APC, PDP and Other.

| Indicator | 2015 | 2019 | 2023 |
|---|---:|---:|---:|
| APC vote share | 53.96% | 55.60% | 36.63% |
| PDP vote share | 44.96% | 41.22% | 29.06% |
| APC + PDP combined share | 98.92% | 96.82% | 65.69% |
| Comparable winning margin | 9.00 pp | 14.38 pp | 2.33 pp |

The combined APC and PDP share fell substantially in 2023. The comparable winning margin also narrowed to approximately **2.33 percentage points**.

**Note:** The longitudinal `Other` category includes all valid votes outside APC and PDP. It is not the same as the full-party `Other` category used in the 2023 breakdown.

### 3. New political forces became significant in 2023

The full-party national vote-share breakdown for 2023 was:

| Party | Vote share |
|---|---:|
| APC | 36.63% |
| PDP | 29.06% |
| Labour Party (LP) | 25.37% |
| NNPP | 6.23% |
| Other parties | 2.71% |

The Labour Party received approximately one-quarter of valid votes, while NNPP also secured a notable share. The 2023 result therefore showed a more diverse pattern of national party competition than the APC/PDP-dominated structure used for the earlier longitudinal comparison.

### 4. Many state/FCT units changed their winning party in 2023

| Election transition | State/FCT units changing winner |
|---|---:|
| 2015–2019 | 6 of 37 |
| 2019–2023 | 25 of 37 (67.6%) |

The number of state/FCT units changing their comparable winning party increased considerably between the two election periods. This indicates that the geographical distribution of party support changed substantially in 2023.

### 5. Winner-changing states recorded higher average volatility

For 2019–2023, average electoral volatility was:

| Winner-change group | Average volatility |
|---|---:|
| Changed winner | 48.80 |
| Same winner | 22.44 |

State/FCT units that changed their winning party had more than twice the average volatility of those that retained the same winner. This is a descriptive association; it does not establish that one pattern caused the other.

### 6. Polling-unit records revealed a different view of party performance

The final analytical polling-unit dataset contained **123,918 observations**.

| Polling-unit winner | Number of records |
|---|---:|
| APC | 50,797 |
| Labour Party | 40,052 |
| PDP | 26,849 |
| NNPP | 6,220 |

The polling-unit winner counts show APC first and Labour Party second in the available crosschecked records. These counts measure the number of records won, not the total number of votes received nationally.

The polling-unit winner in the analysed records agreed with the official state-level winner in **32 of 37** state/FCT units. The five differences were Katsina, Lagos, Nasarawa, Osun and Rivers.

### 7. Polling-unit data quality checks identified records for review

Of the 123,918 analytical polling-unit observations, **7,951 (approximately 6.4%)** were flagged because the combined votes recorded for APC, LP, PDP and NNPP exceeded accredited voters.

These are statistical/data-quality flags that warrant investigation. They are **not, by themselves, evidence of electoral fraud or manipulation**.

### 8. States followed different electoral trajectories

K-means clustering grouped the 37 state/FCT units into six clusters based on similarities in electoral change. The resulting groups showed different combinations of APC vote-share change, PDP vote-share change and change in the effective number of parties.

The clusters are descriptive groupings, not political labels, and do not imply that geographically separate states necessarily share the same causes of electoral change.

---

## Tools and Technologies

| Tool / Library | Use in the project |
|---|---|
| Python | Data preparation, analysis and statistical modelling |
| pandas | Data loading, cleaning, transformation and aggregation |
| NumPy | Numerical calculations |
| Matplotlib | Data visualisation during analysis |
| SciPy | Statistical testing |
| statsmodels | Regression analysis, diagnostics and robust standard errors |
| scikit-learn | Standardisation, K-means clustering and silhouette evaluation |
| Jupyter Notebook | Interactive analytical workflow |
| Power BI | Interactive report and data visualisation |

---

## Data Sources and Scope

### Election results

The project examines Nigeria's 2015, 2019 and 2023 presidential election results. INEC was the primary source strategy for official election information. The notebook uses harmonised election files named:

- `2015_harmonized.csv`
- `2019_harmonized.csv`
- `2023_harmonized.csv`

These files were inspected and prepared for longitudinal analysis. The repository should include the source files only where redistribution is permitted; otherwise, provide the relevant source links and instructions for obtaining them.

### 2023 polling-unit records

A separate 2023 polling-unit source archive contained records classified as:

- Crosschecked
- Unsure
- Not found

The 37 crosschecked CSV datasets were used to create the canonical analytical polling-unit dataset. The unsure and not-found records were retained for coverage and data-quality context rather than treated as equivalent voting observations.

### Geographic scope

The state-level longitudinal analysis covers **37 Nigerian state/FCT units**: the 36 states and the Federal Capital Territory.

### Important party-comparability decision

The party system and available party-level data were not structured identically across the three elections.

For longitudinal comparisons, the project uses:

- APC
- PDP
- Other

For the 2023 full-party analysis, it separately examines:

- APC
- PDP
- Labour Party (LP)
- NNPP
- Other parties

In the longitudinal structure, 2023 `Other` means all valid votes outside APC and PDP, including LP and NNPP. In the 2023 full-party breakdown, `Other` excludes LP and NNPP. These two definitions should not be mixed.

---

## Analytical Approach

The analysis was developed in stages.

### 1. Data inspection and standardisation

The three election datasets were inspected for dimensions, columns, sample records, state coverage and structural differences. Column names and state names were standardised, including consistent handling of the FCT label.

### 2. Geographic harmonisation

A consistent state-code lookup was created and applied across the election datasets. This supported reliable state-level matching and joins.

Output: `nigeria_state_code_lookup.csv`

### 3. Party harmonisation and validation

The party categories were aligned into APC, PDP and Other for longitudinal comparison, while 2023 LP and NNPP results were retained separately for the 2023 full-party analysis.

Electoral arithmetic checks included reconciling party totals against valid votes and checking for negative calculated Other values. Vote shares, winners, runners-up, winning margins and effective number of parties were then derived.

### 4. Longitudinal datasets

The state-election master dataset contains **111 observations**:

`37 state/FCT units × 3 elections = 111 state-election observations`

Each row represents one state/FCT unit in one presidential election.

Key outputs:

- `nigeria_presidential_results_master_2015_2019_2023.csv`
- `nigeria_presidential_results_analysis_2015_2019_2023.csv`

The analysis-ready dataset adds election-to-election changes, including party vote-share changes, turnout change, ENP change, margin change and winner switching.

### 5. National and state-level analysis

National percentages were calculated from national vote totals divided by national valid votes, rather than by taking a simple average of state percentages. This ensures that states contribute according to their vote totals when calculating national shares.

State-level analysis examined party support, turnout, winning parties, margins, effective number of parties and changes between elections.

### 6. Electoral volatility

Pedersen-style electoral volatility was calculated as:

\[
V = \frac{1}{2}\sum_{i=1}^{n}|p_{i,t}-p_{i,t-1}|
\]

where \(p_{i,t}\) is the vote share of party category \(i\) in the current election and \(p_{i,t-1}\) is its share in the previous election.

For the longitudinal volatility calculation, the comparable party categories are APC, PDP and Other. Volatility measures the scale of change in the distribution of party support; it does not explain why that change occurred.

Outputs include:

- `nigeria_electoral_volatility.csv`
- `nigeria_electoral_volatility_summary.csv`
- `nigeria_volatility_drivers.csv`

### 7. Geographic analysis

The 37 state/FCT units were assigned to Nigeria's six geopolitical zones:

- North Central
- North East
- North West
- South East
- South South
- South West

The analysis examined turnout, party support and geographic patterns across these zones. Where zone-level visuals use averages of state percentages, they should be interpreted as unweighted state averages rather than voter-weighted regional totals.

### 8. 2023 polling-unit deep dive

The polling-unit analysis used the fields available in the source records, including APC, LP, PDP and NNPP votes, registered voters, accredited voters and result/status indicators.

The four-party vote total was calculated as:

`APC votes + LP votes + PDP votes + NNPP votes`

The analysis derived party shares, polling-unit winners, winner margins, winner shares and selected participation/competitiveness indicators.

The source did not provide official valid votes, rejected votes or total votes cast at polling-unit level in the form needed for this analysis. Those measures were not fabricated.

### 9. Correlation and regression

The statistical analysis used the state-level election data to explore relationships between turnout, party vote shares, the effective number of parties and electoral margins.

Exploratory regression models examined 2019–2023 changes in APC and PDP vote shares. The APC model considered turnout change, ENP change and change in comparable winning margin as predictors.

The models were treated as exploratory because the state-level sample contains only 37 observations. Regression results are interpreted as associations, not causal effects.

### 10. Diagnostics and robustness checks

The regression work included checks for:

- Multicollinearity using VIF
- Residual normality
- Heteroskedasticity
- HC3 robust standard errors
- Influential observations and Cook's distance
- A leave-one-out robustness check

These checks were used to assess how sensitive the exploratory regression results were to model assumptions and influential observations.

### 11. K-means clustering

K-means clustering was used to group state/FCT units with similar electoral changes. The clustering variables were standardised before fitting the model so that variables measured on different scales would not dominate distance calculations.

Candidate cluster counts were evaluated using silhouette scores. The selected clustering was profiled and stability was checked across multiple random seeds.

The cluster profiles are descriptive summaries of the states assigned to each group.

---

## Power BI Dashboard

The Power BI report turns the analysis into an interactive, nine-page story.

**Dashboard overview**

<!-- Replace the image path below with the screenshot filename you add to powerbi/screenshots/. -->
![Power BI dashboard overview](powerbi/screenshots/dashboard-overview.png)

### Page 1 — Executive Summary

Presents the central findings: growth in registered voters, declining turnout, weakening APC/PDP dominance and increased electoral competition in 2023.

![Page 1 — Executive Summary](powerbi/screenshots/01-executive-summary.png)

### Page 2 — National Electoral Trends

Examines registered and accredited voters, valid and rejected votes, and rejected ballot rates across the three elections.

![Page 2 — National Electoral Trends](powerbi/screenshots/02-national-electoral-trends.png)

### Page 3 — State-Level Voting Behaviour

Highlights differences in state-level party support, changes in comparable winning margins and electoral volatility.

![Page 3 — State-Level Voting Behaviour](powerbi/screenshots/03-state-level-voting-behaviour.png)

### Page 4 — Geographic Patterns

Compares turnout and party support across Nigeria's six geopolitical zones and highlights state-level turnout patterns.

![Page 4 — Geographic Patterns](powerbi/screenshots/04-geographic-patterns.png)

### Page 5 — Electoral Volatility

Compares electoral volatility across election periods and examines how volatility differs between state/FCT units that changed their winning party and those that did not.

![Page 5 — Electoral Volatility](powerbi/screenshots/05-electoral-volatility.png)

### Page 6 — The 2023 Presidential Election

Shows the national 2023 party vote-share breakdown, the winning party by state/FCT unit and party support across states.

![Page 6 — The 2023 Presidential Election](powerbi/screenshots/06-2023-presidential-election.png)

### Page 7 — Polling-Unit Analysis

Explores polling-unit winners, the distribution of polling-unit records by state and records flagged by the selected data-quality check.

![Page 7 — Polling-Unit Analysis](powerbi/screenshots/07-polling-unit-analysis.png)

### Page 8 — Electoral Clusters

Presents the six groups of state/FCT units identified through K-means clustering and compares their average electoral-change profiles.

![Page 8 — Electoral Clusters](powerbi/screenshots/08-electoral-clusters.png)

### Page 9 — Methodology & Data Quality

Summarises the project workflow, polling-unit validation checks, coverage differences and key interpretation limitations.

![Page 9 — Methodology & Data Quality](powerbi/screenshots/09-methodology-data-quality.png)

> **Adding your screenshots:** Save each exported report-page image in `powerbi/screenshots/` using the filenames shown above. If you do not have a separate overview image, you can remove the overview image block.

---

## Repository Structure

The structure below is a suggested organisation for the GitHub repository. Adjust filenames to match the files you choose to publish.

```text
nigeria-presidential-election-analysis/
│
├── README.md
├── requirements.txt
│
├── data/
│   ├── raw/
│   │   └── README.md
│   ├── processed/
│   │   └── README.md
│   └── README.md
│
├── notebooks/
│   └── Master.ipynb
│
├── powerbi/
│   ├── nigeria_election_analysis.pbix
│   └── screenshots/
│       ├── dashboard-overview.png
│       ├── 01-executive-summary.png
│       ├── 02-national-electoral-trends.png
│       ├── 03-state-level-voting-behaviour.png
│       ├── 04-geographic-patterns.png
│       ├── 05-electoral-volatility.png
│       ├── 06-2023-presidential-election.png
│       ├── 07-polling-unit-analysis.png
│       ├── 08-electoral-clusters.png
│       └── 09-methodology-data-quality.png
│
└── reports/
    └── analytical-story.md
```

Large source datasets and polling-unit archives may be unsuitable for direct GitHub upload. If they cannot be redistributed or exceed repository limits, document where they came from and how to obtain them instead of committing them.

---

## Running the Project

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
cd YOUR-REPOSITORY
```

### 2. Create and activate a virtual environment (recommended)

```bash
python -m venv .venv
```

On Windows:

```bash
.venv\Scripts\activate
```

On macOS/Linux:

```bash
source .venv/bin/activate
```

### 3. Install the dependencies

```bash
pip install -r requirements.txt
```

### 4. Add the required source data

Place the harmonised election CSV files in the data directory expected by the notebook, or update the notebook's `DATA_DIR` and input paths to match your local folder structure.

The notebook currently contains a local Windows data path. This path must be changed before the notebook can run on another computer.

### 5. Open the notebook

```bash
jupyter notebook
```

Open `notebooks/Master.ipynb` and run the cells in order. Some later analytical sections depend on variables and dataframes created earlier in the notebook.

### 6. Open the Power BI report

Open the `.pbix` file in Power BI Desktop. If the report uses local CSV paths, update the data-source paths and refresh the model.

---

## Important Definitions

| Term | Meaning in this project |
|---|---|
| Registered voters | People recorded on the voter register. |
| Accredited voters | Registered voters accredited to vote, as represented in the source election data. |
| Turnout | Accredited voters divided by registered voters. |
| Valid votes | Votes accepted as valid in the official election results. |
| Rejected votes | Votes classified as rejected in the official election results. |
| Vote share | A party's votes divided by the relevant valid-vote total. |
| Percentage points (pp) | The arithmetic difference between two percentages. A change from 40% to 30% is −10 percentage points. |
| Comparable winner | The leading category among APC, PDP and Other in the longitudinal party structure. |
| ENP | Effective Number of Parties, a measure of how concentrated or dispersed party vote shares are. |
| Electoral volatility | Half the sum of the absolute changes in comparable party vote shares between two elections. |
| Polling-unit win | A party recorded as having the highest vote total in an analysed polling-unit record. |
| Data-quality flag | A record meeting a specified validation condition; it is not proof of misconduct. |

---

## Data Quality and Limitations

The findings should be interpreted with the following considerations in mind:

1. **Differences between election datasets:** The 2015, 2019 and 2023 source files were not originally structured identically. State labels, state codes, party columns and aggregation differed, so harmonisation was required.
2. **Party comparability:** APC/PDP/Other is used for longitudinal comparisons. LP and NNPP are separately analysed in the 2023 full-party view; their earlier absence as separate comparable categories should not be interpreted as zero support.
3. **Polling-unit coverage:** The 2023 polling-unit source had crosschecked, unsure and not-found classifications. Coverage varied considerably by state/FCT unit. Polling-unit findings are therefore a deep-dive view of the available records, not a replacement for official state-level results.
4. **Polling-unit source fields:** The source did not provide all official polling-unit totals needed to calculate valid votes, rejected votes or total votes cast. The analysis uses the fields available and does not manufacture missing measures.
5. **Polling-unit winner counts:** These count analysed records won by each party. They are not national vote totals and should not be compared as if they were.
6. **Validation flags:** Records where four-party votes exceeded accredited voters were flagged for review. The flag alone does not establish why the discrepancy occurred.
7. **Regional averages:** Some geographic visuals use unweighted averages of state-level percentages. These are not the same as voter-weighted regional totals.
8. **Exploratory regression:** The regression models use 37 state-level observations and are intended to explore associations, not establish causality.
9. **Clustering:** Cluster assignments depend on the selected variables, scaling and model configuration. The groups describe similarities in the analysed changes; they do not explain the causes of those changes.
10. **Source reconciliation:** Published figures can differ depending on the specific official measure or stage of collation being compared. The definitions and source basis should be checked before quoting a figure.

---

## Further Questions

This analysis raises several questions for further exploration:

- What factors may help explain the decline in voter participation despite growth in the registered electorate?
- How did the geographic distribution of APC, PDP, LP and NNPP support shape the 2023 result?
- Why did some state/FCT units experience much larger changes in party support than others?
- How much of the observed polling-unit pattern is influenced by uneven source coverage?
- What additional data would be needed to investigate the relationship between voter participation and changes in party support more rigorously?

---

## Project Note

This is an independent data analytics portfolio project. It is intended to explore patterns in published election data and demonstrate a reproducible analytical workflow. It does not claim to establish the causes of voting behaviour, validate every polling-unit record or make findings of electoral misconduct.

**The central takeaway:** Between 2015 and 2023, Nigeria's registered electorate expanded while voter participation declined. At the same time, the traditional dominance of APC and PDP weakened, new political forces gained ground, and electoral change varied substantially across the country's state/FCT units.
