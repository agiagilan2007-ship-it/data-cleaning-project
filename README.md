# Data Cleaning and Visualization Project

This project now follows the Google Colab notebook workflow and visualization code exactly in structure and chart formatting.

## Step-by-step cleaning procedure

1. **Load the dataset:** verify the input CSV exists, load it with pandas, reject an empty dataset, and display its shape and first five rows.
2. **Identify missing values:** count nulls in every column and report the total. The raw file contains 43 rows, 5 columns, and 11 missing cells.
3. **Clean text and handle missing values:** strip text whitespace, title-case `Name` and `Department`, convert `Age` and `Salary` to numeric values, fill missing numeric values with medians, parse `Join_Date`, and remove invalid dates.
4. **Remove duplicates:** remove only exact duplicate records. One duplicate is removed.
5. **Handle salary outliers:** calculate Q1, Q3, IQR, and the 1.5-IQR bounds. Six extreme salary records are removed.
6. **Convert data types:** store age as rounded integers, salary as floats, and joining dates as datetimes.
7. **Encode categories:** use `pd.get_dummies` with `drop_first=False`, producing `Department_Finance`, `Department_Hr`, and `Department_It`.
8. **Validate:** confirm the cleaned output is non-empty, has no missing values, and has no duplicate rows. The final shape is 36 rows × 7 columns.
9. **Save:** write the cleaned dataframe to `cleaned_data.csv`.
10. **Visualize:** reload the saved CSV and generate the four charts below.

## Colab visualizations

### 1. Department Distribution

The code sums all one-hot encoded department columns and uses `department_counts.plot(kind="bar")` with an 8 × 6 figure. The SVG preview uses Matplotlib's default blue bar styling.

![Department Distribution](visualizations/department_distribution.svg)

### 2. Salary Distribution

The notebook calls `plt.hist(cleaned_data["Salary"], bins=10, edgecolor="black")`. The chart shows salary frequency after median imputation and IQR filtering.

![Salary Distribution](visualizations/salary_distribution.svg)

### 3. Salary vs. Age

The notebook uses `plt.plot(cleaned_data["Age"], cleaned_data["Salary"], marker="o", linestyle="-")`. This is a connected record-order plot, not a regression line.

![Salary vs. Age](visualizations/salary_vs_age.svg)

### 4. Salary vs. Age by Department

The notebook loops through each `Department_` column, masks rows where the value equals 1, and calls `plt.scatter(cleaned_data.loc[mask, "Salary"], cleaned_data.loc[mask, "Age"])`. Finance, Hr, and It are separated by the legend.

![Salary vs. Age by Department](visualizations/salary_vs_age_by_department.svg)

The notebook saves equivalent PNG files in `visualizations/` when run.

## Run

```bash
pip install -r requirements.txt
jupyter notebook cleaningdata_final_submission_tested.ipynb
```
