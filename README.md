# 🌍 Cocoa Yield Prediction – Ghana (2000–2023)

## 📌 Project Overview
This project develops a **cocoa yield prediction model for Ghana (2000–2023)** by integrating  
**FAOSTAT yield data** with seasonal **satellite and climate indicators**:

- 🌧️ **CHIRPS Rainfall** (May–Aug, flowering & pod set)  
- 🌡️ **ERA5-Land Temperature** (May–Aug, heat stress)  
- 🌱 **MODIS NDVI** (Aug–Oct, pod filling canopy vigor)  

Features are aggregated according to cocoa phenology and joined with yearly FAOSTAT yield statistics.  
A **Random Forest regression** model was trained and validated using a **time-based split**:

- **Train:** 2000–2018  
- **Test:** 2019–2023  

---

## ⚙️ Methodology

1. **Labels (FAOSTAT)**  
   - Download production (tonnes) & harvested area (ha).  
   - Compute yield = Production / Area.  

2. **Seasonal Predictors**  
   - Aggregate CHIRPS rainfall (May–Aug sum).  
   - Aggregate ERA5 temperature (May–Aug mean, °C).  
   - Aggregate MODIS NDVI (Aug–Oct mean, scaled 0–1).  

3. **Preprocessing**  
   - Reduce to national averages for Ghana.  
   - Join yearly features with yield labels.  

4. **Model Training & Validation**  
   - Train Random Forest regression (500 trees).  
   - Evaluate on test years (2019–2023).  

---

## 📊 Results

- **R² (Test):** ~0.62  
- **RMSE / MAE:** Reasonable error margins on test years.  
- **Directional Hit-Rate:** Correctly predicted yield trend (up/down) in most years.  
- **Feature Importance:** Rainfall > NDVI > Temperature.  

**Charts produced:**  
- Time series: Observed vs Predicted yield (2019–2023).  
- Scatter plot: Observed vs Predicted yields with regression line.  

---

## 🚀 How to Run

### A) Run in Google Earth Engine (recommended)
1. Upload FAOSTAT Ghana cocoa CSV as a **Table asset**.  
2. Open `ghana_cocoa_yield_gee.js` in [GEE Code Editor](https://code.earthengine.google.com).  
3. Replace `FAOSTAT_ASSET` with your asset ID.  
4. Click **Run** → view metrics & charts in Console.  
5. In **Tasks**, export predictions CSV to Google Drive.  

### B) Optional: Python Post-Processing
- Place exported CSV in `data/`.  
- Install requirements:  
  ```bash
  pip install -r requirements.txt
  python python/train_from_export.py --csv data/ghana_predictions_RF_TEST_2019_2023.csv
