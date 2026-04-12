# 🍔 Swiggy Data Analysis Dashboard

---

## 📑 Table of Contents

1. Project Overview  
2. Dataset Description   
3. Data Preparation & Transformations  
4. DAX Measures  
5. Key KPI Measures  
6. Branch / Location Measures  
7. Dashboard Pages & Visualizations     
8. Drill-Down & Interactivity  
9. Performance Optimization  
10. How to Reproduce / Deliverables  
11. Business Insights
12. Conclusion
13. Dashboard Images

---

# 📌 1. Project Overview

This project analyzes food delivery data from Swiggy to uncover insights related to:

- 🍽️ Order trends  
- 💰 Revenue performance  
- 📍 Location-based demand  
- ⏱️ Delivery behavior  

### 🎯 Objective:
To improve **delivery efficiency, customer satisfaction, and revenue optimization** using data analytics.

---

# 📊 2. Dataset Description

The dataset contains food delivery transaction data:

| Column Name        | Description |
|-------------------|------------|
| Order_ID          | Unique order identifier |
| Order_Date        | Date of order |
| Order_Time        | Time of order |
| Customer_ID       | Unique customer identifier |
| Restaurant_Name   | Restaurant name |
| Cuisine           | Type of food |
| Order_Value       | Total order amount |
| Delivery_Time     | Delivery duration |
| Delivery_Status   | Delivered / Cancelled |
| Payment_Mode      | Online / Cash |
| City              | Order location |

---

---

# 🧹 3. Data Preparation & Transformations

## Step 1: Data Cleaning
- Removed null values  
- Removed duplicate records  
- Standardized column names  

---

## Step 2: Data Type Conversion
- Converted Order_Date & Order_Time to datetime  
- Ensured numeric columns (Order_Value, Delivery_Time)  

---

## Step 3: Feature Engineering

### Extract Date Components
```python id="s1"
df['Year'] = df['Order_Date'].dt.year
df['Month'] = df['Order_Date'].dt.month
df['Day'] = df['Order_Date'].dt.day_name()

```
### Extract Hour
df['Hour'] = pd.to_datetime(df['Order_Time']).dt.hour
## Step 4: Create Day / Night Flag
df['Day_Night'] = df['Hour'].apply(lambda x: 'Day' if 6 <= x < 18 else 'Night')
## Step 5: Data Validation
- Checked delivery time consistency
- Verified order values

--
## 📐 4. DAX Measures (Power BI)
- ### Total Orders
Total Orders = COUNT('Swiggy'[Order_ID])
- ### Total Revenue
Total Revenue = SUM('Swiggy'[Order_Value])
- ### Average Order Value
Avg Order Value = AVERAGE('Swiggy'[Order_Value])
- ### Cancellation Rate
Cancellation Rate = 
DIVIDE(
    COUNTROWS(FILTER('Swiggy','Swiggy'[Delivery_Status]="Cancelled")),
    COUNT('Swiggy'[Order_ID])
)

--

# 📊 5. Key KPI Measures
- 📦 Total Orders
- 💰 Total Revenue
- 📉 Average Order Value
- ❌ Cancellation Rate
- ⏱️ Average Delivery Time

 --
 
 # 📍 6. Location-Based Measures
- ### Orders by City
City Orders = COUNT('Swiggy'[City])
- ### Revenue by City
City Revenue = SUM('Swiggy'[Order_Value])

--

# 📊 7. Dashboard Insights: Chart-by-chart analysis

## A)Excel:

### 1)Chart Type: Column chart
- Insight: Count of orders by city
- Minimum count of orders : 14914 and City : Pune
- Maximum count of orders : 25022 and City : Bangalore


### 2) Chart Type Column chart
- Insight: Delivery fee vs discount applied
- Minimum delivery fee :897388.94, City : Pune
- Maximum delivery fee:1498608.87, City : Bangalore
- Minimum discount applied:1192645.23, City: Pune
- Maximum discount applied:2018314.98, City: Bangalore

