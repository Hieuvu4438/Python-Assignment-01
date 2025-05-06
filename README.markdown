# Premier League Player Statistics Analysis

This repository contains a Python-based project that scrapes, processes, analyzes, clusters, and predicts player statistics from the Premier League, sourced from [FBref](https://fbref.com). The project is structured into four main exercises, implemented in a Jupyter Notebook (`Python Assignment.ipynb`). Below is a detailed description of each component to help users understand the purpose and functionality of the code.

## Project Overview

The project focuses on collecting comprehensive player statistics from the Premier League, performing statistical analysis, clustering players based on performance metrics, and predicting player market values. It leverages web scraping, data processing, clustering, and machine learning techniques using Python libraries such as `BeautifulSoup`, `Selenium`, `Pandas`, `Scikit-learn`, `Matplotlib`, and `Seaborn`.

The notebook is divided into four exercises:
1. **Exercise 1**: Web scraping and data aggregation into a structured CSV file.
2. **Exercise 2**: Statistical analysis (top/bottom performers and team/player statistics).
3. **Exercise 3**: Clustering players based on performance metrics using K-Means.
4. **Exercise 4**: Predicting player market values using Random Forest.

## Requirements

To run the code, install the required Python libraries:

```bash
pip install beautifulsoup4 selenium pandas numpy scikit-learn matplotlib seaborn
```

Additionally, you need:
- **Selenium WebDriver**: A Chrome WebDriver compatible with your browser version.
- **Jupyter Notebook**: To execute the `.ipynb` file.

## Exercise Descriptions

### Exercise 1: Web Scraping and Data Aggregation

**Objective**: Scrape player statistics from multiple tables on FBref and merge them into a single dataset, saved as `results.csv`.

**Key Components**:
- **Data Sources**: Scrapes data from FBref pages covering standard stats, goalkeeping, shooting, passing, goal creation, defensive actions, possession, and miscellaneous stats.
- **Web Scraping**:
  - Uses `Selenium` to load dynamic content and `BeautifulSoup` to parse HTML tables.
  - Filters players with at least 1.0 "90s" (90 minutes played) and goalkeepers for relevant tables.
  - Custom attribute extraction handles specific data formats (e.g., nationality, birth year).
- **Data Processing**:
  - Merges dataframes on `player`, `team`, and `position` columns.
  - Adds a `No.` column for indexing and sorts by player name.
  - Handles missing values by replacing `NaN` with "N/A".
  - Organizes columns into a multi-index structure for clarity (e.g., "Performance", "Expected", "Goalkeeping").
- **Output**: Saves the processed dataset to `results.csv`.

**Code Highlights**:
- Modular functions (`create_attributes`, `extract_data`, `scrape_table`) for reusable scraping logic.
- Custom extractors for complex fields like nationality and birth year.
- Multi-index column structure for organized data presentation.

### Exercise 2: Statistical Analysis

**Objective**: Perform statistical analysis to identify top/bottom performers and compute team/player statistics, with results saved to `top_3.txt` and `results2.csv`.

#### Part 1: Top 3 Highest and Lowest Performers
- **Task**: Identifies the top 3 and bottom 3 players for each numeric statistic.
- **Process**:
  - Converts relevant columns to numeric types, filling missing values with 0.
  - For each statistic, sorts players to find the highest and lowest values.
  - Saves results to `top_3.txt` in a readable format (e.g., "Statistic: goals\nTop 3 Highest:\n1. Player A (10)\n...").
- **Output**: `top_3.txt` lists the top and bottom performers for each statistic.

#### Part 2: Median, Mean, and Standard Deviation
- **Task**: Calculates the median, mean, and standard deviation for each statistic across all players and per team.
- **Process**:
  - Processes numeric columns, handling missing values.
  - Computes statistics for the entire dataset ("all") and each team.
  - Organizes results in a multi-index dataframe with columns for median, mean, and standard deviation.
- **Output**: Saves results to `results2.csv`.

**Code Highlights**:
- Efficient use of `Pandas` for numeric conversions and statistical computations.
- Multi-index dataframe for structured output in `results2.csv`.
- Clear text formatting in `top_3.txt` for easy interpretation.

### Exercise 3: Clustering Players

**Objective**: Group players into clusters based on performance metrics to identify similar playing styles or roles using K-Means clustering.

**Key Components**:
- **Data Preparation**:
  - Selects a subset of performance metrics, including per-90 stats (e.g., `goals_per90`, `assists_per90`), passing stats (e.g., `passes_completed`, `passes_pct`), defensive actions (e.g., `tackles`, `interceptions`), and possession metrics (e.g., `touches_att_3rd`, `carries_into_penalty_area`).
  - Converts selected features to numeric types, filling missing values with 0.
  - Standardizes features using `StandardScaler` to ensure equal weighting during clustering.
- **Clustering**:
  - Applies K-Means clustering with an optimal number of clusters (set to 4, determined via the elbow method).
  - Tests cluster counts from 1 to 10 to compute inertia and visualize the elbow curve.
  - Assigns each player to a cluster, storing the cluster label in a new `Cluster` column.
- **Visualization**:
  - Uses PCA to reduce features to 2D for visualization.
  - Creates a two-panel plot:
    - Left: Elbow plot showing inertia vs. number of clusters to justify the choice of 4 clusters.
    - Right: Scatter plot of players in 2D PCA space, colored by cluster, with a colorbar indicating cluster labels.
  - Saves the plot as `player_clustering.png` with high resolution (300 DPI).
- **Output**:
  - Saves a CSV file (`clustered_players.csv`) containing player names, teams, positions, cluster labels, and selected features.
  - Generates `player_clustering.png` for visual analysis of clusters.

**Code Highlights**:
- Careful feature selection to capture diverse aspects of player performance (attacking, passing, defending, possession).
- Use of `StandardScaler` and `PCA` for robust preprocessing and visualization.
- Professional visualization with `Seaborn` and `Matplotlib`, including customized styling (e.g., whitegrid, bold fonts, color schemes).
- Elbow method implementation to determine the optimal number of clusters.

### Exercise 4: Player Market Value Prediction

**Objective**: Build a Random Forest model to predict player market values based on their statistics, with results visualized in a scatter plot.

**Key Components**:
- **Data Preparation**:
  - Assumes a merged dataframe with a `price` column (in €, with "M" or "K" suffixes).
  - Converts prices to numeric values (e.g., "€10M" → 10,000,000).
  - Drops irrelevant columns (e.g., `player`, `nationality`) and encodes categorical variables (`nationality`, `team`, `position`) using `LabelEncoder`.
  - Fills missing numeric values with column medians.
- **Modeling**:
  - Uses a `RandomForestRegressor` with tuned hyperparameters (`n_estimators=100`, `max_depth=15`, `min_samples_split=5`, `min_samples_leaf=3`).
  - Splits data into 80% training and 20% testing sets.
  - Evaluates performance using Mean Squared Error (MSE) and R² score.
- **Visualization**:
  - Plots actual vs. predicted prices (in millions of €) using `Matplotlib`.
  - Includes a diagonal line for reference and displays MSE and R² in the title.
  - Saves the plot as `actual_vs_predicted.png`.
- **Feature Importance**: Computes and sorts feature importances to identify key predictors of market value.

**Code Highlights**:
- Robust price conversion function to handle various formats.
- Use of `LabelEncoder` for categorical variables.
- Clear visualization with `Matplotlib` and `Seaborn` for model evaluation.
- Feature importance analysis to understand model behavior.

## Output Files

- **results.csv**: Comprehensive dataset of player statistics with multi-index columns.
- **top_3.txt**: List of top 3 and bottom 3 players for each statistic.
- **results2.csv**: Median, mean, and standard deviation for each statistic, overall and per team.
- **clustered_players.csv**: Player names, teams, positions, cluster labels, and selected features (from Exercise 3).
- **player_clustering.png**: Visualization of player clusters with elbow plot and PCA scatter plot (from Exercise 3).
- **actual_vs_predicted.png**: Scatter plot of actual vs. predicted player market values (from Exercise 4).

## Usage

1. **Setup**:
   - Install dependencies and configure Chrome WebDriver.
   - Ensure the Jupyter Notebook environment is set up.
2. **Run the Notebook**:
   - Execute `Python Assignment.ipynb` in Jupyter.
   - Ensure internet access for scraping FBref pages.
3. **Notes**:
   - The `df_merge` in Exercise 4 assumes an additional `price` column. You may need to merge the scraped data with a market value dataset.
   - Exercise 3 uses a fixed number of clusters (4); you can adjust `optimal_k` or explore other clustering methods (e.g., DBSCAN) for different insights.
   - Web scraping may fail if FBref's structure changes; verify table classes and URLs.
   - Adjust file paths if running in a different environment.

## Future Improvements

- Add error handling for web scraping failures (e.g., network issues, page changes).
- Incorporate additional data sources for market values in Exercise 4.
- Enhance clustering in Exercise 3 with advanced techniques (e.g., silhouette score analysis, hierarchical clustering).
- Include more visualizations (e.g., feature importance plots, cluster profiles, team comparisons).
- Optimize Random Forest model with hyperparameter tuning (e.g., GridSearchCV).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.