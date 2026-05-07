# Exploring-NYC-school-SAT-scores-
This project analyzes SAT performance data from NYC schools using Python and Pandas.
# NYC Schools SAT Analysis

A Python data analysis project exploring SAT performance across NYC public schools using Pandas.

---

# Project Description

This project analyzes SAT score data from NYC schools to:

- Identify top-performing math schools
- Calculate total SAT scores
- Find the top 10 schools overall
- Analyze SAT score variation by borough

The project demonstrates practical data analysis techniques using Python and Pandas.

---

# Dataset

Dataset used:

```bash
schools.csv
```

Dataset columns include:

- school_name
- borough
- average_math
- average_reading
- average_writing

---

# Technologies Used

- Python
- Pandas

---

# Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/nyc-schools-sat-analysis.git
```

Move into the project directory:

```bash
cd nyc-schools-sat-analysis
```

Install required libraries:

```bash
pip install -r requirements.txt
```

---

# requirements.txt

```txt
pandas
```

---

# Project Structure

```bash
NYC-Schools-SAT-Analysis/
│
├── schools.csv
├── analysis.py
├── requirements.txt
├── info.txt
└── README.md
```

---

# Full Code

```python
# Import pandas
import pandas as pd

# Read in the dataset
schools = pd.read_csv("schools.csv")

# Preview dataset
print(schools.head())

# ---------------------------------------------------
# Finding Best Math Schools
# ---------------------------------------------------

# Set threshold at 80% of maximum SAT math score
threshold = 0.8 * 800

# Filter schools with high math scores
best_math_schools = schools[
    schools["average_math"] >= threshold
][["school_name", "average_math"]].sort_values(
    by="average_math",
    ascending=False
)

print("\nBest Math Schools:\n")
print(best_math_schools)

# ---------------------------------------------------
# Creating Total SAT Score
# ---------------------------------------------------

# Add total SAT column
schools = schools.assign(
    total_SAT =
    schools["average_math"] +
    schools["average_reading"] +
    schools["average_writing"]
)

# ---------------------------------------------------
# Top 10 Schools by SAT Score
# ---------------------------------------------------

top_10_schools = (
    schools.loc[:, ["school_name", "total_SAT"]]
           .sort_values(by="total_SAT", ascending=False)
           .head(10)
           .reset_index(drop=True)
)

print("\nTop 10 Schools by Total SAT:\n")
print(top_10_schools)

# ---------------------------------------------------
# Borough Statistics
# ---------------------------------------------------

borough_stats = schools.groupby("borough").agg(
    num_schools=("school_name", "count"),
    average_SAT=("total_SAT", "mean"),
    std_SAT=("total_SAT", "std")
).round(2)

print("\nBorough Statistics:\n")
print(borough_stats)

# ---------------------------------------------------
# Borough with Highest SAT Variability
# ---------------------------------------------------

largest_std_dev = borough_stats.sort_values(
    "std_SAT",
    ascending=False
).head(1).reset_index()

print("\nBorough with Highest Standard Deviation:\n")
print(largest_std_dev)
```

---

# Example Output

## Best Math Schools

| School Name | Average Math |
|---|---|
| Stuyvesant High School | 754 |
| Bronx High School of Science | 714 |
| Staten Island Technical High School | 711 |

---

## Top 10 Schools by SAT

| School Name | Total SAT |
|---|---|
| Stuyvesant High School | 2144 |
| Bronx High School of Science | 2041 |

---

## Borough Statistics

| Borough | Num Schools | Average SAT | Std SAT |
|---|---|---|---|
| Manhattan | 89 | 1340.13 | 230.29 |

---

# Key Concepts Used

This project demonstrates:

- Data filtering
- Sorting
- Aggregation
- GroupBy operations
- Feature engineering
- Statistical analysis
- DataFrame manipulation

---

# Future Improvements

Possible future additions:

- Data visualizations
- Interactive dashboards
- Correlation analysis
- Machine learning models
- Borough comparison charts

---

# Author

TechnoBear  
