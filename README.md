
# 🎵 Spotlytics: Spotify Global Top 100 - End-to-End Data Pipeline

This project implements a fully automated **data engineering pipeline** to extract, process, and analyze Spotify’s weekly **Global Top 100** songs. It leverages modern cloud technologies to build a scalable, serverless architecture that delivers real-time music insights.

---

## 🚀 Business Problem

**Objective:**  
To collect and analyze **Spotify's weekly Global Top 100 chart** to uncover trends in music popularity, artist performance, genre evolution, and streaming behavior.

Stakeholders such as music analysts, producers, and marketers require automated insights to track song momentum, identify breakout artists, and forecast listening patterns. Manual collection is inefficient and error-prone, hence this pipeline solves the need for timely, structured data delivery.

---

## 🔧 Tech Stack & Services Used

| Tool / Service        | Purpose                                      |
|-----------------------|----------------------------------------------|
| **Spotify API**       | Extract weekly chart data                   |
| **AWS Lambda**        | Serverless data extraction & transformation |
| **AWS S3**            | Data lake storage (raw and transformed)     |
| **AWS Glue**          | Data cataloging and schema management       |
| **AWS Athena**        | Serverless SQL queries and analytics        |
| **Python + Spotipy**  | API integration and processing logic        |
| **Pandas**            | DataFrame transformation                    |

---

## 🧩 Pipeline Architecture

![ETL Workflow](https://github.com/user-attachments/assets/574d9232-81c6-4211-83cb-cfafb57535d1)

This diagram illustrates the end-to-end ETL workflow for extracting data from the Spotify API using Python and AWS Lambda, transforming it, and loading it into Amazon Athena for analytics. The pipeline is orchestrated with Amazon CloudWatch, stores data in S3, and utilizes AWS Glue for schema inference and queryability.

### 1. **Data Extraction**

- Source: [Spotify’s Global Top 100 playlist](https://open.spotify.com/playlist/37i9dQZEVXbNG2KDcFcKOF)
- Tool: `spotipy` (Python SDK for Spotify API)
- Process:
  - Deployed on **AWS Lambda**
  - Triggered weekly via **Amazon CloudWatch**
  - Pulls song metadata (track ID, name, artist, album, etc.)
  - Stores raw JSON into `S3/raw_data/to_processed/`

### 2. **Data Transformation**

- Lambda function processes raw JSON from S3:
  - Extracts structured tables for:
    - `albums`
    - `artists`
    - `tracks`
  - Uses `pandas` for normalization
- Output stored as CSV in `S3/transformed_data/`

### 3. **Data Cataloging & Querying**

- **AWS Glue Crawlers**:
  - Automatically catalog transformed CSVs into Glue tables.
- **AWS Athena**:
  - Queries performed directly on S3 data using standard SQL.

---

## 📊 Insights Generated

Here are some of the valuable insights derived using Athena:

1. **Top Artists by Chart Presence**  
2. **Genre Trends Over Time** *(if genre is enriched)*  
3. **Songs with Longest Streak in Top 100**  
4. **Highest Climbing Songs (Week-over-Week)**  
5. **New Entrants vs. Repeat Songs Ratio**  
6. **Average Track Duration Trend**  
7. **Most Collaborative Artists (based on features)**  
8. **Custom Artist Momentum Score** *(based on rank shifts, entry frequency)*

---

## ✅ Business Impact

This project:
- **Automates Spotify data collection** – no manual scraping
- Provides **data-driven insights** to music stakeholders
- Enables **trend forecasting** and **artist performance tracking**
- Supports **self-service analytics** via Athena & dashboards

---

## 📁 Folder Structure

```
├── spotify_api_data_extract.py          # Lambda script to extract Spotify data
├── spotify_transformation_load_function.py  # Lambda function for data cleaning/loading
├── Spotify Data Pipeline Project.ipynb  # Local exploration and testing
├── spotipy_layer.zip                   # Lambda layer for Spotipy and dependencies
├── transformed_data/                   # (S3) CSV output after transformation
└── raw_data/                           # (S3) Raw JSON extracted from Spotify API
```

---

## 🔐 Environment Variables

To run the Lambda locally or test extraction:

```
export client_id=<YOUR_SPOTIFY_CLIENT_ID>
export client_secret=<YOUR_SPOTIFY_CLIENT_SECRET>
```

---

## 📌 Future Enhancements

- Add genre classification (via audio features)
- Integrate with visualization tools (e.g., Power BI, Looker)
- Build ML models to **predict chart entries**
- Add support for region-specific charts (US, UK, etc.)

---

> Built with ❤️ by a data engineer passionate about music, automation, and cloud computing.
