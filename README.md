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
- Średnia cena auta wynosi 61 000 PLN, średni rok produkcji wynosi 2012, średni przebieg to 151 000 km, średnia moc silnika to 150 KM, a pojemność 1882 cm^3.

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
|-----------------------------------------------|	
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
![](/images/corr_matrix)

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
7. Conclusion


