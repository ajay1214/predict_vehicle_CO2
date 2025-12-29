# 🚗 CO₂ Emission Predictor

A machine learning–powered web application that predicts **vehicle CO₂ emissions (g/km)** using vehicle specifications and fuel consumption data. This repository contains a minimal, production-ready Streamlit app that loads a serialized scikit-learn pipeline for inference.

> Predict vehicle carbon dioxide emissions from common vehicle features in a transparent and reproducible way — outputs are scientific (g/km) with no fabricated indicators.

---

## 🔍 Project Summary

This project implements a full ML workflow: data preprocessing, model training, pipeline serialization, and deployment via a Streamlit web UI. It accepts vehicle inputs (engine size, cylinders, transmission, fuel consumption, etc.) and returns an estimated CO₂ emission value in grams per kilometer.

The repository focuses on correctness, clear engineering practices (pipeline-driven preprocessing), and an easy local deployment path.

---

## 📊 Dataset (description)

The model is trained on a real-world vehicle dataset containing both numerical and categorical fields. Typical columns include:

- `Make` (vehicle manufacturer)
- `Vehicle Class` (COMPACT, SUV-SMALL, TWO-SEATER, FULL-SIZE, etc.)
- `Engine Size (L)`
- `Cylinders` (count)
- `Transmission` (manual/automatic variants)
- `Fuel Type`
- `Fuel Consumption City (L/100 km)`
- `Fuel Consumption Highway (L/100 km)`
- `Fuel Consumption Combined (L/100 km)`
- `CO2 Emissions (g/km)` — target

> Note: This README does not include the raw dataset for licensing reasons. Add or document your dataset file under `data/` if you include it.

---

## ⚙️ Methodology

The modelling pipeline follows a standard supervised regression approach:

1. **Preprocessing**
   - Categorical encoding (e.g., OneHot or Ordinal depending on the feature)
   - Numeric scaling (StandardScaler or similar)
   - Feature engineering (e.g., converting combined fuel consumption from L/100 km to MPG if needed)
2. **Modeling**
   - Train a regression model (classical scikit-learn estimator)
   - Evaluate using RMSE / MAE and cross-validation
3. **Packaging**
   - Wrap preprocessing + estimator inside a single `Pipeline`
   - Serialize the pipeline using `joblib` (saved as `co2_pipeline.pkl`)
4. **Deployment**
   - Streamlit app loads the serialized pipeline and exposes a compact input form for inference

This approach guarantees identical transforms during training and inference.

---

## 🖥️ Web App (Streamlit)

`app.py` contains the Streamlit interface. Key behaviors:

- Structured input form for vehicle features
- Uses Streamlit session state to keep inputs persistent across reruns
- Loads `co2_pipeline.pkl` and returns a prediction on-demand
- Minimal dark-themed UI (embedded HTML/CSS)

### Run locally

```bash
# clone
git clone https://github.com/ajay1214/predict_vehicle_CO2.git
cd predict_vehicle_CO2

# create venv (recommended)
python -m venv .venv
# windows: .venv\Scripts\activate
# linux/mac: source .venv/bin/activate

pip install -r requirements.txt

# run the app
streamlit run app.py
```

Open the URL printed by Streamlit (usually `http://localhost:8501`).

---

## 📁 Repository structure

```
predict_vehicle_CO2/
├── app.py                  # Streamlit app (inference UI)
├── co2_pipeline.pkl        # Serialized preprocessing + trained model
├── requirements.txt        # Python dependencies
├── README.md               # This file
├── .gitignore
```

---
## 👤 Contact

Made with ❤️ by Ajay Bind

- GitHub: `https://github.com/ajay1214`

---

