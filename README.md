# Urban Heat Island Analyzer

A zero-cost, open-source project that generates daily maps of Urban Heat Islands (UHIs) in Malaysian cities using NASA MODIS and local weather data.



## Purpose

Cities trap heat, creating Urban Heat Islands that worsen health risks and reduce comfort.
This project automatically analyzes satellite + weather data to:


- Map the hottest zones in cities.


- Update results every day at 12 PM MYT.


- Show only the latest 14 days of maps for short-term context.

## Features

- Daily Data Refresh: Automated job updates temperature maps every 24 hours.


- Satellite + Ground Data: Combines NASA MODIS imagery with local weather station readings.


- Interactive Maps: Web-friendly heatmaps to explore by date and location.


- Actionable Insights: Highlights areas for tree planting, reflective pavements, or cooling centers.

## Data Sources

NASA MODIS Land Surface Temperature (free) and Local Weather Stations (open government/public APIs).

## How It Works

1. Fetch Data — Daily job fetches MODIS + weather feeds.


2. Process with DuckDB — Data is loaded into uhi.duckdb (lightweight, file-based DB) and aggregated into heat anomaly zones.


3. Map Generation — Daily PNG map is created.


4. Retention Policy — Only last 14 maps are kept, older ones deleted.


5. Publishing — Results are committed back to repo & published on Web Pages.


## Repository Structure

```

uhi-analyzer/
│── data/              # temp working dir (cleared after each run)
│── db/uhi.duckdb      # DuckDB file (latest dataset only)
│── notebooks/         # Jupyter notebooks for dev/experiments
│── scripts/           # Python scripts for fetch, process, map
│── outputs/maps/      # Last 14 days of heat maps
│── .github/workflows/ # GitHub Actions CI/CD
│── README.md          # Project documentation
│── requirements.txt   # Python dependencies

```

## Automation (GitHub Actions)

This repo uses GitHub Actions to retrain/recompute the model daily:


- Runs at 12:00 PM Malaysia Time (4 AM UTC).

- Executes pipeline: `fetch → process → map → cleanup`

- Uses `git commit --amend && git push --force` to overwrite history (prevents repo bloat).

- Keeps 14 days of maps for short-term insights.


## Benefits for Malaysians

1. Daily Heat Awareness : check hot zones before outdoor activity.

2. Short-term Planning : 14-day trends for events, work, and safety planning.

3. Accessible to All : media, NGOs, and citizens can freely embed/share maps.


## Future Plans

- Add vegetation index (NDVI) to correlate heat with greenery.

- Extend history beyond 14 days using free cloud hosting (Hugging Face Datasets / Supabase).

- Add alert system (Telegram bot/ email).


## License

MIT License : free for research, education, and public use.