### 3) Chart Type: Bar chart
- Insight: Discount applied by payment mode
- Minimum discount applied:2398569.91, Payment mode: UPI
- Maximum discount applied :3221865.94, Payment mode: Card
 
### 4) Chart Type: Pie chart
- Insight: Payment mode distribution
- Minimum count :29825(29.83%),Payment mode: Cash
- Maximum count:40240(40.24%),Payment mode: Card
 
### 5) Chart Type: Bar chart
- Insight: Order count by cuisine type
- Minimum order count :19812,Cuisine type: South Indian
- Maximum order count:20188, Cuisine type: Fast Food

### 6) Chart Type: Pie chart
- Insight: Count of prepaid
 - Yes:49935(50%)
 - No:5006(50%)

### 7) Chart Type: Column chart
- Insight: Revenue by city
- Minimum revenue: 11627648.33 ,City: Pune
- Maximum revenue:19605812.11, City: Bangalore

### 8) Chart Type: Clustered bar chart
- Insight: Sum of rider and user rating by city
- Minimum rider rating: 63350.7,City: Pune
- Maximum rider rating:106446.1, City: Bangalore
- Minimum user rating: 63383.9 ,City: Pune
- Maximum user rating:106333.4, City: Bangalore

### 9) Chart Type: Column chart
- Insight: Item count by cuisine type
- Minimum item count: 59276, Cuisine type: South Indian
- Maximum item count: 60576 ,Cuisine type: Fast Food

---

## B)Microsoft Power Bi:
### Dashboard Objective:
#### To provide a comprehensive view of Swiggy's business performance by analyzing customer orders, delivery efficiency, restaurant ratings, and city-wise trends to support operational and strategic decision-making.

### 1) Chart Type: Bar chart
- Insight: Order id count by city
- Minimum order count :11922905 and City: Pune
- Maximum order count:20125518 and City: Bangalore

### 2) Chart Type: Area chart
- Insight: Order id count by year and month
- Minimum order count :3129 ,Year : 2024, Month: June
- Maximum order count :8593,Year : 2025, Month: March

### 3) Chart Type: Stacked Bar chart
- Insight: Orders count by cuisine type and city 
- Minimum order count :2878,City : Pune, Cuisine type: South Indian
- Maximum order count :5059,City :Bangalore, Cuisine type: Fast Food

### 4) Chart Type: Pie chart
- Insight: Payment mode distribution
- Minimum count :29825(29.83%),Payment mode: Cash
- Maximum count:40240(40.24%),Payment mode: Card
 
### 5) Chart Type: Bar chart
- Insight: Avg discount applied by city 
- Minimum avg discount :79.82 ,City : Delhi
- Maximum avg discount : 80.66,City :Bangalore

### 6) Chart Type: Donut chart
- Insight: Count of is prepaid by payment mode
- Minimum count of is prepaid :29825(29.83%),Payment mode: Cash
- Maximum count of is prepaid :40240(40.24%),Payment mode: Card


### 7) Chart Type: Stacked bar chart
- Insight: Rider rating and user rating by city
- Minimum sum of rider rating:63350.70, City:Pune
- Maximum sum of rider rating:106446.10,City:Bangalore
- Minimum sum of user rating:63383.90, City:Pune
- Maximum sum of user rating:106333.40,City:Bangalore


### 8) Chart Type: Column chart
- Insights: Count of peak hour by  city
- Minimum peak hour count:14914,city:Pune
- Maximum peak hour count:25022,city:Bangalore

### 9) Chart Type: Donut chart
- Insights: Count of order id by year
- Minimum count of order: 46482(46.48%),year: 2025
- Maximum count of order53518(53.52%),year:2024

### 10) Chart Type: Treemap chart
- Insights: Revenue by city
- Minimum revenue:11627648.33, City: Pune
- Maximum revenue:19605812.11, City: Bangalore

### 11) Chart Type: Bar chart
- Insights: Count of prepaid by city
- Minimum prepaid count: 14914 , City: Pune
- Maximum peak hour count:25022, City: Bangalore

