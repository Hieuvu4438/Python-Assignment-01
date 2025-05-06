# 🌟 Premier League Player Statistics Analysis

Welcome to the **Premier League Player Statistics Analysis** project! This Python-based repository scrapes, processes, analyzes, clusters, and predicts player statistics from the Premier League, sourced from [FBref](https://fbref.com). The project is elegantly structured into four core exercises, implemented in a Jupyter Notebook (`Python Assignment.ipynb`). Below, you'll find a visually appealing and comprehensive guide to understanding the project's purpose, functionality, and outputs.

---

## 📋 Project Overview

This project dives deep into Premier League player data, offering insights through:
- **Web Scraping**: Collecting detailed player stats from FBref.
- **Statistical Analysis**: Identifying top performers and team metrics.
- **Clustering**: Grouping players by performance using K-Means.
- **Prediction**: Forecasting player market values with Random Forest.

The project leverages powerful Python libraries like `BeautifulSoup`, `Selenium`, `Pandas`, `Scikit-learn`, `Matplotlib`, and `Seaborn` to deliver robust data processing and visualization.

### 🗂️ Notebook Structure
The Jupyter Notebook is divided into four exercises:
1. **Exercise 1**: Scrape and aggregate player stats into `results.csv`.
2. **Exercise 2**: Analyze top/bottom performers and team stats.
3. **Exercise 3**: Cluster players based on performance metrics.
4. **Exercise 4**: Predict player market values using machine learning.

---

## ⚙️ Requirements

To run this project, install the following Python libraries:

```bash
pip install beautifulsoup4 selenium pandas numpy scikit-learn matplotlib seaborn
```

### Additional Setup:
- **Selenium WebDriver**: Install a Chrome WebDriver compatible with your browser version.
- **Jupyter Notebook**: Required to run `Python Assignment.ipynb`.

---

## 🔍 Exercise Breakdown

### 🕸️ Exercise 1: Web Scraping & Data Aggregation
**Goal**: Scrape player statistics from FBref and compile them into a structured `results.csv`.

- **Data Sources**: Includes standard stats, goalkeeping, shooting, passing, goal creation, defensive actions, possession, and more.
- **Process**:
  - **Scraping**: Uses `Selenium` for dynamic content and `BeautifulSoup` for HTML parsing.
  - **Filtering**: Includes players with ≥1.0 "90s" (90 minutes played) and goalkeepers for relevant stats.
  - **Merging**: Combines dataframes based on `player`, `team`, and `position`.
  - **Formatting**: Adds a `No.` column, sorts by player name, and organizes columns into a multi-index structure (e.g., "Performance", "Expected").
  - **Handling Missing Data**: Replaces `NaN` with "N/A".
- **Output**: `results.csv` with a clean, comprehensive dataset.
- **Highlights**:
  - Modular scraping functions (`create_attributes`, `extract_data`, `scrape_table`).
  - Custom extractors for fields like nationality and birth year.

### 📊 Exercise 2: Statistical Analysis
**Goal**: Identify top/bottom performers and compute team/player statistics, saving results to `top_3.txt` and `results2.csv`.

#### Part 1: Top/Bottom Performers
- **Task**: Find the top 3 and bottom 3 players for each numeric statistic.
- **Process**:
  - Converts columns to numeric, filling missing values with 0.
  - Sorts and saves results to `top_3.txt` (e.g., "Statistic: goals\nTop 3:\n1. Player A (10)\n...").
- **Output**: `top_3.txt`.

#### Part 2: Team & Player Stats
- **Task**: Calculate median, mean, and standard deviation for all stats, overall and per team.
- **Process**:
  - Processes numeric columns and organizes results in a multi-index dataframe.
- **Output**: `results2.csv`.
- **Highlights**:
  - Efficient `Pandas` operations for stats computation.
  - Clear, structured text output in `top_3.txt`.

### 🧩 Exercise 3: Player Clustering
**Goal**: Group players into clusters based on performance metrics using K-Means.

- **Data Prep**:
  - Selects key metrics (e.g., `goals_per90`, `passes_pct`, `tackles`, `touches_att_3rd`).
  - Standardizes features with `StandardScaler`.
- **Clustering**:
  - Uses K-Means with 4 clusters (optimized via elbow method).
  - Tests 1–10 clusters to plot inertia and confirm the optimal number.
- **Visualization**:
  - Reduces features to 2D using PCA.
  - Creates a two-panel plot:
    - **Left**: Elbow plot (inertia vs. clusters).
    - **Right**: Scatter plot of players in PCA space, colored by cluster.
  - Saves as `player_clustering.png` (300 DPI).
- **Output**:
  - `clustered_players.csv`: Player details with cluster labels.
  - `player_clustering.png`: Visual representation of clusters.
- **Highlights**:
  - Robust feature selection for attacking, passing, defending, and possession.
  - Professional visualizations with `Seaborn` and `Matplotlib`.

### 💸 Exercise 4: Market Value Prediction
**Goal**: Predict player market values using a Random Forest model.

- **Data Prep**:
  - Converts `price` (e.g., "€10M") to numeric values.
  - Encodes categorical variables (`nationality`, `team`, `position`) with `LabelEncoder`.
  - Fills missing values with column medians.
- **Modeling**:
  - Uses `RandomForestRegressor` (`n_estimators=100`, `max_depth=15`).
  - Splits data (80% train, 20% test).
  - Evaluates with MSE and R².
- **Visualization**:
  - Scatter plot of actual vs. predicted prices, with a diagonal reference line.
  - Saves as `actual_vs_predicted.png`.
- **Feature Importance**: Identifies key predictors of market value.
- **Highlights**:
  - Robust price parsing.
  - Clear model evaluation visualizations.

---

## 📁 Output Files
| File                     | Description                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| `results.csv`            | Comprehensive player stats with multi-index columns.                        |
| `top_3.txt`              | Top/bottom 3 players for each statistic.                                   |
| `results2.csv`           | Median, mean, and standard deviation for stats (overall and per team).     |
| `clustered_players.csv`  | Player details with cluster labels and selected features.                   |
| `player_clustering.png`  | Elbow plot and PCA scatter plot of player clusters.                        |
| `actual_vs_predicted.png`| Actual vs. predicted market values scatter plot.                           |

---

## 🚀 Usage

1. **Setup**:
   - Install dependencies and Chrome WebDriver.
   - Set up a Jupyter Notebook environment.
2. **Run**:
   - Open and execute `Python Assignment.ipynb`.
   - Ensure internet access for scraping FBref.
3. **Notes**:
   - Exercise 4 requires a `price` column; merge with a market value dataset if needed.
   - Adjust `optimal_k` in Exercise 3 for different clustering insights.
   - Verify FBref table classes/URLs if scraping fails.

---

## 🌈 Future Improvements
- 🛡️ Add robust error handling for web scraping.
- 📈 Incorporate additional data sources for market values.
- 🔍 Explore advanced clustering (e.g., silhouette scores, DBSCAN).
- 📊 Enhance visualizations (e.g., feature importance plots, team comparisons).
- ⚡ Optimize Random Forest with hyperparameter tuning.

---

## 📜 License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

**Happy analyzing!** ⚽️