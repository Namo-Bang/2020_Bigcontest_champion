# 2020_Bigcontest_champion
## __2020 BigContest Champion League Finalist__

__TEAM 데이터 공방__

Team member: Namo Bang, Ayoung Jo, Dongyeon Keum, Sanghyun Park

Assistant: Gaeun Sung

*Beacause of security rule, I cannot open data and full codes uesd in this proj*

## Goal of Competition
Using 2019 sales data to predict your handling amount for June 2020

## Engineering Environment
module|version
---|---
tensorflow|2.2.x
catboost|0.24.1
pandas|1.2.0
numpy|1.19.2

## Feature
feature|description
---|---
Broadcast date and time|product broadcast date and time
Exposure (minutes)|Product broadcast duration
Mother Code|A code containing brand and product classification information
Product Code|A code containing detailed product classification information
Product name|Product name (optional information such as product name, sales method, set availability, etc.)
Product group|The name of the major product group
Unit of sale price|list price of each product
Handling amount|Total sales for each product during the broadcast time (unit selling price X order quantity)

## External data
Because the sales performance of home shopping is highly affected by the weather, weather data from the Meteorological Administration was additionally used. In addition, Naver shopping trend data was also used to reflect in the model which items consumers are interested in by period.

## Mother Code & Product Code Target Embedding
When considering the deep learning model, the dimension of the data becomes too large when one-hot encoding of the categorical variable mother code and product code, so the two variables were converted in a similar manner to Target Embedding using the average of 2019 performance.

## Model Stacking
We tried a number of algorithms, among which CatBoost predicted high for a few specific products, DNN found a tendency to predict conservatively as a whole.

![image](https://user-images.githubusercontent.com/48271454/105502911-5067c980-5d09-11eb-8796-2222cafab5ec.png)

So we tried to combine the two models.

### Model structure
![image](https://user-images.githubusercontent.com/48271454/105503294-be13f580-5d09-11eb-9b5f-3d21b5545441.png)

## Mapping Algorithm
Since the train data is from 2019 and the test data is from 2020, many products in the test data were products that are not in the train data. So, an algorithm was needed to map new products to similar existing products. After tokenizing the product name, we constructed the jacarrd similarity-based algorithm and the simple intersection-based algorithm, and as a result, we adopted the intersection-based algorithm with better performance.

>Products with a history of sales in the past → mapping based on product code
>If there is a sales history of products with the same mother code in the past → Mapping to products with similar prices and similar names among products with mother codes
>If the two above are not applicable → Mapping to products with similar names among products in the same product group with similar price points

## Result
We 데이터 공방 made it to the finalists of 16 teams, but unfortunately, we did not win the award. The reason for the defeat seems to be that the business improvement part using the last model and analysis result was very poor. However, it was a very good experience to have this level of achievement and experience as a non-major in the first challenged competition.
