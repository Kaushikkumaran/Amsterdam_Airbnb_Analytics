# MISs381N-finalproject

## Steps to the solution
- Data Cleansing
- Exploratory Data Analysis
- Models
- Business Impact

## Exploratory Data Analysis
Listing Price seems to be largely driven by room type 
![image](https://user-images.githubusercontent.com/20616274/128670754-8bbfd36d-7f99-4baa-824a-d794b2689e1b.png)

Future Availability does not seem to affect the price
![image](https://user-images.githubusercontent.com/20616274/128670786-6d1956e6-74f7-4954-92b7-fb2a78f2dbc6.png)

For entire apartments, minimum nights at a listing seem to have a positive association with price
![image](https://user-images.githubusercontent.com/20616274/128670800-fd2dba10-64f6-4b3f-a345-bfcf13c36528.png)

Prices are affected by neighborhood, across homes and rooms
![image](https://user-images.githubusercontent.com/20616274/128671790-9c8d90d6-c039-46fe-9c61-b936ff632d31.png)

Explaining neighborhood price differentiation with safety
![image](https://user-images.githubusercontent.com/20616274/128670902-c854c92c-f667-4633-bab5-d7d2af2a0def.png)

Neighborhoods with higher safety score seem to have higher mean price
![image](https://user-images.githubusercontent.com/20616274/128671029-117db4ab-0867-4e57-b635-3984e940482c.png)

## Modeling
### KNN (K Nearest Neighbours)
Running a k-fold cross validation yields least Price RMSE of 50.1 at k = 35

Predictors used for modeling : 
- Neighborhood 
- Room Type 
- Latitude 
- Longitude

![image](https://user-images.githubusercontent.com/20616274/128671204-9c169807-eb38-4507-a862-78544f167507.png)

### Random Forest
Random Forest yields a RMSE score of 52 for Entire Apt and 42 for Private Room

Important Predictors:
- Longitude
- Latitude
- Number of reviews
- availability_365
- Minimum nights

![image](https://user-images.githubusercontent.com/20616274/128671691-117abfa1-12fa-43bc-8a9a-c8d4c92eb1cf.png)


Key Model Features:
Entire Home/Apt:
Train RMSE -  50
Test RMSE - 52

Private Room:
Train RMSE -  39
Test RMSE - 42
![image](https://user-images.githubusercontent.com/20616274/128671472-92e46e2b-ca62-4913-ab1f-523e9b3ace93.png)


Remarks:
- The prediction is better for private room type than entire apartment/house
- The model is under estimating at higher prices and over estimating at lower prices

### Linear Regression
Linear Regression yields a RMSE score of 51.5

Important Predictors:
- Room Type
- Neighbourhood
- Number of reviews
- Minimum nights

Key Model Features:
- Train RMSE -  51.51
- Test RMSE - 51.53
- Cross Validation RMSE - 51.53

Remarks:
- Higher the minimum nights, lesser the price
- The prices are very low for shared rooms
- Neighbourhood centrum west has higher prices

### Ridge Regression
Ridge Regression yields a RMSE score of 53 for Entire Apt and 42 for Private Room 

Important Predictors:
Split the model based on room type
- Neighbourhood
- Number of reviews
- Minimum nights

Key Model Features:
Entire Home/Apt:
Train RMSE -  53.68
Test RMSE - 54.02
Cross Validation RMSE - 53.07 (alpha = 0.89)

![image](https://user-images.githubusercontent.com/20616274/128672187-a369c0ea-9500-4411-b765-fb5187272a6a.png)


Private Room:
Train RMSE -  39.96
Test RMSE - 42.55
Cross Validation RMSE - 38.64 (alpha = 0.95)

![image](https://user-images.githubusercontent.com/20616274/128672203-c20a43c8-fcee-4034-a1e9-3dbabee17648.png)


Remarks:
- Provide a grid for alpha values
- Choose the model with least cross validation rmse
- Repeat the same for entire home/apt and private room


## Business Impact

Metric
Calculation
Predicted price of the listing
x = y_pred  - RMSE 
(removing RMSE for conservative approach)

$x aggregated for listings with 
their actual price < x
(potentially underpriced listings)
$11,865 
(underpriced listings in test data - revenue)

Number of Potentially underpriced listings
654 
(unique low priced listings in test data)

Profit per underpriced listing per day
$18.14

Average occupancy days per underpriced listing per month
18 
(from average reviews per month and minimum nights)

Average occupancy days per underpriced listing per year
216

Profit per year per underpriced  listing
$3919 (occupancy days per year * profit per listing)

Assuming 50 % is the true profit
$1959 (Removing some additional costs)

### The model drives ~$2000 per year per listing if prices are optimized

