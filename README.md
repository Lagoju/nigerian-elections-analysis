# Nigeria Presidential Election Analysis (2015–2023)

## Project Overview

This project examines how voting behaviour in Nigeria changed across the 2015, 2019 and 2023 presidential elections. It combines national and state-level election results with a separate 2023 polling-unit dataset to investigate turnout, party support, electoral competition, changes in state winners and patterns of electoral volatility.

The analysis was completed using **Python** for data preparation, statistical analysis and clustering, and **Power BI** for interactive reporting.

The central question behind the project is:

> **How has voting behaviour in Nigeria changed between the 2015, 2019 and 2023 presidential elections?**

Before proceeding, I must highlight that this project focuses on observable changes in the available election data. It does not attempt to establish why individual voters made particular choices, and statistical associations and correlations are not interpreted as proof of causation.

## Objectives

- Compare registered voters, accredited voters, votes cast, valid votes and rejected ballots across the three elections.
- Examine changes in APC and PDP support using a comparable party grouping across election years.
- Higlight the broader party landscape in 2023, including LP and NNPP.
- Identify states where the presidential winner changed between elections.
- Measure electoral volatility and compare it with winner-switching patterns.
- Explore differences in voting patterns across Nigeria's geopolitical zones.
- Analyse the available 2023 polling-unit results while documenting coverage and data-quality limitations.
- Use exploratory regression and clustering to investigate state-level patterns.
- Present the findings in an interactive Power BI report.

## Research Questions

1. How did the size of the registered electorate change between 2015 and 2023?
2. How did accreditation and turnout change over the same period?
3. Did APC and PDP remain dominant, or did the 2023 election show a more fragmented party landscape?
4. How did state-level party support and winning margins change?
5. How many states changed their presidential winner between election cycles?
6. Were states with a change in winner also characterised by higher electoral volatility?
7. How did party support vary across geopolitical zones?
8. What can the available 2023 polling-unit data tell us, and what are its limitations?
9. Can states be grouped by similarities in their electoral changes from 2019 to 2023?

## Data Sources and Scope

The project uses election-result material from the Independent National Electoral Commission (INEC) and structured secondary datasets used during the collection and harmonisation process.

| Election dataset | Use in the project |
|---|---|
| INEC 2015 Presidential Election Summary | 2015 national and state presidential results |
| INEC 2019 General Election Report | 2019 election results and validation reference |
| INEC 2023 General Election Report, Annexure 2 | Official 2023 national reference figures |
| Nigeria2.0 structured election data | Structured state-level 2023 party results and polling-unit data used in the analysis |
| Stears and other supplementary material | Secondary cross-checking and source investigation |

INEC is treated as the primary reference source where official election-report figures are available. Structured secondary data were used where they provided a workable format for analysis. Differences between source figures are documented rather than silently replaced.

### Dataset scope

The harmonised state-level comparison covers **37 reporting units: the 36 states and the Federal Capital Territory (FCT)**, across three presidential elections.

The separate 2023 polling-unit dataset contains **123,918 records**. It is analysed separately from the state-level comparison because its coverage and data structure are not equivalent to the national state-result dataset.

## Definitions and Measures

| Measure | Definition used |
|---|---|
| Registered voters | Number of voters on the electoral register |
| Accredited voters | Number of voters recorded as accredited |
| Turnout | Accredited voters divided by registered voters, multiplied by 100 |
| Valid votes | Votes accepted as valid |
| Rejected votes | Votes rejected as invalid |
| Party vote share | Party votes divided by valid votes, multiplied by 100 |
| Winning margin | Difference in vote share between the first- and second-place parties |
| Effective Number of Parties (ENP) | A measure of electoral competition; higher values indicate a more fragmented vote |
| Winner switching | A change in the party with the highest vote total in a state between two elections |
| Electoral volatility | A Pedersen-style measure of the aggregate change in party vote shares between elections |

### Comparable Party Grouping

