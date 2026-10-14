# 🏏 IPL Match Analytics Dashboard
### Exploring Team Performance, Toss Strategy, Match Conditions & Dew Likelihood

An end-to-end sports analytics project using **Power BI, Python, DAX, and historical weather data** to explore IPL match outcomes, team performance, toss decisions, and the relationship between match conditions and chasing strategies.

---

## 📌 Project Overview

Cricket matches are influenced by several factors, including team performance, venue conditions, toss decisions, match timing, and weather. However, the impact of these factors is not always straightforward.

This project analyzes historical Indian Premier League (IPL) matches through an interactive Power BI dashboard. It combines historical match data with fixture timing and weather information to investigate patterns in match outcomes and toss strategy.

The project has two analytical components:

- **Historical IPL Analysis:** Examines team performance, match outcomes, and toss-related patterns across multiple IPL seasons.
- **Match Conditions Analysis:** Investigates the association between match timing, weather-based dew likelihood, chasing outcomes, and decisions made after winning the toss.

The objective is to turn historical cricket data into meaningful, data-driven insights that can support further sports analytics research.

## 🎯 Problem Statement

**How are IPL match outcomes and toss strategies associated with team performance, match timing, and weather-related conditions?**

The project investigates whether historical match data reveals meaningful differences in observed outcomes across these factors, rather than assuming that winning the toss automatically provides a competitive advantage.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| Power BI | Interactive dashboard development and data visualization |
| Python | Data preparation, fixture enrichment, and weather-data processing |
| DAX | Calculated measures and analytical metrics |
| CSV | Structured storage and exchange of match and enriched data |
| Open-Meteo Historical Weather API | Historical hourly weather data for match-condition analysis |
| Git & GitHub | Version control and project documentation |

## 📊 Dataset & Data Preparation

