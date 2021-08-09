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
![image](https://user-images.githubusercontent.com/20616274/128670971-f38a8361-d60d-4eb9-89d4-5d73100e0cef.png)

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
![image](https://user-images.githubusercontent.com/20616274/128671453-d6b251e1-4ed2-4603-8bee-44f445a9d30b.png)


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




