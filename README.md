# Stock Price Prediction based on Analyst Ratings

![Stonks](images/stonks.png)

# Project Overview


### Business Understanding
This machine learning model aims to predict whether a stock's price is likely to increase or decrease based on analyst ratings. The data for the model will be obtained from the Koyfin website using selenium and beautiful soup to automate the downloading process. 

The final model will predict the 5-day stock movement primarily based on analyst ratings and changes in those ratings.

The final product will be a streamlit application which runs this model. 

### Stakeholders
The stakeholders for this project are any financial firms or individual investors who are interested in taking short-term positions in stocks. The model will be used to predict whether a stock is likely to increase or decrease in price over the next five business days, primarily based on analyst ratings and changes in those ratings.


### Evaluation Metrics

As I want an equal balance between false positives and negatives, I will use the F1 score as my evaluation metric. The F1 score is the harmonic mean of precision and recall.


### Data Understanding
The initial data includes the following features for each stock:
- Ticker
- Date
- Analyst Price Target (avg)
- Analyst Price Target (High)
- Analyst Price Target (Low)
- Analyst Price Target (StDev)
- Analyst Price Target (Median)
- Open Price
- Close Price
- Volume
- High Price
- Low Price
- Analyst average Rating
- Count of Price Targets from Analysts


#### Data Preparation
The data was aggregated by date, cleaned, and prepared for modeling. 
While at first I looked at each stock's data individually, the purpose was to look at the general effects of analyst ratings on stock price. Therefore, I aggregated the data by date, and just have ticker as a single feature. 

- Price vs Target Features
    -   Is stock price above min price target?
    -   Is stock price below max price target?
    -   Is stock price above mean price target?
    -   Is stock price below mean price target?
    -   Is stock price both above min price target and below max price target?
- Running Correlations (1, 3, 6 months) of stock price and analyst ratings
- Return Features
    -   One-day return (stock price change)
    -   Three-day return (stock price change)
    -   Five-day return (stock price change)
    -   Ten-day return (stock price change)
    -   Twenty-day return (stock price change)
    -   Thirty-day return (stock price change)
    -   Sixty-day return (stock price change)
- Average Analyst Rating Change (1, 3, 6 months)
- Average Analyst Price Target Change (1, 3, 6 months)
- Max Analyst Rating Change (1, 3, 6 months)
- Max Analyst Price Target Change (1, 3, 6 months)


#### Modeling
I utilized a variety of different models to train and test the data. The models I used included:
- Logistic Regression
- Random Forest
- XGBoost
- Support Vector Machine
- K-Nearest Neighbors
- Naive Bayes
- Decision Tree
- Extra Trees


## Conclusion

The best performing model in this project had a rounded F1 score of .50 and was an XGBoost model, optimized using grid search with the following parameters:

    Max Depth of 50
    Max Features of 'auto'
    Min Samples Leaf of 1
    Min Samples Split of 2
    Number of Estimators of 1500

The most significant features for the model were:

    10-day average price target change: the average of all analysts' price targets for a stock, and the change in that average over the last 10 days.
    Above median = False: a boolean feature indicating whether the stock price is above the median price target.
    3-day low price target change: the lowest price target of all analysts for a stock, and the change in that target over the last 3 days.
    3-day price target count change: the number of price targets from all analysts for a stock, and the change in that number over the last 3 days, indicating when analysts are adding or removing targets.
    180-day close change: the change in the stock price over the last 180 days.
    Price target - low: the current low price target for a stock.
    1-day high price target change: the change in the highest price target from all analysts for a stock over the last 1 day.
    Above min = False: a boolean feature indicating whether the stock price is above the lowest price target.
    3-day close change: the change in the stock price over the last 3 days.
    10-day average analyst rating change: the average rating of all analysts for a stock, and the change in that average over the last 10 days.

## Future Work
This project represents a preliminary iteration of the model, and there is much room for improvement, including:

    Adding additional features, such as:
        Rate features
        Company data
        Sector data
        Industry data
        Earnings data
    Further exploratory data analysis
    Deployment of a Streamlit application
    Additional model iterations
    Modeling based on individual stock data, rather than all stocks, to determine the impact of this change
    Modeling based on a single sector or industry to examine the effect of this change
    Outlier removal, for example, the analyst ratings and stock price correlation for Tesla may not be representative of the rest of the market and removing these outliers may impact the model results.
    Adding more stocks, beyond just the SP100, such as the SP500 and Nasdaq.