To compare the three elections on a consistent basis, the analysis groups votes into **APC, PDP and Other**. In this comparison, `Other` includes all votes outside APC and PDP, including LP and NNPP in 2023.

The full 2023 party analysis is presented separately using **APC, PDP, LP, NNPP and Other**, where `Other` excludes the four named parties. These two groupings answer different questions and should not be treated as interchangeable.

## Data Preparation and Validation

The Python workflow harmonises the election data into consistent state- and election-level structures.

The preparation process includes:

1. Identifying the variables needed for comparison: state, registered voters, accredited voters, votes cast, valid votes, rejected votes, party votes and winning party.
2. Standardising state names and state identifiers for cross-election comparisons.
3. Harmonising party categories where the source data allow a comparable grouping.
4. Calculating turnout, party vote shares, winning margins, ENP and winner-switching indicators.
5. Checking arithmetic relationships within the source data, including:
   - APC + PDP + Other = valid votes, for the 2019 grouped data.
   - Valid votes + rejected votes = total votes, where the relevant source fields are available.
6. Comparing selected national figures against INEC references.
7. Keeping the 2023 polling-unit analysis separate and checking its coverage and internal consistency.

The Nigeria2.0 API documentation was reviewed during source investigation, but the endpoint could not be accessed in the working environment. The analysis therefore uses the structured files available to the project.

### Source discrepancies

Some figures in the working dataset differ from the corresponding INEC reference figures. Examples documented during the project include:

| Measure | Working dataset | INEC reference noted in project material |
|---|---:|---:|
| 2019 registered voters | 82,344,107 | 84,004,084 |
| 2023 registered voters | Approximately 93.2 million | 93,469,008 |
| 2023 APC votes | 8,805,655 | 8,794,726 |
| 2023 valid votes | 24,030,689 | 24,025,940 |

These differences may reflect source definitions, aggregation or transcription differences. They are retained as a data-quality consideration and should be reconciled before the figures are used for official reporting. The README does not silently substitute one source's values for another.

## Python Analysis

The analysis notebook is organised into sections covering data preparation, descriptive analysis, state comparisons, polling-unit analysis, regression and clustering.

### National Electoral trends

The national comparison indicates that the registered electorate expanded while accreditation and turnout declined.

| Indicator | 2015 | 2019 | 2023 |
|---|---:|---:|---:|
| Registered voters | 67.4m | 82.3m | 93.2m |
| Accredited voters | 31.7m | 29.4m | 25.3m |
| Turnout | 47.09% | 35.66% | 27.13% |
| Total votes cast | 29.43m | 28.61m | 24.98m |
| Valid votes | 28.59m | 27.32m | 24.04m |
| Rejection rate | 2.87% | 4.51% | 3.76% |

Turnout declined by approximately **42.39% relative to its 2015 level** over the period. This is a descriptive trend in the compiled dataset; it does not by itself explain the reasons for non-participation.

### Party competition

Using the comparable APC/PDP/Other grouping:

| Indicator | 2015 | 2019 | 2023 |
|---|---:|---:|---:|
| APC winner share | 53.96% | 55.60% | 36.63% |
| Winning margin | 9.00 pp | 14.38 pp | 2.33 pp |
| Comparable ENP | 2.03 | 2.08 | 2.97 |

The comparable APC and PDP vote-share total fell from approximately **98.92% in 2015** to **96.82% in 2019** and **65.69% in 2023**.

The separate full-party 2023 breakdown is:

| Party grouping | 2023 vote share |
|---|---:|
| APC | 36.63% |
| PDP | 29.06% |
| LP | 25.37% |
| NNPP | 6.23% |
| Other | 2.71% |

The 2023 results therefore show a more fragmented party landscape in the compiled data, with LP and NNPP appearing as substantial forces alongside APC and PDP.

### State-level winner changes

The state-level comparison records:

- **6 of 37 states/reporting units (16.2%)** changing winner between 2015 and 2019.
- **25 of 37 states/reporting units (67.6%)** changing winner between 2019 and 2023.

