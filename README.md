# Renovate_to_increase_SalePrice
Use King County Housing Data to recommend improvements that increase the value of home-owners' properties.

## Overview

This project aims to produce recommendations for home-owners who want to renovate their homes based on the price increase associated with those renovations.  The King County Housing data set has been interpretted via multiple linear regression to make recommendations as to how much certain renovations increase the price of a home.

One idea, is for these recommendations to be used within an application of an existing real-estate tech company such as Redfin or Zillow to drive traffic to their platform and increase income from  a variety of their products.

## Business Problem

* Home-owners want to know: 
    * Will renovations increase the price of my home?  
        * And if so, by how much?
        * Which renovations will reap the greatest reward?

* Housing Data allows us to make strong inferences and therefore recommendations to answer these questisons.

## Data

The data for this project comes from a King County Housing data set, including home sales from years 1900 - 2015. The factors in this data set included in the final model were: price (independent variable), sqft_living, bathrooms, bedrooms, yr_built, floors, waterfront, view, grade, and condition (dependent variables). Factor or feature interpretation can be found on the [King County eSales website](https://info.kingcounty.gov/assessor/esales/Glossary.aspx?type=r).

Some data cleaning and manipulation was required.  For example, the categories waterfront and view contained NaN values that did not represent a value, so those placeholders were replaced with the median value in those columns, which was NO for Waterfront and NONE for view.

The categorical variable waterfront was binary encoded so it would become a yes/no or True/False feature.

The categorical variables view, grade, and condition were one-hot-encoded and the columns condition_Poor, condition_Average, grade_3 Poor, grade_7 Average, grade_10 Very Good, view_NONE, and view_Average were all dropped to prevent multicollinearity.

No values were changed in the numerical columns, as their value counts all seemed accurate and did not contain missing information.

Outlier rows were removed based on the column Price, resulting in a loss of 1.07% of the overall data set.


## Methods

The results were calculated from a multiple linear regression that prioritized inferential results, while attempting to maximize predictive results.  A more predictive model could be built with product features that incorporate interactions between the predictors, however this model would not produce predictions that are as accurate, so interactions between features were not included in the final model.

The final model, as determined by statsmodels' Ordinary Least Squares Regression Summary, had an R-squared and Adj. R-Squared value of 0.558

The final model also met all assumptions of linearity. Including: normality, multicollinarity, and homoscedasticity.  

* Normality was determined using scipy.stats linreg.predict() function, which shows the closeness of fit between sample and theoretical quantities after a train, test, split has been performed.

* Multicollinarity was calculated with statsmodels' stats.outliiers_influence package that includes a variance_inflation_factors function.  Features with a variance inflation factor (VIF) score above 5 were removed.  Removed features included: view_NONE - score 12.4 and grade_7 Average - score 7.42.

* Homoscedasticity was measured by plotting the residuals (Actual-Predicted) against the predicted value.  The scatter plot showed a fairly even distribution about the x and y axes.

## Results

Feature Impact on Price:

- Calculated from features and independent variable that were logged and normalized through z-score standardization.

* An increase of 918.11 square feet increased the price by 187,614.89
* An increase of 0.769 bathrooms increased the price by 36,222.49
* An increase of 0.926 bedrooms decreased the price by 47,390.48
* Addition of waterfront increased price by 154,661.97
* Changing view from Fair to Excellent, increased price by 99,373.07
* Changing condition from Fair to Very Good, increased price by 155,102,81
* Changing grade from grade8_good to grade9_better, increased price by 126,448.10
* An increase of 29.38 years of age decreased the price by 105,765.28
* An increase of .54 floors increased the price of a house by 41,843.23

The Train, Test, Split of the final model led to a Train Mean Squared Error of 0.4000 and a Test Mean Squared Error of 0.3844 with a train R-squared value of 0.5618, which is a promising result for a largely inferential model.

### Visual 1
![Top Features by Price Increase](https://github.com/jpetoskey/Renovate_to_increase_SalePrice/blob/main/images/Top%20Features%20by%20Price%20Increase.png)

### Visual 2
![Secondary Features by Price Increase](https://github.com/jpetoskey/Renovate_to_increase_SalePrice/blob/main/images/Secondary%20Features%20by%20Price%20Increase.png)


## Conclusion

Renovating to increase sale price is a viable option for homeowners and seems like it would provide value to customers who own homes or who want to buy a home and evaluate the price of a recently remodeled property.

It seems viable to create an application and website that would provide homeowners suggestions for which renovations would improve the sale price of their home.  This type of product would make money through advertising on their website and application.

Many real estate tech companies would like to have a product like this in their suite of businesses to funnel more customers to their platform.

### Renovate Interior
* Grade and Condition score increases were correlated to large price increases.
Spending on an interior renovation, especially in regards to the whole house being considered very good to luxury is likely to increase sale price.

### Create a View
* Add larger windows that face pleasant scenery.
* Add a deck or rooftop deck to enhance access to outdoor views.
* Landscape and design views from windows to include desirable plants and scenery.

### Add Square Footage
* Add liveable space in your home.
* Not necessarily bedrooms or bathrooms, though it is better to add bathrooms, in terms of sale price.
* Renovate Garage to be fully insulated livable space.
* Add a guest cottage with full pluming, electrical, and HVAC.


## Further Studies Recommended

Examine other housing data sets to determine if they contain similar trends to predictors in the King County Data Set.

Find additional predictors to better estimate how much certain home changes alter sale price.¶
* Type of remodel or home additions.
    * Ex. Kitchen, Garage, Patio, additional Bedrooms/Bathrooms.
    
Estimate return on investment for renovations.
* How do certain projects increase sale price?
    * Example: Is it better to convert a garage to livable space or update a bathroom?
* What amount of spending reaps a higher gain?

## For More Information

Please review my full analysis in [Jupyter Notebook](.Phase 1 Project - Microsoft Studios Proposal - Jim Petoskey.ipynb) or my [presentation](https://github.com/jpetoskey/Renovate_to_increase_SalePrice/blob/main/Return%20on%20Renovation.ipynb).

For any additional questions, please contact **Jim Petoskey - Jim.Petoskey.146@gmail.com**

## Repository Structure

```
├── README.md                           <- The top-level README for reviewers of this project
├── Return_on_Renovation.ipynb   <- Narrative documentation of analysis in Jupyter notebook
├── Return_on_Renovation.pdf         <- PDF version of project presentation
├── data                                <- Both sourced externally and generated from code
└── images                              <- Both sourced externally and generated from code
```
