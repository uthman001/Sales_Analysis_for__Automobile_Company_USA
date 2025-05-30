  # Sales_Analysis_for__Automobile_Company_USA
A Data Science Project that Analysed  the sales performance of an Automobile company Based in the United States. The company’s sales transaction data generated over the past years was used for this  analysis.

##  PROBLEM STATEMENT
What are the Top Most-Profitable 5 States for a Bike business in the United States ?

## DATA PRE-PROCESSING
#### DATA LOADING

## Import all the necessary python packages 
```Python
import numpy as np 
import pandas as pd 
import matplotlib.pyplot as plt

```
#reading the sales data into panda data frame
```Python
bikes_df = pd.read_csv("C:/Users/uthma/OneDrive/Desktop/Data Set/bikes.csv")

bikes_df.head()
```
![Panda_Sreenshot](https://github.com/user-attachments/assets/e4ed211a-b883-44b0-b646-cdb49b7ead41)


## Data Modification
```Python
#Adding the following 3 columns to your pansdas Dataframe:  bikes_df
# TotalCostPrice : To be obtained by (OrderQuantity x CostPrice_usd)


bikes_df["TotalCostPrice"] = bikes_df["OrderQuantity"] * bikes_df["CostPrice_usd"] 


# SalesRevenue : To be obtained by (OrderQuantity x SellingPrice_usd)


bikes_df["SalesRevenue"] = bikes_df["OrderQuantity"] * bikes_df["SellingPrice_usd"] 



# Profit : To be obtained by (SalesRevenue - TotalCostPrice)



bikes_df["Profit"] = bikes_df["SalesRevenue"] - bikes_df["TotalCostPrice"]


bikes_df.head()


```
![Data modification Screenshot](https://github.com/user-attachments/assets/16824235-2fc1-4c80-b1f1-91ce98ea7ee5)

## DATA ANALYSIS
```Python
#Filtering out only the data relevant to solve the problem statements

IS_USA = bikes_df["CustomerCountry"] == "United States"
For_bk = bikes_df["ProductCategory"] == "Bikes"
bikes_df[(IS_USA) & (For_bk)].head()


```
![Data Analysis Screenshot](https://github.com/user-attachments/assets/d0d4fe55-201d-410e-a32b-ce88a6e1f30b)

#### DATA AGGREGATION
```Python
For_bk_in_USA = bikes_df[(IS_USA) & (For_bk)].pivot_table(values = "Profit",index = "CustomerState", aggfunc = np.sum)


For_bk_in_USA

```

![Data Aggregation](https://github.com/user-attachments/assets/69e48235-21ee-4265-a7df-ef12d66a1549)

#### DATA SORTING
```Python
For_bk_in_USA.sort_values("Profit", ascending = False)
```

![Data sorting screenshot](https://github.com/user-attachments/assets/04f69168-011d-45da-9577-645eeddac372)

#### RESULT
```Python
#Top Most-Profitable 5 States for a Bike business in the United States ?

Top_5_most_profitable_states_us = For_bk_in_USA.sort_values("Profit", ascending = False).head()
Top_5_most_profitable_states_us
```
![Result screenshot](https://github.com/user-attachments/assets/114cd2ff-f648-4a5a-8831-700016054918)

#### DATA VISUALIZATION
```Python
For_bk_in_USA.sort_values("Profit", ascending = False).head(5).plot(kind = "bar", title = "Top 5 Most-Profitable States for a Bike business in the United State")

#lebel
plt.xlabel("CustomerState")
plt.ylabel("Profit") 

plt.show()
```

![Project_1_screenshot](https://github.com/user-attachments/assets/07fa9c1b-0e19-48dc-8c0c-cb08c552074b)
