# Premier League Player Statistics Analysis

This repository contains a Python-based project that scrapes, processes, and analyzes player statistics from the Premier League, sourced from [FBref](https://fbref.com). The project is structured into three main exercises, each implemented in a Jupyter Notebook (`Python Assignment.ipynb`). Below is a detailed description of each component to help users understand the purpose and functionality of the code.

## Project Overview

The project focuses on collecting comprehensive player statistics from the Premier League, performing statistical analysis, and building a predictive model for player market values. It leverages web scraping, data processing, and machine learning techniques using Python libraries such as `BeautifulSoup`, `Selenium`, `Pandas`, `Scikit-learn`, and `Matplotlib`.

The notebook is divided into three exercises:
1. **Exercise 1**: Web scraping and data aggregation into a structured CSV file.
2. **Exercise 2**: Statistical analysis (top/bottom performers and team/player statistics).
3. **Excercise 3**: Clustering Players for Classfiers
4. **Exercise 3**: Machine learning to predict player market values.

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



### Exercise 4: Player Market Value Prediction

**Objective**: Build a Random Forest model to predict player market values based on their statistics, with results visualized in a scatter plot.

**Key Components**:
- **Data Preparation**:
  - Assumes a `df_merge` dataframe containing player statistics and a `price` column (in €, with "M" or "K" suffixes).
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
- **actual_vs_predicted.png**: Scatter plot of actual vs. predicted player market values.

## Usage

1. **Setup**:
   - Install dependencies and configure Chrome WebDriver.
   - Ensure the Jupyter Notebook environment is set up.
2. **Run the Notebook**:
   - Execute `Python Assignment.ipynb` in Jupyter.
   - Ensure internet access for scraping FBref pages.
3. **Notes**:
   - The `df_merge` in Exercise 3 assumes an additional `price` column. You may need to merge the scraped data with a market value dataset.
   - Web scraping may fail if FBref's structure changes; verify table classes and URLs.
   - Adjust file paths if running in a different environment.

## Future Improvements

- Add error handling for web scraping failures (e.g., network issues, page changes).
- Incorporate additional data sources for market values in Exercise 3.
- Enhance the Random Forest model with hyperparameter tuning (e.g., GridSearchCV).
- Include more visualizations (e.g., feature importance plots, team comparisons).

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
