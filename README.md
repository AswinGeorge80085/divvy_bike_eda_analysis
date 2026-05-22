# 🚲 Divvy Bikes — Exploratory Data Analysis

> An end-to-end exploratory data analysis of Chicago's Divvy bike-sharing program,
> examining user behavior, trip patterns, station usage, and seasonal trends
> across February–April 2026.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Installation & Setup](#installation--setup)
- [Analysis Summary](#analysis-summary)
- [Key Findings](#key-findings)
- [Business Recommendations](#business-recommendations)
- [Technologies Used](#technologies-used)
- [Author](#author)

---

## Project Overview

**Divvy** is Chicago's official bike-sharing program operated by Lyft in partnership
with the Chicago Department of Transportation. Users can pick up bikes from hundreds
of docking stations across the city and return them at any other station.

This project analyzes **941,274 valid rides** across three months to answer nine
analytical questions about user behavior, trip patterns, peak usage, station popularity,
and seasonal trends — and translates those findings into actionable business
recommendations for Divvy management.

### Two User Types
| User Type | Description |
|-----------|-------------|
| **Casual Riders** | Pay per ride or buy short-term passes |
| **Annual Members** | Subscribe yearly for unlimited 45-minute rides |

---

## Dataset

Three monthly CSV files downloaded from the official
[Divvy System Data portal](https://divvybikes.com/system-data):

| File | Link |
|------|------|
| `202602-divvy-tripdata.csv` | https://divvy-tripdata.s3.amazonaws.com/202604-divvy-tripdata.zip |
| `202603-divvy-tripdata.csv` | https://divvy-tripdata.s3.amazonaws.com/202603-divvy-tripdata.zip
| `202604-divvy-tripdata.csv` | https://divvy-tripdata.s3.amazonaws.com/202602-divvy-tripdata.zip |

### Dataset Columns

| Column | Type | Description |
|--------|------|-------------|
| `ride_id` | string | Unique identifier for each ride |
| `rideable_type` | string | Bike type: `electric_bike` or `classic_bike` |
| `started_at` | datetime | Trip start timestamp |
| `ended_at` | datetime | Trip end timestamp |
| `start_station_name` | string | Name of the starting station |
| `start_station_id` | string | ID of the starting station |
| `end_station_name` | string | Name of the ending station |
| `end_station_id` | string | ID of the ending station |
| `start_lat` | float | Starting latitude coordinate |
| `start_lng` | float | Starting longitude coordinate |
| `end_lat` | float | Ending latitude coordinate |
| `end_lng` | float | Ending longitude coordinate |
| `member_casual` | string | User type: `member` or `casual` |

### Dataset Size
| Metric | Value |
|--------|-------|
| Raw combined rows | 966,739 |
| Rows after cleaning | 941,274 |
| Rows removed | 25,465 (2.63%) |
| Columns (after feature engineering) | 22 |

---

## Project Structure

```
divvy-eda/
│
├── data/                              # Raw CSV files (not included in repo)
│   ├── 202602-divvy-tripdata.csv
│   ├── 202603-divvy-tripdata.csv
│   └── 202604-divvy-tripdata.csv
│
├── Divvy_EDA_Final.ipynb              # Main analysis notebook
│
│
└── README.md                          
```

---

## Installation & Setup

### Prerequisites
- Python 3.8 or higher
- Jupyter Notebook or JupyterLab

### Step 1 — Clone or Download the Repository

```bash
git clone https://github.com/AswinGeorge80085/divvy_bike_eda_analysis
```

### Step 2 — Create a Virtual Environment (Recommended)

```bash
python -m venv .venv

# Windows
.venv\Scripts\activate

# macOS / Linux
source .venv/bin/activate
```

### Step 3 — Install Required Libraries

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

Or install from a requirements file:

```bash
pip install -r requirements.txt
```

**Requirements:**
```
pandas>=1.5.0
numpy>=1.23.0
matplotlib>=3.6.0
seaborn>=0.12.0
jupyter>=1.0.0
```

### Step 4 — Add the Dataset

Download the three CSV files from the links in the [Dataset](#dataset) section
and place them inside a `data/` folder in the project root.

### Step 5 — Run the Notebook

```bash
jupyter notebook Divvy_EDA_Final.ipynb
```

> ⚠️ **Important:** Always use **Kernel → Restart & Run All** when opening the
> notebook to ensure all cells execute in the correct order.

---

## Analysis Summary

The notebook is organized into 8 sections:

| Section | Content |
|---------|---------|
| 1. Environment Setup | Library imports and display settings |
| 2. Data Loading & Understanding | Load 3 files, validate structure, check missing values and duplicates |
| 3. Data Cleaning | Convert dates, calculate duration, remove invalid trips, handle missing stations |
| 4. Feature Engineering | Extract hour, day, month, day type, duration category, time of day |
| 5. Exploratory Data Analysis | 9 analytical questions with charts and interpretations |
| 6. Q&A Summary | Direct answers to all 9 assignment questions |
| 7. Key Insights & Recommendations | Top 8 findings + 4-category business recommendations |
| 8. Conclusion | Final summary paragraph |

### Questions Answered

| # | Question |
|---|----------|
| Q1 | What is the overall profile of Divvy users? |
| Q2 | How long are typical trips and what does the distribution look like? |
| Q3 | Which stations are the most popular? |
| Q4 | How do casual riders and annual members differ in behavior? |
| Q5 | What are the peak hours and peak days? |
| Q6 | What are the seasonal and monthly trends? |
| Q7 | Is there a relationship between trip duration and time? |
| Q8 | Are there station usage patterns specific to each user type? |
| Q9 | What additional insights can be drawn from the data? |

---

## Key Findings

| # | Finding | Data Point |
|---|---------|------------|
| 1 | Members dominate the platform | 73% of all rides |
| 2 | Electric bikes are universally preferred | 68.6% of all rides |
| 3 | Members follow a commuter pattern | Double-peak at 8am & 5pm; peak day = Thursday |
| 4 | Casuals follow a leisure pattern | Single afternoon peak; peak day = Saturday |
| 5 | Casuals ride 45% longer per trip | Avg 16.4 min vs 11.3 min for members |
| 6 | Strong seasonal growth underway | +56% Feb→Mar, +41% Mar→Apr |
| 7 | Station usage is user-type specific | Tourist belt (casuals) vs commuter grid (members) |
| 8 | Electric bikes complete trips faster | Median 7.89 min vs 9.47 min for classic bikes |

### Bonus Insights
- **Round trips** (same start and end station) are significantly more common among
  casual riders — especially on weekends — confirming their leisure riding behavior.
  Top round-trip stations are all tourist and lakefront locations.
- **100% of missing station names** belong to electric bike rides. Electric bikes
  can be locked to street posts rather than docking stations, so no station name
  is recorded. These are valid trips and were retained in the analysis.

---

## Technologies Used

| Library | Version | Purpose |
|---------|---------|---------|
| Python | 3.10+ | Core language |
| Pandas | 1.5+ | Data loading, cleaning, manipulation |
| NumPy | 1.23+ | Numerical operations |
| Matplotlib | 3.6+ | Base plotting engine |
| Seaborn | 0.12+ | Statistical visualizations |
| Jupyter | 1.0+ | Interactive notebook environment |

---

## Author

**Aswin George**
Data Science Internship Program

---

*This project was completed as part of a Data Science Internship assignment
focused on Exploratory Data Analysis using real-world bike-sharing data.*
