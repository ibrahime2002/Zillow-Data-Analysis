# US Housing Price Analysis and Forecast (2015-2024)

This project analyzes and forecasts US housing prices using Zillow's ZGVI (Zillow Home Value Index) dataset. The analysis involves data cleaning, exploratory data analysis (EDA) at both the city and state level, and time-series forecasting to predict future prices for key states.

## Key Features & Insights

* **Multi-Level EDA:** Conducts a "top-down" analysis, starting with a national-level trend, moving to state-level comparisons (Top 10 Most Expensive, Key State Trends), and finally performing a targeted, city-level analysis of major US markets.
* **Targeted Market Analysis:** Compares the 10-year growth rate of 14 major US cities (e.g., 'Austin, TX' vs. 'San Francisco, CA') by precisely filtering the dataset using a `pandas` merge.
* **Predictive Modeling:** Implements a time-series forecast using **Prophet** to predict the average home price for the next 24 months for 5 key states: CA, TX, NY, WA, and CO.
* **Data-Specific Insight:** Highlights a key finding about the dataset itself, explaining why its "middle-tier" focus leads to different (and often higher) growth rates than the median prices cited in news reports.

---

### A Note on the Data: "Middle-Tier" vs. "Median"

A crucial finding of this project is the importance of data specificity. The dataset used is Zillow's **`City_zhvi_uc_sfrcondo_tier_0.33_0.67_...`**, which tracks the average price of "middle-tier" homes (those between the 33rd and 67th percentile).

This differs from the more common **median** price (50th percentile) often cited in news reports.

* **What this means:** The growth rates in this analysis (e.g., ~150% for Houston) are higher than the 80-90% figure one might find on Google.
* **Why?** This data suggests that the *lower end* of the market (starter homes, near the 33rd percentile) grew significantly faster than the upper end. This is a valuable insight: the "floor" of the market rose faster than the "ceiling," making this dataset ideal for analyzing market entry pressure and affordability challenges.

---

### Analysis & Methodology

The project is broken into two main parts: (1) Exploratory Data Analysis and (2) Predictive Forecasting.

#### 1. Data Cleaning & Exploratory Analysis (Pandas, Matplotlib, Seaborn)

The initial script loads the raw data, cleans it by dropping rows with excessive missing values, and then performs four key analyses to understand historical trends:

1. **Top 10 Most Expensive States:** Identifies the states with the highest average home price over the entire period.
2. **National Price Trend:** Plots the average price of all cities over time to establish a single national trend line.
3. **Key State Comparison:** Compares the historical price trends of five major states (CA, TX, NY, FL, WA) on a single line chart.
4. **Major City Growth:** Uses a `pd.merge()` operation to create a precise list of 14 major US cities and plots their total growth rate from 2015 to 2024.

#### 2. Predictive Forecasting (Prophet)

The second half of the project focuses on forecasting. To get a stable, high-level forecast, the data is aggregated to the state level for five key states (CA, TX, NY, WA, CO).

* **Why Prophet was Chosen:** A common machine learning model like a Random Forest (from `scikit-learn`) is not suitable for this problem. A Random Forest **cannot extrapolate**—it is unable to predict a price higher than the maximum price it has ever seen in the training data. This would result in an unrealistic "flat-line" forecast.
* **The Solution:** The `Prophet` library is used because it is specifically designed for time-series forecasting. It works by **decomposing** the data into its core components:
    1. **Trend:** The long-term growth (which this model *can* project into the future).
    2. **Seasonality:** The yearly, recurring patterns (e.g., prices rising in spring).
    3. **Holidays:** (Not used in this model but a key feature).

This approach provides a realistic 24-month forecast that captures both long-term growth and seasonal market behavior.

---

### Key Visualizations

*(In GitHub, you can drag and drop your saved `.png` files directly into this text editor to embed them. Replace these lines with your images.)*

`![Top 10 States by Price](top_10_states.png)`

`![Major City Growth](major_city_growth.png)`

`![National Trend](national_trend.png)`

`![State Forecast](state_forecast_plot_prophet.png)`

---

### How to Run This Project

1. Clone the repository:

    ```bash
    git clone [your-repo-url]
    cd [your-repo-name]
    ```

2. Install the required libraries:

    ```bash
    pip install pandas matplotlib seaborn prophet
    ```

3. Place the raw data file `City_zhvi_uc_sfrcondo_tier_0.33_0.67_sm_sa_month.csv` in the same directory as the script.

4. Run the Python script:

    ```bash
    python [your_script_name.py]
    ```

### Technologies Used

* **Python**
* **Pandas:** Data loading, cleaning, filtering, and aggregation
* **Matplotlib & Seaborn:** Data visualization
* **Prophet:** Time-series forecasting
* **Jupyter Notebook** (Optional, but recommended)
