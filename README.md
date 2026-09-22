# Data Cleaning and Visualization Project

This repository now follows the workflow and chart code from the linked Google Colab notebook `cleaningdata_final_submission_tested.ipynb`.

## Dataset

- **Input:** `sample_data_cleaning_project - Sample_data_cleaning_project.csv`
- **Output:** `cleaned_data.csv`
- **Libraries:** pandas and Matplotlib
- **Raw data:** 43 rows and 5 columns
- **Colab cleaning result:** 36 rows and 7 columns

## Cleaning procedure

### Step 1: Load the dataset

The notebook checks that the raw CSV exists, loads it with pandas, rejects an empty file, and prints the row count, column count, and first five records.

### Step 2: Identify missing values

`data.isnull().sum()` reports missing values for every column and the total number of missing cells. In the Colab run, there are 4 missing ages and 7 missing salaries, for 11 missing values total.

### Step 3: Clean text and handle missing values

Text fields are stripped of accidental spaces, names and departments are title-cased, and age and salary are converted to numeric values. Missing ages and salaries are replaced with their medians. Joining dates are parsed with `pd.to_datetime`; invalid dates are removed because they cannot be inferred reliably.

### Step 4: Remove duplicate rows

Only exact duplicate records are removed. The Colab run removes 1 exact duplicate and keeps different records even when they share a name or age.

### Step 5: Remove salary outliers

The notebook calculates Q1, Q3, and the interquartile range. Salaries outside `Q1 - 1.5 × IQR` and `Q3 + 1.5 × IQR` are removed. The Colab output reports Q1 = 68,500, Q3 = 77,421, IQR = 8,921, bounds of 55,118.50 and 90,802.50, and 6 salary outliers removed.

### Step 6: Convert data types

Age is rounded and stored as an integer, salary is stored as a float, and `Join_Date` is stored as a pandas datetime.

### Step 7: Encode departments

`pd.get_dummies(..., drop_first=False)` creates one column for every department: `Department_Finance`, `Department_Hr`, and `Department_It`. Keeping all categories makes every department visible in the exported file and charts.

### Step 8: Validate the output

The notebook confirms that the result is not empty, contains no missing values, and contains no duplicate rows. The Colab output validates a final shape of **(36, 7)**.

### Step 9: Save the cleaned dataset

The validated dataframe is saved to `cleaned_data.csv` and the notebook checks that the file exists.

### Step 10: Load data for visualization

The saved CSV is loaded again so every chart is based on exactly the exported cleaned dataset, rather than an earlier intermediate dataframe.

## Visualizations from the Colab notebook

### 1. Department Distribution

The notebook sums each one-hot department column and plots the totals as a bar chart. This compares employee counts across Finance, HR, and IT.

![Department distribution](visualizations/department_distribution.svg)

### 2. Salary Distribution

The histogram uses ten salary bins to show how frequently salary values occur after missing-value treatment and outlier removal.

![Salary distribution](visualizations/salary_distribution.svg)

### 3. Salary vs. Age

The Colab notebook uses a connected line plot with age on the x-axis and salary on the y-axis. The markers show individual cleaned records; because the data is not ordered as a time series, this is an exploratory view rather than a trend estimate.

![Salary versus age](visualizations/salary_vs_age.svg)

### 4. Salary vs. Age by Department

The final chart uses the one-hot department columns as masks. Each department is plotted as a separate scatter series, with salary on the x-axis and age on the y-axis, making department groups easier to compare.

![Salary versus age by department](visualizations/salary_vs_age_by_department.svg)

The SVG previews are committed for README display. Running all notebook cells also creates matching PNG files in `visualizations/`.

## Run the project

```bash
pip install -r requirements.txt
jupyter notebook cleaningdata_final_submission_tested.ipynb
```

Run the notebook from the repository root so it can find the input CSV and save the output charts.
