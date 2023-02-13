# Stock Price Prediction based on Analyst Ratings

![Stonks](images/stonks.png)

# Project Overview


### Business Understanding
This machine learning model will predict if a stock is likely to increase or decrease in price based on the analyst ratings. The model will be trained on the data from the Koyfin website. The data will be downloaded, not scraped, but using selenium and beautiful soup to automate the downloading process to make it less arduous. 

The end model will predict 5-day stock movement based primarily on analyst ratings and the changing of those ratings. 


### Stakeholders
The stakeholders are any financial firm or individual investor who is interested in taking short-term positions in stocks. The model will be used to predict if a stock is likely to increase or decrease in price over the next five days (one business week), based primarily on analyst ratings and the changing of those ratings.


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

The best performing model achieved an F1 score of .50 (rounded). It was an XGBoost model which was gridsearched with the following optimal parameters:
- Max Depth of 50
- Max Features of 'auto'
- Min Samples Leaf of 1
- Min Samples Split of 2
- Number of Estimators of 1500

The most important features to the model include:
- The 10-day price target (average) change. This is the average price target over all of the analysts for the stock, and the change in that average price target over the last 10 days.
- Above median = False. This is a boolean feature which indicates if the stock price is above the median price of its price targets.
- The 3-day price target (low) change. This is the lowest price target over all of the analysts for the stock, and the change in that lowest price target over the last 3 days.
- The 3-day price target count change. This is the number of price targets over all of the analysts for the stock, and the change in that number of price targets over the last 3 days. This indicates when analysts are adding or removing price targets for the stock.
- 180-day close change. This is the change in the stock price over the last 180 days.
- Price target - low. This is the current low price target for the stock. 
- 1-day Price Target - High Change. This is the change in the highest price target over all of the analysts for the stock over the last 1 day.
- Above min = False. This is a boolean feature which indicates if the stock price is above the lowest price of its price targets.
- 3-day close change. This is the change in the stock price over the last 3 days.
- 10-day average analyst rating change. This is the average analyst rating over all of the analysts for the stock, and the change in that average analyst rating over the last 10 days.


## Future Work
This is the first iteration of the model, and has lots of improvements to be made, including:
- Adding more features
    - Rate features
    - Company data
    - Sector data
    - Industry data
    - Earnings data
- Expanded EDA
- Streamlit Application for deployment
- More model iterations
- Solving the model based only on SINGLE stock data, not all stocks. How would this change things?
- Solving the model based on a single sector, or industry. How would this change things?
- Outlier removal (for instance, I know from experience that the analyst ratings for Tesla and the correlation between analyst ratings and stock price are not representative of the rest of the market. How would removing these outliers change the model?)
- Adding more stocks. This was just with the SP100. What about the SP500? The Nasdaq?
