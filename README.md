# Data Cleaning and Visualization Project

This project cleans an employee dataset with pandas, removes exact duplicates, imputes missing numeric values with medians, converts dates, removes salary outliers using the IQR method, one-hot encodes departments, exports `cleaned_data.csv`, and creates four visualizations.

## Files

- `sample_data_cleaning_project - Sample_data_cleaning_project.csv` — raw input data
- `cleaningdata_final_submission_tested.ipynb` — executable cleaning and visualization notebook
- `cleaned_data.csv` — cleaned dataset example/output

## Run

```bash
pip install -r requirements.txt
jupyter notebook cleaningdata_final_submission_tested.ipynb
```