### 12) Chart Type: Clustered column chart
- Insights: sum of delivery fee and sum of discount applied by city
- Minimum delivery fee:897388.94 , City: Pune
- Maximum delivery fee :1498608.87, City: Bangalore
- Minimum discount applied:1192645.23, City: Pune
- Maximum discount applied : 2018314.98, City : Bangalore

### 13) Chart Type: Column chart
- Insights: Count of order by peak hour
- Minimum count of orders: 41959, Peak hour: Y
- Maximum count of orders: 58041, Peak hour: N

### 14) Chart Type: Donut chart
- Insights: Cuisine type distribution
- Minimum cuisine count: 19812(19.81%) , Cuisine type: South Indian
- Maximum cuisine count: 20188(20.19%), Cuisine type: Fast Food

### 15) Chart Type: Bar chart
- Insights: Top 10 high value customers 
- Minimum sum of total amount: 369.34
- Maximum sum of total amount:1469.02


---

## C) Tableau Public Edition 

### 1) Chart Type: Bar chart
- Insight: Order id count by city
- Minimum order count :11922905 and City: Pune
- Maximum order count:20125518 and City: Bangalore

### 2) Chart Type: Line chart
- Insight: Order id count by year and month
- Minimum order count :3129 ,Year : 2024, Month: June
- Maximum order count :8593,Year : 2025, Month: March

### 3) Chart Type: Column chart
- Insight: Sum of delivery fee by city
- Minimum delivery fee: 897389, City : Pune
- Maximum delivery fee : 1498609, City: Bangalore

### 4) Chart Type: Packed bubbles
- Insight: City wise avg user rating
- Minimum user rating: 4.2475 (19.99%), City: Hyderabad
- Maximum user rating: 4.2520(20.01%), City: Mumbai

### 5) Chart Type: Bar chart
- Insight: Top 10 high value customers by city
- Minimum amount : 1577.17, City: Delhi
- Maximum amount: 1591.72, City: Pune

### 6) Chart Type: Treemap chart
- Insight: City wise total amount
- Minimum amount: 11627648, City : Pune
- Maximum amount: 19605812, City: Bangalore

### 7) Chart Type: Pie chart
- Insight: Cuisine type distribution 
- Minimum sum of orders: 15856373, Cuisine type: South Indian
- Maximum sum of orders : 16211624, Cuisine type: Fast Food

### 8) Chart Type: Bar chart
- Insight: Top 10 restaurant by order value
- Minimum order value: 1499.8300
- Maximum order value :1500.0000

### 9) Chart Type: Pie chart
- Insight: Count of order id by peak hour
- Yes : Count of order value : 41959, Order value : 33738899
- No : Count of order value:58041, Order value : 46441293

### 10) Chart Type: Packed bubbles
- Insight: City wise avg rider rating
- Minimum avg rider rating: 4.2477, City : Pune
- Maximum avg rider rating: 4.254100 , City : Bangalore 


# 🔍 8. Drill-Down & Interactivity
### Drill-Down:
- Year → Month → Day
- City → Restaurant
### Filters:
- Date
- City
- Cuisine
### Interactivity:
- Cross-filtering
- Dynamic visuals

---


# ⚡ 9. Performance Optimization
- Removed unnecessary columns
- Optimized DAX calculations
- Reduced visuals per page

---

# 🚀 10. How to Reproduce / Deliverables
### Steps:
- Load dataset into Power BI / Tableau
- Clean and transform data
- Create calculated columns
- Build dashboard

### 📦 Deliverables
- ✅ Power BI Dashboard (.pbix)
- ✅ Tableau Dashboard (.twbx)
- ✅ Dataset
- ✅ Insights

--- 

# 📈 11. Business Insights & Recommendations

- 📊 Key Insights
- 🍽️ Peak orders during evening hours
- 📍 Certain cities generate higher revenue
- ❌ Cancellations higher during peak time
- ⏱️ Delivery delays impact customer satisfaction

---

# ⭐12. Conclusion

This project demonstrates:

- End-to-end food delivery data analysis
- Dashboard creation using Power BI & Tableau
- Strong business insight generation