The project uses historical IPL match data obtained from [Cricsheet](https://cricsheet.org/).

The original historical dataset contains **1,243 matches** across 19 seasons. The match data was cleaned and standardized before being used for dashboard development.

Key preparation steps included:

- Standardizing team names across historical seasons.
- Cleaning and validating match outcomes, toss decisions, venues, and other match-level fields.
- Preparing a separate enriched dataset for the match-conditions analysis.
- Matching fixtures with scheduled match dates and start times.
- Enriching the fixture data with historical hourly weather observations.

### Match-Conditions Dataset

The enriched dataset covers the **2016–2026 IPL seasons** and contains **726 matched fixtures**.

| Dataset characteristic | Value |
|---|---:|
| Seasons covered | 2016–2026 |
| Matched fixtures | 726 |
| Weather records successfully matched | 687 |
| Weather coverage | 94.63% |
| Matches with missing weather data | 39 |

The weather-enriched dataset is analyzed separately from the full historical dataset to preserve the intended scope of each dashboard section.

## 🌦️ Weather Enrichment & Dew-Likelihood Methodology

One of the main extensions of this project is the enrichment of IPL fixtures with historical weather observations.

Scheduled fixture information was used to identify match dates and approximate start times. Historical hourly weather data was then retrieved from Open-Meteo and matched to the relevant fixtures.

Weather variables included:

- Temperature
- Relative humidity
- Dew point
- Dew-point depression

### Dew-Likelihood Proxy

Actual dew accumulation on the pitch was not directly measured. Therefore, the project uses a **weather-based dew-likelihood proxy** to classify match conditions.

Dew-point depression is calculated as:

`Dew-point depression = Temperature − Dew point`

A lower dew-point depression generally indicates that the air temperature is closer to the dew point. Relative humidity is also considered when estimating the likelihood of dew-favourable conditions.

The proxy score combines normalized humidity and dew-point-depression components:

`DewProxyScore = 100 × (0.60 × H + 0.40 × Dₛ)`

Where:

- `H` is the normalized humidity component, based on relative humidity.
- `Dₛ` is the normalized dew-point-depression component.
- Both components are clipped to the range 0–1.

The classification rules are:

- **High:** Relative humidity ≥ 80% and dew-point depression ≤ 4°C.
- **Medium:** Relative humidity ≥ 70% and dew-point depression ≤ 6°C, provided the High criteria are not met.
- **Low:** Conditions that do not satisfy the Medium or High criteria.

These categories represent estimated weather conditions, not direct observations of dew on the cricket ground.

## 📈 Power BI Dashboard

The report is organized into four analytical pages.

### 1. How IPL Strategy Has Evolved

Explores historical trends across IPL seasons and examines how match outcomes and strategic patterns have changed over time.

### 2. Who Actually Wins — And Why

Examines match outcomes and toss-related patterns to explore whether winning the toss consistently translates into winning the match.

### 3. Team Analysis

Compares teams across match outcomes and performance indicators to identify differences in historical performance.

### 4. How Match Conditions Shape Toss Strategy

Focuses on the 2016–2026 enriched dataset and investigates:

- Differences in weather-based dew likelihood between day and night matches.
- Observed win rates when batting first versus chasing.
- Toss-winner success after choosing to field, across dew categories.
- Toss-winner success after choosing to bat versus field.
- Differences in toss decisions between day and night matches.

The report uses interactive visuals and comparisons to make these patterns easier to explore.

## 🔍 Key Findings

The enriched dataset reveals several descriptive patterns worth investigating.

- **Match timing and weather:** Night matches had a higher average dew-proxy score than day matches in the enriched dataset.
- **Chasing outcomes:** Observed win rates differed across batting-first and chasing scenarios, with the size of the difference varying by dew category.
- **Toss strategy:** Toss-winner success after choosing to field varied across the Low, Medium, and High dew-likelihood categories.
- **Day versus night decisions:** Choosing to field was more common among toss winners in night matches than in day matches.
- **Toss advantage is not universal:** The observed relationship between winning the toss and winning the match depends on the subset of matches and the conditions being analyzed.

These findings describe associations in the available data. They do not establish that dew or toss decisions directly cause a particular match outcome.

## 🧠 Analytical Approach

The project follows a structured analytics workflow:

1. **Data collection:** Obtain historical IPL match data and fixture information.
2. **Data cleaning:** Standardize team names and validate match-level fields.
3. **Fixture enrichment:** Match historical fixtures with scheduled dates and start times.
4. **Weather enrichment:** Retrieve and match historical weather observations.
5. **Feature engineering:** Calculate dew-point depression, a dew-proxy score, and dew-likelihood categories.
6. **Dashboard development:** Create calculated measures and interactive Power BI visuals using DAX.
7. **Exploratory analysis:** Compare outcomes across teams, seasons, match timing, toss decisions, and dew-likelihood categories.
8. **Interpretation:** Evaluate the observed patterns while considering missing data and the limitations of proxy variables.

## ⚠️ Limitations

- Weather observations are matched using fixture timing and historical hourly data; they are not direct measurements from the pitch.
- Dew likelihood is an estimated proxy, not a confirmed record of dew accumulation.
- Weather data is unavailable for 39 of the 726 enriched fixtures.
- Historical patterns do not establish causation.
- Team composition, player availability, venue characteristics, match format, innings progression, and other variables may also influence match outcomes.
- The enriched analysis covers 2016–2026, while the broader historical analysis covers 19 IPL seasons. Results from these two scopes should not be compared without accounting for their different coverage.

## 📂 Repository Structure

```text
ipl-match-analytics-dashboard/
│
├── README.md
├── dashboard/
│   ├── IPL_Dashboard.pbix
│   └── IPL_Dashboard.pdf
│
├── scripts/
│   ├── fixture_enrichment.py
│   └── weather_enrichment.py
│
└── data/
    └── README.md
```

*This is the intended structure. Keep only the files and folders that are actually present in the repository, and update filenames to match your project.*

The PDF provides a convenient way to view the report pages without Power BI Desktop. The `.pbix` file, if included, allows users with Power BI Desktop to explore the report interactively.

## 🚀 How to Explore the Project

1. Open `dashboard/IPL_Dashboard.pdf` to view the report pages.
2. If the `.pbix` file is included, download it and open it in Power BI Desktop for interactive exploration.
3. Review the `scripts/` directory for the data-enrichment workflow, if the scripts are included.
4. Read the methodology and limitations before interpreting the weather-related findings.

## 🔮 Future Improvements

- Incorporate additional match-level and team-level variables.
- Evaluate the effect of venue, innings, team strength, and match format on observed outcomes.
- Test whether weather-related variables improve the explanatory or predictive performance of statistical models.
- Develop a reproducible automated data-refresh pipeline.
- Explore predictive models for match outcomes using appropriate training and validation procedures.

## 👨‍💻 Author

**Manoj**  
MSc Big Data Analytics | Aspiring Data Analyst & Sports Analytics Enthusiast

Interested in applying data analytics, visualization, and statistical methods to real-world sports problems.

---

**Tools:** Power BI · Python · DAX · Historical Weather Data · Sports Analytics
