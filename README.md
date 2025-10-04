# Linear Regression - Predicting House Prices

**Team Number:** 

- `Team 2`

**Team Name:** 

- `SRAF`

**Team Members:**

- `Ananya Makwana`
- `Faye Yang`
- `Jianan Peng`
- `Rosnita Dey`

---

## Report

## Data Distribution Analysis

Our group's Linear regression model utilized the `Kaggle: Housing Prices dataset to predict House prices`.  
Processing the data into a histogram displayed a right-skewed distribution, specifically meaning that most of the
outliers from the data is from a higher price and the majority of houses are between 2 to 8 million dollars. There is
also a drop in number of houses that are at the 4 million mark, preventing a closer bell-shape for the histogram.

<p align="center">
  <img src="https://i.postimg.cc/9fXtx3X5/We-Chatcc6236826ebac5fe849f7f04380db89c.jpg" width="400"/>
</p>

## Model Performance & Outliers

The Linear regression model that we trained gives a close prediction for housing prices. From the comparison graph of
between Predicted and Actual House Prices, there is only 1 very visible outlier where the
actual price is far from the predicted linear fit line. For the outlier the actual price is in the 10 million area,
which is one of the outliers from the Kaggle data set. The predicted price is far lower than the actual price at the 8
million mark, meaning that our linear regression model does not provide accurate predictions for houses that are priced
very largely.

## Model Fit & Dataset Limitations

Out Best fit line for Predicted vs. Actual Houses prices has a lower slope from the best prediction line, meaning that
our predicted prices are generally lower than the actual prices. Because our model shows a linear path, it is Underfit.
This could be the result from insufficient training or features from the model. As the data from the Kaggle set provides
information of around 550 houses out of around 16000 in Ames, lowa, the data represents 3% of the housing population and
does not provide information of any the city or state. Thus, having a larger data set would enable a better prediction
of the housing price.

<p align="center">
  <img src="https://i.postimg.cc/XqnV5gcg/We-Chat354113cc5bcdc8f3dc83a272a401ae45.jpg" width="400"/>
</p>