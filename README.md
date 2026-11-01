# COVID-19 Global Analysis Dashboard (Power BI)

An interactive Power BI dashboard that shows how COVID-19 spread across the world, which countries were hit hardest, and how vaccination changed the outcome.

![Dashboard Preview](images/dashboard-preview.png)
<!-- Add a screenshot of your dashboard at images/dashboard-preview.png -->

---

Table of Contents

- [Project Overview](#project-overview)
- [Business Questions](#business-questions)
- [Dataset](#dataset)
- [Data Dictionary](#data-dictionary)
- [Tools Used](#tools-used)
- [Data Preparation](#data-preparation)
- [Dashboard Pages](#dashboard-pages)
- [Key DAX Measures](#key-dax-measures)
- [Key Insights](#key-insights)
- [How to Use This Project](#how-to-use-this-project)
- [Repository Structure](#repository-structure)
- [Limitations](#limitations)
- [Author](#author)

---

 Project Overview

This project analyses real-world COVID-19 data to tell one story: **how the pandemic spread, who was affected most, and whether vaccination made a difference.** The dashboard is built in Power BI and covers cases, deaths, and vaccination trends at the global, continent, and country level.
 Business Questions

1. How many total cases and deaths were reported worldwide?
2. How did new cases change over time, and when did the major waves occur?
3. Which countries had the highest cases and deaths per million people?
4. How does the fatality rate vary between countries and regions?
5. Did higher vaccination coverage lead to fewer deaths?

Dataset

| Item | Details |
|------|---------|
| **Source** | [PASTE SOURCE NAME HERE, e.g. WHO COVID-19 Dashboard / Our World in Data] |
| **Link** | [PASTE DOWNLOAD LINK HERE] |
| **Format** | CSV |
| **Coverage** | [e.g. January 2020 to [END DATE], all reporting countries] |
| **Rows** | [PASTE NUMBER OF ROWS] |
| **Date downloaded** | [DD Month YYYY] |
| **File in this repo** | `data/[YOUR_FILE_NAME].csv` |

> Data is owned by the original source. Please check the source's license and cite it if you reuse the data.

## Data Dictionary

Edit this table to match the columns in your file.

| Column | Description |
|--------|-------------|
| `Date_reported` | Date the figures were reported |
| `Country_code` | ISO country code |
| `Country` | Country name |
| `WHO_region` | WHO region of the country |
| `New_cases` | Newly reported cases that day |
| `Cumulative_cases` | Total cases reported to date |
| `New_deaths` | Newly reported deaths that day |
| `Cumulative_deaths` | Total deaths reported to date |

## Tools Used

- **Power BI Desktop**: data modelling and visualisation
- **Power Query**: data cleaning and transformation
- **DAX**: calculated measures and columns
- **GitHub**: version control and project hosting

## Data Preparation

Steps done in Power Query:

1. Loaded the CSV using **Get Data → Text/CSV**.
2. Set the date column to the **Date** type and numeric columns to **Whole Number**.
3. Replaced null values in new cases and new deaths with `0`.
4. Removed aggregate rows (such as "World" or continent totals) to avoid double-counting. *(Remove this step if your file does not contain them.)*
5. Created a **Date table** for time-based analysis.
6. Renamed columns for readability.

## Dashboard Pages

 Page 1: Global Overview
- KPI cards: total cases, total deaths, fatality rate
- World map of cases per million
- Line chart of new cases over time (7-day average)
- Slicers: continent/region, country, date range

Page 2: Country Comparison
- Top 10 countries by total deaths
- Multi-country trend comparison
- Table of cases, deaths, and fatality rate by country

Page 3: Vaccination Impact
*(Include only if your dataset contains vaccination data.)*
- Vaccination rollout by country
- Vaccination coverage vs. death trend

# Key DAX Measures

Adjust the table and column names to match your model.

```DAX
Total Cases = SUM('Covid'[New_cases])
```

```DAX
Total Deaths = SUM('Covid'[New_deaths])
```

```DAX
Fatality Rate % =
DIVIDE ( [Total Deaths], [Total Cases], 0 ) * 100
```

```DAX
7-Day Avg New Cases =
AVERAGEX (
    DATESINPERIOD ( 'Date'[Date], MAX ( 'Date'[Date] ), -7, DAY ),
    CALCULATE ( SUM ( 'Covid'[New_cases] ) )
)
```

## Key Insights

Fill these in from your own dashboard. Examples of the kind of findings to write:

- [Example: Global cases peaked in [MONTH YEAR] during the Omicron wave.]
- [Example: [COUNTRY] reported the highest total deaths in the dataset.]
- [Example: The fatality rate fell significantly after [YEAR] as vaccination expanded.]