This indicates a substantial increase in state-level winner switching in the 2019–2023 comparison. A change in the winning party does not necessarily mean that every voter changed preference; it describes the party with the highest recorded vote total in each state.

### State-level party-share changes

The largest APC vote-share declines between 2019 and 2023 in the project dataset were recorded in:

| State | Change in APC vote share |
|---|---:|
| Yobe | -48.99 pp |
| Kano | -47.06 pp |
| Gombe | -43.89 pp |
| Bauchi | -40.84 pp |
| Borno | -36.72 pp |

These are percentage-point changes in vote share, not percentage changes in the number of votes.

### Electoral volatility

The analysis compares volatility with whether a state changed its winner. The project results show:

| State grouping | Mean volatility, 2019–2023 |
|---|---:|
| Winner-changing states | 48.80 |
| Non-switching states | 22.44 |

Winner-changing states had higher mean volatility in this dataset. This is a descriptive association and should not be interpreted as evidence that volatility caused a winner change.

### Geopolitical-zone analysis

The project compares party shares and turnout across Nigeria's geopolitical zones. Zone-level values in the relevant visuals are **unweighted averages of state-level values**, unless otherwise stated. They are not population-weighted or calculated by pooling all votes within a zone. This distinction matters when interpreting differences between zones.

### 2023 polling-unit analysis

The polling-unit dataset contains **123,918 observations**. The recorded polling-unit winners are:

| Party | Polling-unit wins |
|---|---:|
| APC | 50,797 |
| LP | 40,052 |
| PDP | 26,849 |
| NNPP | 6,220 |

The polling-unit winner agreed with the official state winner in **32 of 37** states/reporting units in the comparison performed.

The project flagged **7,951 records (approximately 6.4%)** where the combined votes for the four named parties exceeded accredited voters. This is treated as a data-quality flag requiring investigation. It is not, by itself, evidence of fraud or proof of what occurred at a polling unit.

Coverage is uneven across states. The project notes a range from approximately **1.98% in Zamfara to 91.90% in Ekiti** for the source classification used in its coverage check. This coverage measure describes the share of records cross-checked under that source classification; it should not be interpreted as proof that the remaining polling units did not exist or did not report results.

### Exploratory Regression

The project uses state-level regression models to explore relationships between changes in party vote share and selected electoral indicators. The small sample size (37 states/reporting units) limits the strength and generalisability of these models.

Selected results documented in the project include:

- The APC change model has an R² of approximately **0.258**. The HC3-robust p-values reported for turnout change, ENP change and winning-margin change are approximately 0.284, 0.706 and 0.116 respectively; none is statistically significant at the 5% level.
- The PDP change model has an R² of approximately **0.506**. The turnout coefficient is reported as approximately -244.22 with a p-value of 0.008; the winning-margin p-value is approximately 0.065 and the ENP p-value approximately 0.887.
- A leave-one-out check for Rivers changes the APC model R² from approximately 0.258 to 0.347, indicating that individual states can materially affect model fit.

These are exploratory associations, not causal estimates. The small number of observations, model specification and potential influence of individual states were considered when interpreting the results.

### Electoral Clustering

Perhaps the most exciting aspect of the project, K-means clustering groups the 37 states/reporting units into six clusters using standardised changes in APC share, PDP share and comparable ENP between 2019 and 2023.

| Cluster | Number of states | Profile from project analysis |
|---|---:|---|
| A | 5 | Abia, Anambra, Ebonyi, Enugu and Imo; APC share fell by 13.19 pp, PDP share by 70.97 pp and comparable ENP by 0.39 |
| B | 10 | Bauchi, Borno, Gombe, Jigawa, Kaduna, Kano, Katsina, Kebbi, Niger and Yobe; APC share fell by 36.38 pp, PDP share rose by 21.63 pp and comparable ENP rose by 0.79 |
| C | 9 | Bayelsa, Benue, Delta, Edo, FCT, Lagos, Nasarawa, Plateau and Taraba; APC share fell by 14.60 pp, PDP share by 30.93 pp and comparable ENP rose by 0.53 |
| D | 4 | Ekiti, Ogun, Ondo and Oyo; APC share rose by 13.09 pp, PDP share fell by 18.60 pp and comparable ENP fell by 0.17 |
| E | 3 | Akwa Ibom, Cross River and Rivers; APC share rose by 7.63 pp, PDP share fell by 44.65 pp and comparable ENP rose by 1.06 |
| F | 6 | Adamawa, Kogi, Kwara, Osun, Sokoto and Zamfara; APC share fell by 10.12 pp, PDP share rose by 3.54 pp and comparable ENP rose by 0.27 |

