# FLATIRON SCHOOL PHASE 2 PROJECT
*Angelo Turri*

## Stakeholder & Problem
A real estate company, BlackSock, is looking to invest in King County houses. Their plan is to buy these homes, rent them out for a duration of time, and then sell them after their value increases a satisfactory amount. To maximize profits, this company wants information on several factors that influence the price of such homes.

## Data Origin & Description
All of our data was taken from https://info.kingcounty.gov/assessor/DataDownload/default.aspx.
Descriptions of any of the original variables can be found here https://info.kingcounty.gov/assessor/esales/Glossary.aspx?type=r.

Important variables from the original dataset include:

- the date a house was sold & built
- the price it was sold for
- the square footage of:
    - living space
    - space above grade (everything except the basement)
    - patio
    - garage
    - lot
- number of floors, bedrooms, and bathrooms
- home quality (called 'grade' in the dataset)
- the latitude & longitude
- address

## Rationale
BlackSock is looking for insights into what impacts home price; these insights are meant to inform their long-term investment decisions. I am using linear regression to give BlackSock the insights they want.

Linear regression is a modeling technique that allows us to understand relationships between data and make predictions about unknown data. In our specific case, linear regression can:

- tell us how much certain independent variables influence a dependent variable (price)
    - This is directly relevant to the stakeholder's problem
- yields a formula which allows us to predict the price of a home based on data we've collected
    - This is also directly relevant to the stakeholder's problem
    
## Limitations
- Our data has the most important home properties, but it lacks many others; for example, it does not record brick color, type of flooring, the inclusion of a house water filter, ceiling style, etc. Furthermore, it only covers sales in one year. A model is only as good as the data you put into it; as such, our model can only give preliminary insights. While we recommend that BlackSock heed our model's results, we also recommend they utilize other models in conjunction with ours and refrain from making any major investment decisions based on our model alone.

## Data Cleaning

- Our modeling technique, linear regression, has certain standards for data that should be adequately met. In order to do this, we had to eliminate some data that did not adequately satisfy these standards. This included data that:
    - Did not have a linear relationship with the price variable;
    - Was collinear (independent variables that had a correlation coefficient of 0.7 or more with each other)

- There were some outliers in our data (houses that cost over 10 million dollars, etc). Such outliers can skew our data and thus harm our model's accuracy. To avoid this, I eliminated these outliers.

- I only used numeric variables to make the modeling process easier.

- I avoided using any variables that had very weak relationships with price, as they contributed little to nothing in the model.

## Feature Engineering

Our initial dataset had a limited range of variables which I could use in the model. Using existing data, I created a number of new variables in the hope that some of them would significantly contribute to the model's accuracy. Only one of them did; it was a variable called "vicinity_price". This variable measured the average price of homes in a particular house's vicinity (we used latitude/longitude to determine the vicinity). Each particular house that we examined was eliminated from the average, to avoid a house predicting its own price.

## Modeling

I used an iterative modeling technique – that is, I started with a basic model and made adjustments from there. My first model only included the vicinity_price variable. My second included the grade and sqft_living variables. My third included all the same variables but I transformed them to make the model more interpretable – that is, I wanted the results of the model to make more sense to a layperson.

I used several visualizations and model metrics to analyze model performance. One important visualization I used was a scatterplot of the original price values vs. the price values that our model predicted for each house. This graph shows how close the model's predicted values are to the real ones. Another important visualization was a residual histogram. "Residuals" are the magnitude of your model's prediction errors. These residuals are supposed to be normally distributed, and this histogram shows you if they are.

As for model metrics, I used the adjusted R-Squared and the Mean Absolute Error (MAE). The adjusted R-Squared value is a measure of how well your model fits the actual data. The closer to 1 that it is, the better your model fits the data. The MAE is how much your model's predictions typically deviate from the real values.


## Model interpretation

The variables used in our final model were vicinity_price, grade, and sqft_living.
- Vicinity_price: the average price of surrounding homes for each individual house.
- Grade: a numerical variable ranging from 1 to 13 measuring the quality of the home. These are the meanings for the values:
    - 1: Cabin
    - 2: Substandard
    - 3: Poor
    - 4: Low
    - 5: Fair
    - 6: Low average
    - 7: Average
    - 8: Good
    - 9: Better
    - 10: Very good
    - 11: Excellent
    - 12: Luxury
    - 13: Mansion
- Although the grade variable was initially a categorical variable, it had all the properties of a numerical variable. The median value on this scale (7) represented an average grade, which is exactly right. Each increase in grade seems to represent a similar increase in home quality. And finally, the average grade of all the houses in the dataset was 7.7, which is very close to an "average" grade – exactly as you'd expect.
- Sqft_living: the square footage of living space in the home.

Our model yielded the following insights:

- A house in King County surrounded by average-priced homes, with an average grade, and average living space, costs about $1.1 million.
- For every dollar increase in the price of homes in the house's vicinity, the house's price goes up by 76.3 cents.
- Every increase on the grade scale increases house price by about $85,000.
- Every additional square foot of living space increases house price by $260.

On average, our model's predictions were off by about $222,000. The model had an adjusted R-Squared of 0.735 which means it was a reasonably good fit for the data.

## Recommendations

Based on this model, we recommend that BlackSock look at properties whose area is likely to go up in value. We also recommend that they rennovate the house if doing so results in an increase in grade and the cost of doing so is less than $85,000.

Finally, we recommend that BlackSock consult other models in addition to ours. Although our model had reasonably good metrics, they weren't good enough to inform huge investments on their own. However, we still think our model yielded useful insights and that BlackSock should take them into account.

## Repository Structure
- **[data](https://github.com/Jellohub/phase2_project/tree/master/data)**: folder containing data file and and descriptions of variables.
- **[project notebook](https://github.com/Jellohub/phase2_project/blob/master/notebook.ipynb)**: project notebook containing all data imports, cleanup, analyses, and visualizations
- **[visualizations](https://github.com/Jellohub/phase2_project/tree/master/visualizations)**: folder containing all visualizations used in the project notebook and presentation
- **[presentation](https://github.com/Jellohub/phase2_project/tree/master/presentation.pdf)**: pdf file with all presentation slides
- **[notebook pdf](https://github.com/Jellohub/phase2_project/tree/master/notebook.pdf)**: pdf version of project notebook