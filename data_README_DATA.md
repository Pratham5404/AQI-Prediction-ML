# 📊 Dataset Information

## ⚠️ Confidentiality Notice

The dataset used in this project is **proprietary and confidential** and is **not included** in this repository. The raw CSV data files are excluded via `.gitignore` to prevent accidental publication.

---

## Expected Data Format

If you wish to run the notebooks with your own data, your CSV file should contain the following types of columns:

| Column Type | Example Features |
|-------------|-----------------|
| Timestamp | `datetime`, `date`, `timestamp` |
| Particulate Matter | `PM2.5`, `PM10` |
| Gaseous Pollutants | `NO2`, `SO2`, `CO`, `O3` |
| Meteorological | `Temperature`, `Humidity`, `Wind_Speed` |
| Target Variable | `AQI` |

---

## How to Add Your Dataset

1. Place your CSV file(s) in this `data/` folder
2. Rename or update the file path references in the notebooks
3. Ensure the column names match what is expected in the preprocessing cells
4. The `.gitignore` is configured to automatically **exclude all CSV files** from version control

---

## Publicly Available Alternatives

If you do not have access to the original dataset, you may use one of these publicly available air quality datasets:

| Source | Link | Notes |
|--------|------|-------|
| CPCB India | [cpcb.nic.in](https://cpcb.nic.in/) | Official Indian AQI data |
| UCI Air Quality | [UCI ML Repository](https://archive.ics.uci.edu/ml/datasets/Air+Quality) | Italian multi-sensor dataset |
| OpenAQ | [openaq.org](https://openaq.org/) | Global open air quality data |
| Kaggle | [Kaggle AQI Datasets](https://www.kaggle.com/search?q=air+quality+AQI) | Multiple curated datasets |
| WHO | [WHO Air Quality DB](https://www.who.int/data/gho/data/themes/air-pollution) | Global WHO data |
