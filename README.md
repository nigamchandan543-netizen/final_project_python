# Air Quality Analysis – Python Data Analysis Project

## 📌 Project Overview

This project performs **Air Quality Data Analysis** using Python, Pandas, NumPy, Matplotlib, and Seaborn.

The project uses the **UCI Air Quality Dataset** to analyze air pollution levels, particularly **Carbon Monoxide (CO)**, along with temperature and humidity. The dataset is cleaned, transformed, analyzed, and visualized to identify useful patterns and relationships.

---

## 🎯 Objectives

The main objectives of this project are:

* Load and inspect the Air Quality dataset.
* Handle missing values correctly.
* Replace the UCI dataset's `-200` missing-value indicator with `NaN`.
* Remove columns with excessive missing values.
* Fill remaining numerical missing values using the median.
* Create useful DateTime-based features.
* Analyze CO concentration.
* Study CO levels across different months and hours.
* Analyze the relationship between temperature and CO.
* Generate meaningful visualizations.
* Display important statistical insights.

---

## 🛠️ Technologies Used

| Technology | Purpose                              |
| ---------- | ------------------------------------ |
| Python     | Programming language                 |
| Pandas     | Data loading, cleaning, and analysis |
| NumPy      | Numerical operations                 |
| Matplotlib | Data visualization                   |
| Seaborn    | Statistical visualization            |
| Warnings   | Suppress unnecessary warnings        |

---

## 📂 Project Structure

```text
Air-Quality-Analysis/
│
├── AirQualityUCI.csv
├── air_quality_analysis.py
└── README.md
```

---

## 📊 Dataset

This project uses the **Air Quality UCI Dataset**.

The dataset contains measurements related to air pollutants and environmental conditions, including:

* CO – Carbon Monoxide
* C6H6 – Benzene
* NOx – Nitrogen Oxides
* NO2 – Nitrogen Dioxide
* T – Temperature
* RH – Relative Humidity
* AH – Absolute Humidity

The dataset uses `;` as the column separator.

Therefore, the dataset is loaded using:

```python
df = pd.read_csv("AirQualityUCI.csv", sep=';')
```

---

## 🧹 Data Cleaning

### 1. Checking Missing Values

The project first checks the number of missing values:

```python
df.isnull().sum()
```

### 2. Replacing `-200`

The UCI dataset represents missing measurements using `-200`.

These values are replaced with `NaN`:

```python
df.replace(-200, np.nan, inplace=True)
```

### 3. Removing Excessively Missing Columns

The `NMHC(GT)` column is removed because it contains a large number of missing values:

```python
df.drop(columns=['NMHC(GT)'], inplace=True, errors='ignore')
```

### 4. Filling Missing Values

Remaining numerical missing values are replaced with their median:

```python
numeric_cols = df.select_dtypes(include=[np.number]).columns
df[numeric_cols] = df[numeric_cols].fillna(
    df[numeric_cols].median()
)
```

---

## 🕒 DateTime Feature Engineering

The separate `Date` and `Time` columns are combined into a single DateTime column:

```python
df['DateTime'] = pd.to_datetime(
    df['Date'] + ' ' + df['Time'],
    dayfirst=True,
    errors='coerce'
)
```

Two additional features are created:

### Month

```python
df['Month'] = df['DateTime'].dt.month
```

### Hour

```python
df['Hour'] = df['DateTime'].dt.hour
```

These features make it possible to analyze air quality according to **month** and **time of day**.

---

## 📈 Visualizations

The project generates six main visualizations.

### 1. Correlation Heatmap

Shows correlations between numerical variables.

```python
sns.heatmap(corr, annot=True, cmap="coolwarm")
```

This helps identify relationships between pollutants and environmental measurements.

---

### 2. CO Distribution

A histogram is used to understand the distribution of CO measurements.

```python
sns.histplot(df['CO(GT)'], bins=30, kde=True)
```

It shows how frequently different CO concentration levels occur.

---

### 3. CO Levels Over Time

A line chart displays changes in CO concentration over the recorded period.

```python
plt.plot(df['DateTime'], df['CO(GT)'])
```

This can help identify trends and fluctuations in pollution.

---

### 4. Average CO by Month

The average CO concentration is calculated for each month:

```python
monthly = df.groupby('Month')['CO(GT)'].mean()
```

A bar chart is then used to compare the monthly averages.

---

### 5. CO Levels by Hour

A boxplot is used to compare CO levels during different hours of the day.

```python
sns.boxplot(
    x='Hour',
    y='CO(GT)',
    data=df
)
```

This can reveal whether CO concentration varies according to time of day.

---

### 6. Temperature vs CO

A scatter plot shows the relationship between temperature and CO:

```python
sns.scatterplot(
    x='T',
    y='CO(GT)',
    data=df
)
```

This helps investigate whether temperature and CO concentration have any observable relationship.

---

## 🔍 Key Insights

At the end of the program, important statistics are displayed:

```python
print(f"Average CO Level       : {df['CO(GT)'].mean():.2f}")
print(f"Maximum CO Level       : {df['CO(GT)'].max():.2f}")
print(f"Minimum CO Level       : {df['CO(GT)'].min():.2f}")
print(f"Average Temperature    : {df['T'].mean():.2f} °C")
print(f"Average Humidity       : {df['RH'].mean():.2f} %")
```

The program reports:

* Average CO level
* Maximum CO level
* Minimum CO level
* Average temperature
* Average humidity

---

## ▶️ How to Run the Project

### Step 1: Install Python

Make sure Python is installed on your computer.

Check the installation:

```bash
python --version
```

### Step 2: Install Required Libraries

Run:

```bash
pip install pandas numpy matplotlib seaborn
```

### Step 3: Place the Dataset

Keep `AirQualityUCI.csv` in the same folder as your Python program.

### Step 4: Run the Program

```bash
python air_quality_analysis.py
```

If you are using Jupyter Notebook, run the cells individually.

---

## ⚠️ Important Note

The dataset must be loaded with:

```python
sep=';'
```

because the original UCI Air Quality dataset uses a semicolon (`;`) as the separator.

Using the default comma separator may cause the dataset to be loaded incorrectly.

---

## 📋 Analysis Workflow

```text
Load Dataset
     ↓
Inspect Dataset
     ↓
Check Missing Values
     ↓
Replace -200 with NaN
     ↓
Remove Excessively Missing Columns
     ↓
Fill Missing Numerical Values
     ↓
Create DateTime Features
     ↓
Analyze CO Levels
     ↓
Generate Visualizations
     ↓
Display Key Insights
```

---

## 💡 Learning Outcomes

By completing this project, you can practice:

* Reading CSV files with Pandas
* Understanding DataFrames
* Checking dataset structure
* Handling missing data
* Using `NaN`
* Selecting numerical columns
* Using median imputation
* Working with DateTime data
* Grouping data using `groupby()`
* Calculating statistics
* Creating charts with Matplotlib
* Creating statistical plots with Seaborn
* Understanding correlation
* Performing basic exploratory data analysis (EDA)

---

## 🚀 Possible Future Improvements

The project can be extended by adding:

* AQI (Air Quality Index) calculation
* Prediction of CO levels using Machine Learning
* Interactive dashboards using Plotly
* Year/month/day analysis
* Comparison of multiple pollutants
* Outlier detection
* Regression analysis
* Exporting cleaned data to a new CSV file
* Interactive filters and dashboards

---

## 👨‍💻 Project Type

**Python Data Analysis / Exploratory Data Analysis (EDA)**

---

## 📄 License

This project is intended for **educational and learning purposes**.
