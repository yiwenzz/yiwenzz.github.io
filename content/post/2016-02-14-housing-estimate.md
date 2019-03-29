---
title: Analysis of Housing Prices, Features Based Study  – Albuquerque, NM
author: Yiwen Wu
date: '2016-02-14'
categories:
  - Products
tags:
  - Statistics
  - Data

---

![](/img/housing1.jpg)


# Introduction
Analyzing home prices is based on different factors that could affect the price of a house. Home prices may be affected by different factors such as square footage, age, number of features, location, etc. In this study, a dataset from Albuquerque was taken including square feet, age, number of certain features (out of 11, from dishwasher, refrigerator, microwave, disposer, washer, intercom, skylight(s), compactor, dryer, handicap fit, cable TV access), custom built or not, corner location or not, whether the home was located in the Northeast sector of the city, and its annual taxes. All these factors were analyzed to determine the best model for predicting the home price. Following the analysis, the model was checked to see if it would meet all assumptions. In this study, all factors were analyzed to determine the best model to predict home selling prices in Albuquerque.

# Methods
A dataset of 117 homes from the multiple listing agency in Albuquerque was used to analyze the estimated home price. The dataset included information about homes for sale such as selling price, square feet of living space, age, number of features (out of 11, from dishwasher, refrigerator, microwave, disposer, washer, intercom, skylight(s), compactor, dryer, handicap fit, cable TV access), location (if in the northeast part of the city or not), whether or not the home has custom features, whether or not the home is at a corner location, and annual taxes.  

The model began with the assumption that at least one of the aforementioned variables would be significant in predicting home prices in Albuquerque. This was tested in Minitab by fitting a regression model using all variables available. An H0 that all the variables had a slope of zero (were insignificant) was tested against an H1 that at least one variable had significance. This test produced an F-value of 94.74 and a p-value of 0. Because this p-value is less than 0.05, there is sufficient reason to reject H0. As such, there is evidence that at least one of the variables is in some way significant in predicting home price in Albuquerque. 

Since at least part of the model was found to be significant, the gathered data were analyzed in Minitab, with a regression model fit using both the stepwise and backward elimination procedures. The stepwise procedure goes through an iterative process of starting with the most significant variable on its own and then adds in other variables in order of significance. With each addition, the procedure checks to make sure the variable does not need to be removed – none did in this case. The procedure is complete once a model is found such that adding more variables does not significantly increase the abilities of the model. The backward elimination procedure effectively does the same thing in reverse: starting with all variables and removing the least significant variable each step until a model loses significance with a removal. 

Based on this, there is a statistically significant model to determine the selling price of a home in Albuquerque, NM from the variables above. This assumes that the multiple listing service data is accurate and unbiased and that all the assumptions for multiple least squares regression are met. 

# Results and Analysis
Based on the stepwise regression, the best variables to predict selling price are the square feet of living space, annual taxes, and whether or not the home has custom features. The regression equation is PRICE = 74.8 + 0.3206 SQFT + 0.561 TAX + 178.5 CUST. The reason this model was chosen has to do primarily with the Mallow's Cp calculation for each model in the stepwise regression. The above model has a Mallow's Cp value of 3.06, with the ideal value being 4. The models that come before (PRICE = -11 + 0.3910 SQFT + 0.567 TAX) and after (PRICE = 97.9 + 0.3364 SQFT + 0.523 TAX + 177.2 CUST – 77.8 COR) the one chosen have Mallow's Cp values of 12.65 (ideal value of 3) and 2.38 (ideal value of 5), respectively. The model chosen has a Mallow's Cp closest to the ideal value for a 3 variable model. While the Mallow's Cp for this model indicates that there are too many variables, the other options either are extremely biased (12.65) or suggest even more strongly that too many variables are used (2.38). 

Because data were removed from the stepwise regression that are still usable with the variables chosen, another regression (not stepwise) using the chosen variables was carried out. The regression equation is calculated to be PRICE = 164.7 + 0.1881 SQFT + 0.709 TAX + 162.1 CUST. This means that a home with 0 square feet of living space, 0 annual taxes, and no custom features has an average selling price of 16,470. With every 1 square foot increase in living space (everything else held constant) the average selling price increases by 11.81 dollars, with every 1.00 dollar increase in annual taxes (everything else held constant) the average selling price increases by 70.90, and the addition of custom features raises the average selling price by $16,210.

Several assumptions must be met for this least squares regression to be valid, and they were all tested below:

1.	The mean of the residuals is zero. This assumption is always true for least squares regression.
2.	The variance of the residuals is constant. Based on the Residuals vs Fits plot and all the residuals vs variable plots, since there appears to be a “cone” shape in the Residuals vs Fits as well as the Residuals vs SQFT and to a lesser extent in the Residuals vs TAX plot, there appears to be an issue with this assumption in this model.
3.	The distribution of the residuals is normal. Based on the probability plot of the residuals, because the p-value is less than 0.05, there is evidence that the distribution of the errors is not normal. As such, this assumption is not met.
4.	The errors and observations are independent. Because no time order of observations is provided, this assumption cannot be tested.
5.	The model chosen is appropriate. Because there does not appear to be any curve shape or pattern in any of the Residuals vs Plots, there do not seem to be any issues with the model not being appropriate. This assumption is met.

Overall, there are some issues with the assumptions for the multiple regression model. The variance of the errors is not constant, and the distribution of the errors is not normal. Because of this, there is reason to not use this model to predict home price without addressing these first.

Based on the model selected, a home with 2100 square feet of living space; an age of 40 years; a washer, dryer, fridge, microwave, disposer, and cable TV; a location in the SW corner of the city; no custom features; a location not on a corner; and an annual tax of 1,900 USD would have a selling price of 164.7+0.1881(2100)+0.709(1900)+162.1(0) = 190,694. Note that because of the model determined to be best, only the square footage, taxes, and (lack of) custom features played a role in estimated sale price.  

For this estimated sale price, there is a 95% predication interval of (152,939; 228,449). This means that there is 95% confidence that a single home with 2100 square feet of living space, no custom features, and an annual tax of 1900 USD per year will sell for a price within this range. It is very important to note, however, that of all the data collected, the tax rates only fall between 223 and 1765 USD per year. As such, this prediction is outside the range of available data, and may not represent what will actually occur.  


![](/img/housing_post1.jpg)

![](/img/housing_post2.jpg)

![](/img/housing_post3.jpg)


![](/img/housing_post4.jpg)

![](/img/housing_post5.jpg)

# Conclusion
In summary, the selling price of a home in Albuquerque appears to be most closely related to the size of the home (living area in square feet), taxes assessed on the home, and the inclusion of custom features. There were some issues with the model, including a lack of constant variance and normality regarding the error of the regression. So, while the model may not be ideal for predicating home prices in Albuquerque, it does indicate that things like size, taxes paid, and custom features have a larger effect on price than qualities such as features or age. This generalization may extend to homes around the nation as well. In the future, it would be helpful to gather more data from more areas to test this hypothesis, but the data could be limited to taxes paid, sizes, and inclusion of custom features as opposed to needing to gather 8 sets of data. 









