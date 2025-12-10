# NYC 311 Service Requests — Time, Geography and Text-Driven EDA

This project explores patterns in NYC’s 311 service request data, focusing on time trends, borough differences, response delays and text-based signals. The dataset is large and publicly available on NYC Open Data. The goal is to help city operations teams understand complaint hotspots, peak periods and slow-response categories so they can improve staffing and service levels.

---

## 1. Project Overview

### Dataset
Primary dataset (no login required):  
NYC Open Data — 311 Service Requests  
https://data.cityofnewyork.us/Social-Services/311-Service-Requests/fvrb-kbbt

Note: The full dataset has around 20M rows. For notebooks, it is common to export a filtered subset (for example, last 12 months) and save it locally as:
### Business Goal
Identify which complaint types dominate the workload, how requests vary by time and borough, where the longest delays occur and what recurring keywords reveal about underlying issues. These insights can guide resource allocation, staffing changes and SLA improvements.

### Expected Deliverables
- Cleaned dataset snapshot (`artifacts/nyc311_cleaned_snapshot.csv`)
- Jupyter notebook (`notebooks/EDA_NYC311.ipynb`)
- Saved visualizations under `./artifacts/`
- Light text analysis on complaint descriptions
- Time series and seasonal trend visualizations
- Stakeholder summary with recommended actions

---

## 2. Step-By-Step Plan

1. **Define stakeholder questions**
   - What are the top complaint types?
   - When do daily, weekly and monthly spikes occur?
   - Which boroughs have the longest average response time?
   - What text keywords show up in high-priority issues?

2. **Load the dataset**
   - Read from `data/nyc_311.csv`
   - Print `df.shape`, `df.columns` and `df.sample(5)` to confirm integrity

3. **Initial validation**
   - Check missing values and timestamp formats
   - Standardize borough names
   - Remove duplicates and invalid coordinates

4. **Cleaning**
   - Convert timestamps to datetime
   - Create `response_hours = (ClosedDate – CreatedDate)` in hours
   - Normalize categorical text
   - Drop bad latitude and longitude rows

5. **Univariate EDA**
   - Top complaint types
   - Request counts per borough
   - Distribution of response times

6. **Bivariate EDA**
   - Complaint type × borough comparison
   - Boxplots of response time by complaint type
   - Hour-of-day activity

7. **Checkpoint Summary**
   - Dataset loaded and validated
   - Cleaning completed
   - Core EDA visuals saved in `artifacts/`

8. **Text analysis (light)**
   - Tokenize descriptions
   - Word frequency and bigram patterns

9. **Time series analysis**
   - Daily and monthly request trends
   - Detect spikes using moving averages

10. **Geospatial signals (optional)**
   - Borough-level density summaries
   - Hotspot visualizations if coordinates exist

11. **Insights and recommendations**
   - Staffing guidance
   - SLA improvements
   - Category-specific interventions

12. **Packaging**
   - Notebook, cleaned snapshot and plots exported
   - Optional dashboard or text classifier

---

## 3. Jupyter/Colab-Ready Code

All notebook code is guarded and expects a local CSV. Artifacts are stored in:
Key components included:
- Dataset loader with path fallbacks
- Timestamp parsing and cleaning
- Response time calculation
- Bar plots, histograms and boxplots
- Hour-of-day pattern analysis
- Optional keyword extraction
- Export of cleaned snapshot

---

## 4. Business Insights (Short and Actionable)

- A small set of complaint types generates most of the workload, so resource planning should prioritize them.
- Requests spike at predictable hours, revealing gaps in staffing schedules.
- Some complaint categories experience long delays, indicating bottlenecks in workflow or vendor processes.
- Borough-level differences show the need for localized strategies rather than uniform citywide policies.
- Repeated keywords in descriptions highlight recurring quality-of-life issues that may require proactive steps.

---

## 5. Stretch Goals

- Text classifier using TF-IDF + Logistic Regression
- Clustering complaints with embeddings
- Geospatial clustering (DBSCAN)
- Interactive Streamlit dashboard with filters for borough, complaint type and time

---

## 6. What to Show Stakeholders

- Top 10 complaint categories and their share of total volume  
- Median response time by borough and complaint type  
- Daily or monthly trend visualizations  
- Three focused recommendations tied to SLA and staffing improvements  

---

## 7. Folder Structure
project_nyc311_eda/
├─ notebooks/
│  └─ EDA_NYC311.ipynb
├─ data/
│  └─ nyc_311.csv     # user-provided subset
├─ artifacts/
│  ├─ complaint_type_counts.png
│  ├─ borough_counts.png
│  ├─ response_time_distribution.png
│  ├─ response_time_by_type.png
│  ├─ requests_by_hour.png
│  ├─ nyc311_cleaned_snapshot.csv
├─ src/
│  └─ cleaning.py
├─ deploy/
│  └─ dashboard_mockup/
└─ README.md
### requirements.txt
pandas
numpy
matplotlib
seaborn
plotly
wordcloud
