# Aviation-ETL
#  Full Aviation ETL Notebook — APIs → Cleaning → BigQuery  This notebook:  - Fetches data from AviationAPI (Airports, Preferred Routes, VATSIM) - Fetches METAR from NOAA Aviation Weather Center - Cleans / normalizes dataframes - Uploads results to Google BigQuery using a service account (explicit credentials)
Aviation Data Pipeline
METAR Weather • Airport Data • Preferred Routes • VATSIM Traffic → BigQuery → Looker Studio Dashboard

This project implements a full Aviation Data Engineering Pipeline that extracts data from multiple aviation APIs, transforms and cleans it in Python, loads it into Google BigQuery, and visualizes it in a fully designed Looker Studio Dashboard.

🚀 Features
✔ Multi-Source Aviation Data Extraction

The pipeline collects data from:

Airports — ICAO, IATA, location, elevation

METAR (NOAA AWC) — temperature, wind, visibility, clouds, conditions

Preferred Routes — structured IFR routes

VATSIM Pilots — real-time virtual air traffic positions

✔ Data Cleaning & Transformation

Normalizes multi-format aviation API responses

Handles nested JSON fields

Converts lists/dicts to structured columns

Cleans METAR & weather fields

Standardizes units and timestamps

Removes incomplete or invalid records

✔ BigQuery Integration

The notebook automatically creates the dataset:

portfolio-480204.aviation_data


Tables written:

Table	Description
airports	Cleaned master airport table
metar	Normalized METAR weather observations
preferred_routes	IFR route structure
vatsim_pilots	Live VATSIM pilot traffic snapshot
✔ Looker Studio Dashboard

A full dashboard template is included:

looker_studio_aviation_ops.json


Dashboard pages include:

Airport overview

METAR weather insights

Preferred IFR routes explorer

Live VATSIM aircraft map

Traffic analytics and heatmaps

📁 Repository Structure
📦 aviation-pipeline/
│
├── all_aviation_pipeline.ipynb
├── looker_studio_aviation_ops.json
├── README.md
└── requirements.txt

🔧 Installation & Setup
1. Clone the repository
git clone https://github.com/<your-username>/aviation-pipeline.git
cd aviation-pipeline

2. Install dependencies
pip install -r requirements.txt

3. Add your Google Cloud service account

Place your service account file inside the project:

service_account.json


Update the notebook:

SERVICE_ACCOUNT_FILE = "service_account.json"

4. Configure BigQuery dataset

Inside the notebook:

project_id = "portfolio-480204"
dataset_id = "aviation_data"

🗄 BigQuery Table Schemas
airports
_query_apt, name, city, state, country, latitude, longitude, elevation

metar
_query_apt, raw_text, temp, wind_speed, wind_dir, visibility, time

preferred_routes
origin, destination, route, notes

vatsim_pilots
callsign, aircraft, dep, arr, altitude, ground_speed, stage_of_flight,
latitude, longitude

📊 Looker Studio Dashboard Import
Option A — Import via JSON URL

Upload looker_studio_aviation_ops.json to GitHub

Copy the raw URL

Open Looker Studio Importer:

https://lookerstudio.google.com/reporting/create?c.mode=edit&jsonSpec=<RAW_JSON_URL>

Option B — Manual Setup

Create a new Looker Studio report

Add new data source → BigQuery

Connect to:

portfolio-480204 → aviation_data → airports
portfolio-480204 → aviation_data → metar
portfolio-480204 → aviation_data → preferred_routes
portfolio-480204 → aviation_data → vatsim_pilots

▶ Running the Pipeline

In the notebook:

airports_df, metar_df, routes_df, vatsim_df = run_full_pipeline_safe()


Upload to BigQuery:

upload_df_to_bq(bq_client, airports_df, dataset_id, "airports")
upload_df_to_bq(bq_client, metar_df, dataset_id, "metar")
upload_df_to_bq(bq_client, routes_df, dataset_id, "preferred_routes")
upload_df_to_bq(bq_client, vatsim_df, dataset_id, "vatsim_pilots")

📈 Dashboard Preview

(Add your screenshot here)

🤝 Contributing

Contributions are welcome!
Ideas for extensions:

Add TAF forecasts

Add FAA delay datasets

Add ML-based delay prediction model

📧 Contact

Author: Max Abraham
Project: Aviation Data Pipeline
BigQuery Project: portfolio-480204
