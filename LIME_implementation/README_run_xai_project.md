# Run guide

## 1) Install

```bash
pip install -r requirements_xai_project.txt
```

## 2) Put the notebook into the project root

Recommended location:

- `final_telematics_lime_project.ipynb`

The notebook saves everything to `outputs_final/`.

## 3) Fill only 3 TODO paths in the first config cell

- `WEEK_FILES_GLOB`
- `STATIC_PHEV_EV_XLSX`
- `STATIC_ICE_HEV_XLSX`

Example idea:

```python
WEEK_FILES_GLOB = r"D:/VED/VED_DynamicData_Part*/VED_*_week.csv"
STATIC_PHEV_EV_XLSX = Path(r"D:/VED/VED_Static_Data_PHEV_EV.xlsx")
STATIC_ICE_HEV_XLSX = Path(r"D:/VED/VED_Static_Data_ICE_HEV.xlsx")
```

## 4) Run top to bottom

The first full run:

1. builds the raw trip table,
2. tunes XGBoost,
3. trains the final model,
4. scores all trips,
5. detects anomalies,
6. tunes manual LIME,
7. saves 3–5 explanations.

## 5) Outputs

Main files:

- `outputs_final/cache/trip_table_raw.csv.gz`
- `outputs_final/cache/trip_table_scored.csv.gz`
- `outputs_final/models/xgb_energy_artifact.joblib`
- `outputs_final/lime_explanations/`

## Notes

- The notebook does not use ready-made XAI libraries.
- LIME is implemented manually in the notebook.
- The notebook explains trips in the **raw feature space**, then converts perturbations to the XGBoost design matrix.
- This fixes the main issue in the old pipeline where residuals were saved without the raw feature row needed for LIME.
