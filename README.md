# Countries Data Analysis

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![pandas](https://img.shields.io/badge/pandas-data%20analysis-150458)
![License](https://img.shields.io/badge/License-MIT-green)

A beginner-friendly data analysis project that explores a world countries dataset using **Python**, **pandas** and **NumPy**. The notebook answers basic questions about population, democracy scores, regions and political leaders.

---

## Table of Contents

1. [Dataset](#dataset)
2. [Objectives](#objectives)
3. [Project Structure](#project-structure)
4. [Installation and Setup](#installation-and-setup)
5. [How to Run](#how-to-run)
6. [Methodology](#methodology)
7. [Key Findings](#key-findings)
8. [Sample Code](#sample-code)
9. [Limitations and Future Work](#limitations-and-future-work)
10. [License](#license)
11. [Author](#author)

---

## Dataset

- **File:** `Countries.csv`
- **Size:** 194 rows (countries) and 64 columns

### Key columns used

| Column | Description |
|---|---|
| `country` | Country name |
| `country_long` | Official long name of the country |
| `capital_city` | Capital city |
| `region` | Geographic region (22 unique regions) |
| `continent` | Continent |
| `population` | Total population |
| `rural_population` / `urban_population` | Rural and urban population counts |
| `democracy_score` | Democracy index score |
| `democracy_type` | Category such as "Flawed democracy" |
| `political_leader` | Name of the current political leader |
| `title` | Leader's title (e.g. Prime Minister) |
| `currency` | National currency |
| `median_age` | Median age of the population |
| `women_parliament_seats_pct` | Percentage of parliament seats held by women |
| `press` | Press freedom related score |
| `latitude` / `longitude` | Geographic coordinates |

The dataset has 64 columns in total; the table lists only the ones used or visible in the notebook.

---

## Objectives

The notebook answers these questions:

1. Which country has the highest population, and what is its capital?
2. Which country has the lowest population?
3. Which are the top 5 countries by democracy score?
4. How many regions are in the dataset?
5. How many countries lie in Eastern Europe?
6. Who is the political leader of the second most populous country?
7. Which countries have no political leader listed (missing values)?

---

## Project Structure

```
countries-analysis/
├── country.ipynb       # Main analysis notebook
├── Countries.csv       # Dataset
└── README.md           # Project documentation
```

---

## Installation and Setup

**Prerequisites:** Python 3.8 or higher.

1. Clone or download this repository:
   ```bash
   git clone [add repository URL]
   cd countries-analysis
   ```

2. (Optional) Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate      # On Windows: venv\Scripts\activate
   ```

3. Install the dependencies:
   ```bash
   pip install -r requirements.txt
   ```

---

## How to Run

1. Place `Countries.csv` in the same folder as the notebook.
2. Launch Jupyter:
   ```bash
   jupyter notebook
   ```
3. Open `country.ipynb`.
4. **Update the file path.** The notebook reads the CSV from `'/Countries.csv'`, which works only in the original environment. Change it to a relative path:
   ```python
   df = pd.read_csv('Countries.csv')
   ```
5. Run all cells (**Kernel → Restart & Run All**).

---

## Methodology

1. **Load:** read the CSV into a pandas DataFrame with `read_csv`.
2. **Inspect:** preview the data with `head()` and select columns of interest.
3. **Filter:** use boolean masks to find rows matching a condition (e.g. maximum or minimum population).
4. **Sort:** order rows with `sort_values` and pick the top results with `nlargest`.
5. **Count:** use `value_counts` to count regions and countries per region.
6. **Check missing values:** use `isna()` to find countries with no political leader.

**pandas functions used:** `read_csv`, `head`, column selection, boolean filtering, `max`, `min`, `sort_values`, `value_counts`, `nlargest`, `isna`

---

## Key Findings

| # | Question | Answer |
|---|---|---|
| 1 | Country with the highest population | **India** (1,417,173,173), capital **New Delhi** |
| 2 | Country with the lowest population | **Tuvalu** (11,312) |
| 3 | Top 5 countries by democracy score | **Norway, Iceland, Sweden, New Zealand, Denmark** |
| 4 | Number of regions | **22** |
| 5 | Countries in Eastern Europe | **10** |
| 6 | Leader of the second most populous country | **Xi Jinping** (China) |
| 7 | Countries with no political leader listed | Cabo Verde, Timor-Leste, Slovak Republic, West Bank and Gaza, St. Vincent and the Grenadines, St. Kitts and Nevis, St. Lucia |

---

## Sample Code

**Country with the highest population and its capital**
```python
z = df[df['population'] == df['population'].max()]
z[['country', 'capital_city']]
```

**Top 5 countries by democracy score**
```python
df.sort_values(by='democracy_score', ascending=False).head()
```

**Leader of the second most populous country**
```python
df[df['population'] == df['population'].nlargest(2).iloc[1]][['country', 'political_leader']]
```

**Countries with missing political leader**
```python
df[df['political_leader'].isna()]['country']
```

---

## Limitations and Future Work

- The analysis is descriptive only and covers a small set of questions.
- Some countries have no `political_leader` value, and some have a `democracy_score` of 0 with type "Unknown" (for example Tuvalu), so these scores should be interpreted with care.
- The dataset is a snapshot, so values such as population and leaders may be out of date.
- **Ideas for improvement:**
  - Add visualizations with `matplotlib` or `seaborn` (population by continent, democracy score distribution)
  - Explore correlations between `democracy_score` and other columns such as `median_age` or `women_parliament_seats_pct`
  - Compare regions and continents with `groupby`
  - Handle missing values more systematically

---

## License

This project is licensed under the MIT License. See the `LICENSE` file for details. 

---
