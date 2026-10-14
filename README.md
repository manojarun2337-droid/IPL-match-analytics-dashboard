\# 🏏 IPL Match Analytics Dashboard



\### Exploring Team Performance, Toss Strategy, Match Conditions \& Dew Likelihood



An end-to-end sports analytics project using \*\*Power BI, Python, DAX, and historical weather data\*\* to explore IPL match outcomes, team performance, toss decisions, and weather-related match conditions.



\## 📌 Project Overview



Cricket match outcomes can be influenced by team strength, venue conditions, toss decisions, match timing, and weather. This project uses historical Indian Premier League (IPL) data to investigate patterns in match outcomes and toss strategy through an interactive Power BI dashboard.



The project combines historical match analysis with a separate weather-enriched dataset covering the 2016–2026 seasons.



\### 🎯 Problem Statement



\*\*How are IPL match outcomes and toss strategies associated with team performance, match timing, and weather-related conditions?\*\*



The objective is to identify meaningful patterns in historical match data and investigate whether chasing outcomes and toss decisions vary across different match conditions.



\## 🛠️ Technology Stack



\- \*\*Power BI:\*\* Interactive dashboards and data visualization

\- \*\*Python:\*\* Data cleaning, fixture enrichment, and weather-data processing

\- \*\*Pandas \& NumPy:\*\* Data manipulation and feature engineering

\- \*\*DAX:\*\* Calculated measures and analytical metrics

\- \*\*Open-Meteo Historical Weather API:\*\* Historical weather observations

\- \*\*Git \& GitHub:\*\* Version control and project documentation



\## 📊 Dataset \& Preparation



Historical IPL match data was obtained from \[Cricsheet](https://cricsheet.org/).



The original historical dataset contains \*\*1,243 matches across 19 seasons\*\*. The data was cleaned and standardized before being used for analysis.



Key preparation steps included:



\- Standardizing team names across historical seasons.

\- Validating match outcomes, toss decisions, and venue information.

\- Enriching fixture data with scheduled match dates and start times.

\- Matching historical hourly weather observations to match fixtures.

\- Engineering weather-based indicators for dew-likelihood analysis.



\### Weather-Enriched Dataset



The separate match-conditions dataset covers the \*\*2016–2026 IPL seasons\*\*.



| Metric | Value |

|---|---:|

| Matched fixtures | 726 |

| Weather records matched | 687 |

| Weather coverage | 94.63% |

| Missing weather records | 39 |



\## 🌦️ Dew-Likelihood Methodology



Actual dew accumulation on the pitch was not directly measured. Therefore, this project uses a \*\*weather-based dew-likelihood proxy\*\* derived from relative humidity and dew-point depression.



Dew-point depression is calculated as:



`Dew-point depression = Temperature − Dew point`



The proxy score combines normalized humidity and dew-point-depression components:



`DewProxyScore = 100 × (0.60 × H + 0.40 × Dₛ)`



Where `H` represents the normalized humidity component and `Dₛ` represents the normalized dew-point-depression component.



The classification rules are:



\- \*\*High:\*\* Relative humidity ≥ 80% and dew-point depression ≤ 4°C.

\- \*\*Medium:\*\* Relative humidity ≥ 70% and dew-point depression ≤ 6°C, provided the High criteria are not met.

\- \*\*Low:\*\* Conditions that do not satisfy the Medium or High criteria.



These categories estimate weather conditions favourable to dew formation; they do not confirm that dew was present on the pitch.



\## 📈 Power BI Dashboard



The report contains four analytical pages.



\### 1. How IPL Strategy Has Evolved

Explores historical patterns across IPL seasons and examines changes in match outcomes and strategy.



\### 2. Who Actually Wins — And Why

Investigates match outcomes and toss-related patterns to explore whether winning the toss consistently translates into winning the match.



\### 3. Team Analysis

Compares historical team performance and match outcomes across the IPL.



\### 4. How Match Conditions Shape Toss Strategy

Uses the weather-enriched 2016–2026 dataset to investigate:



\- Dew-likelihood differences between day and night matches.

\- Observed win rates when batting first versus chasing.

\- Toss-winner success after choosing to field across dew categories.

\- Toss-winner success after choosing to bat versus field.

\- Differences in toss decisions between day and night matches.



\## 🔍 Key Findings



The analysis identifies several descriptive patterns:



\- \*\*Match timing:\*\* Night matches had a higher average dew-proxy score than day matches in the enriched dataset.

\- \*\*Chasing outcomes:\*\* Observed win rates differed across dew categories and innings strategies.

\- \*\*Toss strategy:\*\* Toss-winner success after choosing to field varied across the Low, Medium, and High dew-likelihood categories.

\- \*\*Day versus night:\*\* Toss winners chose to field more frequently in night matches than in day matches.

\- \*\*Context matters:\*\* Winning the toss alone does not consistently explain match outcomes across every subset of matches.



These findings describe associations in historical data and do not establish that dew or toss decisions directly cause a particular result.



\## 🔄 Project Workflow



1\. Collect historical IPL match data.

2\. Clean and standardize team names and match-level fields.

3\. Enrich fixtures with scheduled dates and start times.

4\. Retrieve and match historical weather observations.

5\. Engineer dew-likelihood indicators.

6\. Create DAX measures and interactive Power BI visuals.

7\. Compare observed outcomes across teams, seasons, toss decisions, and match conditions.

8\. Interpret findings while accounting for missing data and methodological limitations.



\## 📂 Repository Structure



```text

ipl-match-analytics-dashboard/

├── README.md

├── dashboard/

│   ├── IPL\_Dashboard.pbix

│   └── IPL\_Dashboard.pdf

├── notebooks/

│   └── ipl\_weather\_enrichment\_portable.ipynb

├── data/

└── scripts/

```



The PDF provides a convenient way to view the dashboard pages. The Power BI file can be opened in Power BI Desktop for interactive exploration.



The notebook documents the Python weather-enrichment workflow. Input datasets must be supplied separately before running the workflow.



\## ⚠️ Limitations



\- Dew likelihood is estimated from weather variables, not directly measured on the pitch.

\- Weather observations are unavailable for 39 of the 726 enriched fixtures.

\- Historical associations do not establish causation.

\- Team composition, venue characteristics, player availability, and other match-level factors may influence outcomes.

\- The historical dashboard and weather-enriched analysis cover different season ranges and should be interpreted within their respective scopes.



\## 🚀 Future Improvements



\- Incorporate additional team, player, and venue-level variables.

\- Investigate the relationship between weather conditions and match outcomes using statistical models.

\- Evaluate whether weather-related features improve predictive performance.

\- Develop a reproducible automated data-refresh pipeline.

\- Extend the analysis to additional cricket formats and competitions.



\## 📚 Data Sources



\- \[Cricsheet — Historical Cricket Data](https://cricsheet.org/)

\- \[Open-Meteo — Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api)



\## 👨‍💻 Author



\*\*Manoj\*\*  

MSc Big Data Analytics | Aspiring Data Analyst \& Sports Analytics Enthusiast



Interested in applying data analytics, statistical methods, and visualization to real-world sports problems.



\---



\*\*Built with:\*\* Power BI · Python · Pandas · NumPy · DAX · Historical Weather Data

