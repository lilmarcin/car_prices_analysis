# Car prices analysis

## Project Description

The project involves the analysis of a dataset related to car sales in Poland. The dataset contains information about prices, brands, models, production years, engine power, and various other car features. link to download [car dataset](https://www.kaggle.com/datasets/bartoszpieniak/poland-cars-for-sale-dataset/data)
 

## Project Objective

The main goal of the project is to analyze the data and create visualizations to understand the characteristics of the car market in Poland. Various aspects are explored, such as brand popularity, the the relationship between production year and price, impact of transmission type on price and more.

## Tools Used

- Python
- Libraries like Pandas, Matplotlib, Seaborn
- Jupyter Notebook

## Analysis Summary

During the data analysis, the following operations were conducted:

1. Remove duplicates, zeros and NaN values.
These rows has too many nulls and will not be included in the analysis
- Vehicle_version             70222
- Vehicle_generation          60444
- CO2_emissions              114257
- Drive                       15076
- Origin_country              89992
- First_owner                143210
- First_registration_date    121859

These rows has small amount of nulls, and null data with nulls will be trimmed (less than 1% of all)
- Mileage_km                    983
- Power_HP                      643
- Displacement_cm3             1966
- Transmission                  479
- Doors_number                 1487

![](/images/nulls.png)

2. See the data describe
`df.describe().round(2)`
![](/images/data_describe.png)
- The average price of the car is 61.000 PLN, the average year of production is 2012, the average mileage is 151.000km, the average engine power is 150HP and the displacement is 1.882cm^3

3. Some prices are in EUR, so we need to exchange EUR to PLN (1 EUR = 4.46 PLN)
`print(df['Currency'].value_counts())`
```
PLN    203814
EUR       246
Name: Currency, dtype: int64
```
`df.loc[df['Currency'] == 'EUR', 'Price'] *= 4.46`
4. Removal of outliers in car prices to achieve a more even price distribution.
- Some prices or power engines are high, but there are unique cars like Bentley, Lamborghini, Rolls-Royce etc. Some of the vehicles are new and have a mileage of less than 10 km, some have over 2 000 000 km. Power_HP has range from 30KM to 1300 KM, and some vehicles have more than 5 doors, so we wiil remove these rows.
- let's remove vehicles manufactured before 1995, because many of them are classics and their price may vary, depending on the condition.

In conclusion, we have 199 772 records
5. Analysis of relationships between different features, such as prices, brands, engine power, engine displacement, production year, etc.
> Top selling brands

|         | Brand           | Number of sold    |
| ------- | --------------- | ----------------- |
| 1       | Volkswagen      | 17,778  (8,90%)   |
| 2       | Opel            | 16,061  (8,04%)   |
| 3       | BMW             | 16,028  (8,03%)   |
| 4       | Audi            | 16,019  (8,02%)   |
| 5       | Ford            | 15,714  (7,87%)   |
| 6       | Mercedes-Benz   | 10,686  (5,35%)   |
| 7       | Renault         | 10,472  (5,24%)   |
| 8       | Toyota          | 10,081  (5,04%)   |
| 9       | Škoda           | 10,024  (5,02%)   |
| 10      | Peugeot         | 8,843   (4,44%)   | 
	
![](/images/sales_number_brands.png)

> Average price for a given brand
![](/images/most_expensive_brand.png)
- Mercedes-Benz, BMW and Audi are the most expensive
- Mid-class cars are Volkswagen, Ford, Toyota and Škoda 
- Cheaper cars (compared to other brands) are Opel, Renault, Peugot

> Most purchased car year
![](/images/most_purchased_car_year.png)
- People mostly bought the newest cars
- There is also a tendency to buy 4-5 year old cars.
- You can also see a large number of cars sold that are between 8 and 14 years old.

> Most purchased fuel type for a given brand
![](/images/top10brand_car_sold_by_fuel_type.png)

|         | Fuel type       | % of sold   |
| ------- | --------------- | ------------|
| 1       | Gasoline        |   47.35     |
| 2       | Diesel          |   45.35     |
| 3       | Gasoline + LPG  |    4.42     |
| 4       | Hybrid          |    2.85     |
| 5       | Gasoline + CNG  |    0.03     |
| 6       | Hydrogen        |    0.00     |
| 7       | Ethanol         |    0.00     |


> Average car price by fuel type
![](/images/top10_car_price_fuel_type.png)
Price for Diesel or Gasoline are equal. For hybrid you should pay the most. You will pay much less for cars with Gasoline + LPG or Gasoline + CNG.

> Number of sold transmission type by brand
![](/images/top10_count_transmission_type.png)
- Audi BMW and Mercedes-Benz sell more automatics than manuals. In the case of the rest of the cars, the manual type is more often sold.

> Price vs transmission type
![](/images/top10_car_price_transmission_type.png)
- high-class cars (Audi, BMW, Mercedes-Benz) with automatic transmission are up to 4 times more expensive than cars with manual transmission
- for rest brands automatic transmission is 2-3 times more expensive as a manual

6. Correlation matrix - relationships between variables
- Price are mostly correlated with production year, Power_HP and displacement_cm3 (which is correlated with horse power)
![](/images/corr_matrix.png)

> Price vs year of production for a given brand
![](/images/top10brand_price_vs_year_production.png)ear of production
- the newer the car, the more expensive it is
- the most frequently purchased old cars (> 10 years old) are BMW and Mercedes-
- the most frequently sold cars are up to 5 years old are Volkswagen, Opel, BMW, Audi, Mercedes-Benz, Škoda
- Mercedes cars drop the least in price
> Price vs engine power
![](/images/top10brand_price_vs_horse_power.png)

> Engine power vs engine displacement
![](/images/top10brand_engine_power_vs_engine_displacement.png)

| Vehicle_brand   | Power_HP | Displacement_cm3 |
| --------------- | -------- | -----------------|
| Audi            | 195.0    | 2218.0           |
| BMW             | 209.0    | 2326.0           |
| Ford            | 141.0    | 1795.0           |
| Mercedes-Benz   | 210.0    | 2478.0           |
| Opel            | 123.0    | 1603.0           |
| Peugeot         | 120.0    | 1593.0           |
| Renault         | 116.0    | 1519.0           |
| Toyota          | 123.0    | 1745.0           |
| Volkswagen      | 131.0    | 1744.0           |
| Škoda           | 125.0    | 1553.0           |


- the greater the engine power, the greater the engine displacement
- for Mercedes-Benz, Audi and BMW, the average engine power is 200 HP and engine displacement above 2200 cm^3
- for Ford, the average engine power is 141 KM, and engine displacement  ~1800 cm^3
- for Opel, Peugeot, Renault, Toyota, Volkswagen and Škoda, the average engine power is ~120 HP and engine displacement around 1500-1800 cm^3

7. Conclusions


> Most sold model by top 10 brand

| Vehicle Brand     | Model   | Price (PLN) | Year | Condition | Fuel Type | Displacement (cm^3) | Power (HP) | Mileage (km) | Transmission  | Colour   |
|-------------------|---------|-------------|------|-----------|-----------|----------------------|------------|--------------|--------------|----------|
| Volkswagen        | T-Cross | 98900.0     | 2021 | New       | Gasoline  | 999.0                | 110.0      | 5.0          | Automatic    | White    |
| Opel              | Astra   | 67990.0     | 2019 | Used      | Gasoline  | 1399.0               | 150.0      | 61000.0      | Manual       | Gray     |
| BMW               | Seria 3 | 220100.0    | 2020 | New       | Diesel    | 1995.0               | 190.0      | 5.0          | Automatic    | White    |
| Audi              | A3      | 116400.0    | 2021 | New       | Gasoline  | 999.0                | 110.0      | 5.0          | Automatic    | Black    |
| Ford              | EcoSport| 82900.0     | 2021 | New       | Gasoline  | 998.0                | 125.0      | 5.0          | Manual       | Silver   |
| Mercedes-Benz     | GLC     | 349000.0    | 2019 | New       | Gasoline  | 2996.0               | 367.0      | 1.0          | Automatic    | White    |
| Renault           | Clio    | 34700.0     | 2016 | Used      | Gasoline  | 1149.0               | 73.0       | 96638.0      | Manual       | White    |
| Toyota            | Auris   | 50000.0     | 2017 | Used      | Hybrid    | 1798.0               | 135.0      | 213560.0     | Automatic    | White    |
| Škoda             | Octavia | 110499.0    | 2021 | New       | Gasoline  | 1498.0               | 150.0      | 10.0         | Manual       | Black    |
| Peugeot           | 1007    | 8500.0      | 2006 | Used      | Gasoline  | 1587.0               | 109.0      | 144000.0     | Automatic    | Blue     |

- New models (from 2021) are sold most often. mainly gasoline cars dominates. Toyota sold the most Hybrid cars.
- Mileage: Due to new cars, mileage is low.
- Transmission: mostly automatic.
- Colors are subdued, white, gray and black. Only Peugeot sold the most blue cars.
- There is a tendency to buy economical cars that consume little fuel due to their small capacity and engine power. Engine displacement is from 1000 to 1700 cm^3 and engine power is 110-150 HP.

> Average sold car by top 10 brand

| Vehicle Brand     | Price (PLN) | Year | Condition | Fuel Type | Displacement (cm^3) | Power (HP) | Mileage (km) | Transmission | Colour   |
|-------------------|-------------|------|-----------|-----------|---------------------|------------|--------------|--------------|----------|
| Volkswagen        | 51 378      | 2011 | Used      | Diesel    | 1744                | 131        | 168 461      | Manual       | Black    |
| Opel              | 32 006      | 2011 | Used      | Gasoline  | 1602                | 123        | 61 000       | Manual       | Silver   |
| BMW               | 90 350      | 2012 | Used      | Diesel    | 2325                | 209        | 155 629      | Automatic    | Black    |
| Audi              | 84 623      | 2011 | Used      | Diesel    | 2218                | 195        | 166 426      | Automatic    | Black    |
| Ford              | 46 398      | 2012 | Used      | Diesel    | 1794                | 141        | 144 353      | Manual       | Black    |
| Mercedes-Benz     | 99 147      | 2011 | Used      | Diesel    | 2478                | 210        | 150 714      | Automatic    | Black    |
| Renault           | 34 567      | 2012 | Used      | Gasoline  | 1519                | 116        | 137 445      | Manual       | Black    |
| Toyota            | 49 117      | 2012 | Used      | Gasoline  | 1745                | 123        | 127 666      | Manual       | Silver   |
| Škoda             | 53 476      | 2014 | Used      | Gasoline  | 1552                | 131        | 125 138      | Manual       | Black    |
| Peugeot           | 40 714      | 2012 | Used      | Diesel    | 1593                | 125        | 138 303      | Manual       | Black    |

- Condition: Used - The most commonly sold cars are 10 years old models. The average price is ~60 000 PLN.
- Fuel Type: in the case of gasoline and diesel, it is about equal in the number of cars sold
- Engine Displacement: Engine variants with a displacement ranging from approximately 1500 cm^3 to 1800 cm^3 dominate the sales. This range encompasses most passenger cars. For Audi, BMW and Mercedes-Benz displacement is around 2300 cm^3.
- Horsepower: Engine power options ranging from approximately 120 HP to 140 HP are the most popular. Only Mercedes-Benz, Audi and BMW sold cars with more than 200 HP.
- Mileage: The mileage typically averages around 125 000 km, so it is pretty good for 10 years old cars.
- Transmission: Manual is the most frequently chosen type of transmission. For cars with over than 190 HP, people buy automatic transmission.
- Color:  Dominant color is black, only silver is for Toyota and Opel.