The clusters describe similarities in the selected electoral-change variables. They are not causal categories, and states in the same cluster are not necessarily geographically adjacent. Cluster labels are identifiers, not rankings.

## Power BI Report

The Power BI report presents the analysis across nine pages.

| Page | Focus | Main content |
|---|---|---|
| 1. Executive Summary | Main findings | Voter-register growth, turnout decline, state winner changes and the 2023 comparable winning margin |
| 2. National Electoral Trends | Participation and ballots | Registered versus accredited voters, valid versus rejected votes and rejection rate |
| 3. State-Level Voting Behaviour | State comparisons | APC vote-share leaders, changes in winning margins and high-volatility states |
| 4. Geographic Patterns | Geopolitical zones | Average state turnout by zone, party share by zone and top state turnout values |
| 5. Electoral Volatility | Vote-share movement | Highest-volatility states, average volatility by period and volatility by winner-switch status |
| 6. 2023 Presidential Election | Full party landscape | National party shares, state winner map and party shares across states |
| 7. Polling-Unit Analysis | Disaggregated results | Polling-unit wins by party, winner distribution by state and votes-exceeding-accredited data-quality flags |
| 8. Electoral Clusters | State groupings | Cluster sizes, cluster profiles and geographic cluster map |


### Screenshots

Add report screenshots to `powerbi/screenshots/` using the filenames below. The image links will display once the corresponding files are included in the repository.

- `dashboard-overview.png`
- `01-executive-summary.png`
- `02-national-electoral-trends.png`
- `03-state-level-voting-behaviour.png`
- `04-geographic-patterns.png`
- `05-electoral-volatility.png`
- `06-2023-presidential-election.png`
- `07-polling-unit-analysis.png`
- `08-electoral-clusters.png`
- `09-methodology-data-quality.png`

Example Markdown image syntax:

```md
![Executive Summary](powerbi/screenshots/01-executive-summary.png)
```

## Data Model

The Power BI model is organised around dimension and fact tables.

### Dimension tables

- `dim_state`
- `dim_election`
- `dim_party`

### Fact tables

- `fact_state_election`
- `fact_party_result`
- `fact_volatility`
- `fact_cluster`
- `fact_polling_unit`
- `fact_pu_coverage`

The model includes 36 states and FCT, three elections and five party categories. The principal fact-table row counts documented during the project are:

| Table | Rows |
|---|---:|
| `fact_state_election` | 111 |
| `fact_volatility` | 74 |
| `fact_cluster` | 37 |
| `fact_party_result` | 407 |
| `fact_pu_coverage` | 37 |
| `fact_polling_unit` | 123,918 |

## Repository Structure

The following is a suggested structure. Update the paths to match the files actually committed to the repository.

```text
nigeria-election-analysis/
│
├── README.md
├── notebooks/
│   └── Master.ipynb
│
├── data/
│   ├── raw/
│   └──cleaned/
│    │
├── powerbi/
│   ├── Nigeria_Election_Analysis.pbix
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
│      
│
└── images/
│       ├── executive-summary.png
│       ├── national-electoral-trends.png
│       ├── state-level-voting-behaviour.png
│       ├── geographic-patterns.png
│       ├── electoral-volatility.png
│       ├── 2023-presidential-election.png
│       ├── polling-unit-analysis.png
│       ├── electoral-clusters.png
```
## Tools and Skills Demonstrated

