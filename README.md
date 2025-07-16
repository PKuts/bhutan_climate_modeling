
# 🌏 Bhutan Climate Modeling

This repository is part of [Omdena's local chapter challenge](https://www.omdena.com/chapter-challenges/leveraging-ai-to-combat-climate-change-in-bhutan), focused on leveraging AI to combat climate change in Bhutan.

## ✅ Project Goals

- Understand historical meteorological trends and seasonal/regional patterns  
- Build and validate predictive models to forecast floods and extreme weather events such as glacial lake outburst floods (GLOFs)  
- Support downstream applications like risk maps and early-warning systems

## 📄 Project Documentation

I created this workflow and presented this to the team to support understanding and communication:

- [docs/bhutan_flood_model_workflow.pdf](docs/bhutan_flood_model_workflow.pdf):  
  A visual overview of the Bhutan flood risk prediction workflow. It outlines how ERA5 historical data and GraphCast forecasts are used to train and deploy a machine learning model for real-time flood risk assessment, along with a Q&A-style explainer covering common questions about model training, feature selection, proxy labels, GraphCast usage, and more.

These files help both technical and non-technical stakeholders understand our modeling strategy and deployment plan.


## Project Roadmap

### 1. Data Collection
**Goal:** Fetch and organize relevant data from multiple sources  

####  ERA5 Hourly Reanalysis (Main Source)
- **Variables:**  
  - `Total_precipitation`  
  - `2m_temperature`  
  - `2m_dewpoint_temperature`  
  - `10m_u_component_of_wind`  
  - `10m_v_component_of_wind`  
  - `surface_solar_radiation_downwards`  
  - `potential_evaporation`  
  - `snow_depth`  
  - `Snowmelt`  
  - `Soil temperature level 1`  
  - `Relative_humidity`
- **Region:** Bhutan bounding box
- **Temporal range:** 1979 to latest year
- **Tools:** `cdsapi`, structured folder organization (by variable/year)

####  Other Explored Data Sources
- Local MET data (RH, Tmax, Tmin, Rainfall)
- GLOF/flood event history 
- River discharge or lake level data (if available)
- DEM/topographic data (elevation, slope)
- Land cover and infrastructure exposure


---

### 2. Data Preprocessing & Daily Aggregation
**Goal:** Convert hourly data into daily metrics  

- **Daily aggregations:**
  - Sum: `Total_precipitation`, `Snowmelt`
  - Mean: `2m_temperature`, `2m_dewpoint_temperature`, `RH`
  - Max/min: computed for `Tmax`/`Tmin` from hourly temps
- Use `xarray`/`pandas` to resample
- Handle missing values
- Save in `.nc` or `.pkl` formats, organized by region and variable

---

### 3. ML / DL Modeling
**Goal:** Predict flood or extreme rainfall risk  

#### 🧩 Feature Engineering
- Lagged variables (1, 3, 7, 14, 30 days)
- Rolling stats (3, 7, 14, 30 days)
- Temporal features: `dayofyear`, monsoon flag
- (Optional) Spatial features: elevation, river and lake metrics 

#### 🧠 Model Development
- Binary classification (e.g., extreme rainfall event)  
- Regression (e.g., total daily rainfall)
- **Algorithms:**
  - ML: XGBoost, RandomForest, Logistic Regression
  - DL: CNN-LSTM, Transformers
  - (Optional): GNN for spatiotemporal modeling across regions

#### ✅ Evaluation
- Train/test split by time
- Metrics:
  - Classification: Accuracy, F1-score, Confusion Matrix
  - Regression: RMSE, MAE
- Cross-validation or time series split
- Visualizations: prediction vs actual plots

---

### 4. Deployment (Next step)
**Goal:** Build a usable predictive tool  

- Options:
  - Backend: Flask / FastAPI
  - Frontend: Streamlit / Gradio interface
  - Daily scheduled inference
- Stretch goals:
  - Interactive dashboard (Plotly, Dash)
  - Risk alerts for high-probability days

---


## 📁 Repository Structure

- **`code/`** – Python scripts and notebooks for data processing and analysis  
- **`data/`** – Raw meteorological data files
- **`docs/`** – Flood prediction ML workflow
- **`era5_data/`** – Hourly climate variables from ERA5, organized by variable and year
- **`processed_MET_data/`** – Cleaned and standardized MET data for each region  
- **`world_boundaries_for_bhutan_map/`** – Shapefiles and boundary data for mapping  
- **`README.md`** – Project overview and instructions  

