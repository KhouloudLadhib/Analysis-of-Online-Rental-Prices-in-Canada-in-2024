# Analysis of Online Rental Prices in Canada in 2024

##  Goal
This python code analyzes data of rental prices of Canadian rental properties posted online and to build a predictive model to predict prices. Below are the questions that the project answers.

* What's the monthly average rental price of posted properties?
* What are the provinces with the lowest number of postings?
* Which provinces have the lowest and highest average rental prices?
* How big is the percentage of rental properties not allowing each kind of pets?
* Is there a trend in rental prices when it comes to rental terms?
* What is the cheapest rental type and most expensive one?
* Is there a trend in rental prices when it comes the number of beds?

## Data
The data contains 25771 lines before cleanup. There are 17 rows in the dataset. This dataset contains Real Estate Rents listings in the Canada broken by Province and City. Data was collected via web scraping using python libraries.
Source for data: https://www.rentfaster.ca/
Source for description: https://www.kaggle.com/datasets/sergiygavrylov/25000-canadian-rental-housing-market-june-2024

### Variables:
* rentfaster_id:  id of property on https://www.rentfaster.com . Can be explore with www.rentfaster.ca/rentfaster_id
* city: city of property like Toronto, Calgary, Vancuver and etc.
* province: province of property like Alberta, Ontario and etc.
* address: address of property like 333 Seymour St and etc
* latitude: latitude coordinate of rental property
* longitude: longitude coordinate of rental property
* lease_term: category of rental period like Long Term, Negotiable and etc
* type: category of type a rental property like House, Apartment, Basement and etc
* price: price in CAD
* beds: count of bedrooms
* baths: count of bathrooms
* sq_feet: area of rental property in square feets
* link: right side of url for getting full details of the property rentfaster.com+link
* furnishing: Furnished or not
* availability_date: Date of availability
* smoking: allow smoke
* cats: allow cats
* dogs: allow dogs

## Findings:
On average, the rental price per month is $2152
New Brunswick, Newfoundland and Labrador, and Northwest territories have very low numbers of postings. It either means that these places don't have many rental properties or the data was collected from a source that isnèt really used in these places.

Newfoundland and Labrador seem to be the cheapest place to rent in and British Columbia seems to be the most expensive place to rent in.

35% of rental properties do not allow cats vs about 38% for dogs.

The shorter the rental term, the more expensive it is.

Parking Spot and Storage seem to be the cheapest rental types which makes sense since these rental types usually have less regulations (cost less to create) and usually have less space than a residential rental.

Acreage is the most expensive type of rentals.

There seems to be a trend in the number of beds. The more beds there are the more expensive the property is with the exception of 9 properties of 9 beds which cost 1392 monthly on average. This may be explained by outliers or an error in the data collection for 9-bed rentals.

Some outliers were found in the prices and were removed before conduting the regression models.

StandardScale was be used because we are assuming normal distributions in the data. OneHotEncoder wwas be used because the categorical variables are ordinal.

Model1 is a simple linear regression with all variables. The error metrics are too high which means that this model does not perform well in predicting rental prices. In addition, the model is performing much better in the testing then when predicting which means that there might be a case of overfitting.

Model2 was obtained by running the same parameters as model1 but without the 'city' variable. It is performing much better than model1. The independent variables can explain 47.3% of the rental prices. In addition, the model seems to perform as well in the predictions as it does in testing which means that there is no issue with overfitting. type_Vacation Home seems to be the most influential predictor of rental prices.

Model3 was obtained by running a second degree polynomial regression on all variables except for city. Similarly to model1, the error metrics are too high which means that this model also does not perform well in predicting rental prices. In addition, the model is performing much better in the testing then when predicting which means that there might be a case of overfitting.

Model4 was obtained by using the same parameters as model3 but by applying ElasticNetCV. elasticcv_model seems to be the best predictive model compared to the other three. It has the lowest MAE, MSE and RMSE values and has the highest R2 value. The model can explain 49.2% of the variations in rental prices and performs as well in predicting than in testing.