- **Python:** pandas, NumPy, Matplotlib, SciPy, scikit-learn and statsmodels.
- **Data preparation:** cleaning, standardisation, harmonisation, validation and feature creation.
- **Exploratory analysis:** descriptive statistics, state comparisons and trend analysis.
- **Electoral analysis:** vote shares, turnout, winning margins, ENP, winner transitions and volatility.
- **Statistical analysis:** regression, robust standard errors, diagnostic checks, VIF and influence checks.
- **Unsupervised learning:** K-means clustering, standardisation and silhouette-based evaluation.
- **Business intelligence:** Power BI data modelling, DAX measures, report design and interactive visualisation.
- **Analytical communication:** translating data patterns into findings while documenting uncertainty and limitations.

## Limitations Of The Project

1. **Source comparability:** The three election datasets were assembled from sources with differences in structure and available fields. Harmonisation improves comparability but does not remove every source-definition issue.
2. **National figure discrepancies:** Some working figures differ from INEC references. These differences are documented and should be reconciled before official use.
3. **State-level turnout:** The project notes that reliable, harmonised state-level turnout data for 2023 were not available in the working dataset. Missing values were not invented.
4. **Party aggregation:** The comparable APC/PDP/Other grouping is useful for longitudinal comparison but masks the distinct performance of LP and NNPP in 2023. The full-party 2023 view is therefore presented separately.
5. **Polling-unit coverage:** The 2023 polling-unit data have uneven state coverage and should not be treated as a complete, uniformly representative national census of polling units.
6. **Polling-unit validation flags:** Votes exceeding accredited voters identify records for review; the flag alone does not establish misconduct or fraud.
7. **Regression sample size:** Models use only 37 state/FCT observations. Results are exploratory and sensitive to model choices and individual observations.
8. **Clustering interpretation:** Clusters depend on the selected variables, scaling and chosen number of clusters. They are descriptive groupings, not explanations of voter behaviour.
9. **Ecological inference:** State-level patterns cannot be used to infer the motivations or behaviour of individual voters.

## Overall Conclusion

Across the 2015–2023 period, the analysis shows a larger registered electorate alongside declining accreditation and turnout. The 2023 presidential election also presents a more fragmented party landscape than the earlier elections in the comparable analysis, with LP and NNPP becoming significant parts of the full-party picture. State-level winner switching increased sharply between 2019 and 2023, and states that changed winner had higher average electoral volatility in the project dataset.

These findings describe changes in recorded election outcomes. Understanding the causes of those changes would require additional evidence, such as voter-level surveys, campaign and candidate information, local context and more complete election-administration data.

## Sources and Further Reading

The project source material includes:

- Independent National Electoral Commission (INEC), 2015 Presidential Election Summary(https://collata.ng/sources).
- Independent National Electoral Commission (INEC), 2019 General Election Report(https://inecnigeria.org/wp-content/uploads/2020/11/REPORT-OF-THE-2019-GENERAL-ELECTION.pdf).
- Independent National Electoral Commission (INEC), 2023 General Election Report, Annexure 2(https://wp1.inecnigeria.org/wp-content/uploads/2024/02/2023-GENERAL-ELECTION-REPORT-1.pdf).
- Nigeria2.0 structured election data and related documentation(https://nigeria2.com/elections/results).
- Stears election-data material consulted during source investigation(https://open-data.stears.co/elections/nigeria-presidential-elections).

Consult the original publications and dataset documentation for authoritative figures, definitions and permitted reuse. 

## Disclaimer

This is an independent portfolio and learning project. It is an analysis of compiled election-result data, not an official publication by INEC or any other election-management body. Figures and conclusions are subject to the source, harmonisation and coverage limitations described above. The analysis does not make claims of electoral fraud or infer individual voter motivations.
Furthermore, while this project identifies associations and correlations within the data, these findings should not be interpreted as evidence of causation. The author accepts no responsibility for conclusions drawn from the findings when they are used or presented outside their intended analytical context.

## Author

**Jonah Peter**

Junior Data Analyst | Python | Power BI | Data Analysis


