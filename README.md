# Job Market Skills Analysis Using Web Scraping and NLP

An end-to-end pipeline for analysing real-world job market trends by collecting live
remote job postings via API and HTML scraping, then applying NLP techniques to extract
skills, classify roles, and identify hiring patterns for data and analytics positions.

## Problem Statement

Given live job postings from the remote job market, identify which technical skills are
most in demand, how they vary by role family, which seniority levels are most common,
and what terms differentiate roles — helping job seekers and analysts understand the
current data job landscape.

## Data Collection

Data is collected in two stages and merged for richer analysis:

- Stage 1: Remote OK public API (https://remoteok.com/api) — structured metadata including
  job title, company, tags, salary range, and HTML job descriptions
- Stage 2: Individual job page scraping with BeautifulSoup — full page text to supplement
  API descriptions where the API truncates content

Both sources are cleaned, merged, and deduplicated before analysis.

## Pipeline Overview

1. Fetch live job data from the Remote OK API
2. Standardise and deduplicate records
3. Parse HTML job descriptions using BeautifulSoup
4. Filter to analytics and data-related roles using keyword matching
5. Scrape individual job pages for enriched description text (up to 40 pages)
6. Merge API text and scraped page text — use longer source when available
7. Regex-based skill extraction across 25+ technical skills
8. Rule-based role family classification — Data Analyst, Data Engineer, ML Engineer, Data Scientist
9. Rule-based seniority classification — Senior, Manager+, Unspecified
10. Skill frequency analysis and top skills bar chart
11. Skill co-occurrence matrix and heatmap
12. TF-IDF analysis of top terms per role family
13. Word cloud of meaningful technical keywords
14. Salary analysis by skill (where available)
15. Export dashboard-ready CSV files and plot images

## Skills Detected

The pipeline extracts 25+ skills using regex pattern matching including:

Python, SQL, Excel, Tableau, Power BI, Looker, Google Analytics, R, Spark, Scala,
Java, dbt, Airflow, Kafka, Git, Docker, Kubernetes, AWS, GCP, Azure, BigQuery,
Snowflake, Machine Learning, Deep Learning, NLP, Data Visualization, A/B Testing,
Statistics, ETL, Redshift, Databricks

## Output Files

| File | Description |
|---|---|
| analytics_jobs_processed.csv | Full processed dataset with all features |
| analytics_skills_exploded.csv | One row per job-skill pair |
| top_skills.csv | Skill frequency table |
| top_skills_by_role_family.csv | Skill frequency broken down by role |
| tfidf_terms_by_role_family.csv | Top TF-IDF terms per role family |
| skill_cooccurrence_matrix.csv | Co-occurrence counts for top 10 skills |
| dashboard_jobs_summary.csv | Dashboard-ready summary CSV |
| top_15_skills.png | Bar chart of top skills |
| role_family_distribution.png | Role family bar chart |
| seniority_distribution.png | Seniority bar chart |
| skill_cooccurrence_heatmap.png | Co-occurrence heatmap |
| clean_wordcloud.png | Word cloud of technical keywords |

## Tech Stack

| Library | Purpose |
|---|---|
| requests | API calls and web page fetching |
| BeautifulSoup / lxml | HTML parsing and text extraction |
| pandas / numpy | Data manipulation |
| scikit-learn | TF-IDF vectorisation |
| nltk | Lemmatisation for word cloud cleaning |
| wordcloud | Word cloud generation |
| matplotlib | All charts and visualisations |
| tqdm | Progress bars for scraping loop |

## Notes

- The Remote OK API returns approximately 100 records per request. Filtering to
  analytics/data roles typically yields 20–30 jobs from each live snapshot.
- Salary analysis requires listings to include salary fields, which many postings omit.
- Scraping success varies by page structure — approximately 40% of pages yield usable enriched text.
