
# 🚀 Blinkit Sales & Consumer Analytics  
**Data Analysis Python Project**

---

## 📌 Table of Contents  
- [Overview](#overview)  
- [Technologies & Tools](#technologies--tools)  
- [Getting Started](#getting-started)  
- [Usage](#usage)  
- [Project Structure](#project-structure)  
- [Key Findings](#key-findings)  
 

---

## 🧐 Overview  
This project analyses the sales and consumer ratings data from the ‎Blinkit delivery platform (dataset: `blinkit_data.csv`) using Python.  
The goal is to derive business-relevant insights — e.g., total sales, average sales, average ratings, sales distribution by item type, fat content, outlet size/location — and visualise them with charts.

---

## 🛠 Technologies & Tools  
- Python 3.12  
- pandas  
- numpy  
- matplotlib  
- seaborn  
- Jupyter Notebook 

---

## 🧭 Getting Started  
1. Clone this repository:  
 git clone https://github.com/azmisultana/Blinkit-Sales-Consumer-Analytics-Python-Project.git
cd blinkit-analysis
  
2. Set up Environment:

Python ≥ 3.12

Install libraries:

pip install pandas, numpy, matplotlib, seaborn  

3. 💾 Dataset
File: blinkit_data.csv

Location:"C:/Users/Saidul/OneDrive/Documents/Blinkit Python Project Data/blinkit_data.csv"

Source: 

---

## 📊 Project Workflow
### 1️⃣ Import Libraries


    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    import seaborn as sns

### 2️⃣ Load Data

    df = pd.read_csv("C:/Users/Saidul/OneDrive/Documents/Blinkit Python Project Data/blinkit_data.csv")

### 3️⃣ Initial Exploration
- View first & last 10 rows

      df.head(10)
      df.tail(10)

- Check shape, columns & Data Types

      print("Size of the Data:", df.shape)
      df.columns
      df.dtypes


### 4️⃣ Data Cleaning
- Standardize 'Item Fat Content'

    - ➡️ Replacing ‘LF’, ‘low fat’, ‘reg’ with clean labels


          print(df['Item Fat Content'].unique())


          df['Item Fat Content'] = df['Item Fat Content'].replace({'LF':'Low Fat','low fat': 'Low Fat','reg': 'Regular' }) 

- Check for missing or unique values


### 5️⃣ Business Requirements / KPIs
- 📈 Total Sales

      total_sales = df['Sales'].sum()
      print(f"Total Sales: ${total_sales:,.01f}")

- 📉 Average Sales

      avg_sales = df['Sales'].mean()
      print(f"Average Sales: ${avg_sales:,.01f}")

- 🧮 Number of Items Sold

      no_of_items_sold = df['Sales'].count()
      print(f"No. of Items Sold: {no_of_items_sold:,.01f}")

- ⭐ Average Ratings

      avg_rating =df['Rating'].mean()
      print(f"Average Ratings: {avg_rating:,.01f}")

### 6️⃣ Visualization & Analysis
- 🥧 Total Sales by Fat Content

      sales_by_fat = df.groupby('Item Fat Content')['Sales'].sum()

      plt.pie(sales_by_fat, labels=sales_by_fat.index,
        autopct = '%.1f%%',
       startangle = 90)
      plt.title('Sales by Fat Content')
      plt.axis('equal')
       plt.show()

- 🏷️ Total Sales by Item Type

      sales_by_type = df.groupby('Item Type')['Sales'].sum().sort_values(ascending=False)

      plt.figure(figsize=(10,6))
      bars = plt.bar(sales_by_type.index,sales_by_type.values)

      plt.xticks(rotation=-90)
      plt.xlabel('Item Type')
      plt.ylabel('Total Sales')
      plt.title('Total Sales by Item Type')

      for bar in bars:
          plt.text(bar.get_x() + bar.get_width() / 2, bar.get_height(),
             f'{bar.get_height():,.0f}', ha='center', va='bottom', fontsize=7)

      plt.tight_layout()
      plt.show()

- 🏭 Fat Content by Outlet for Total Sales

      grouped = df.groupby(['Outlet Location Type','Item Fat Content'])['Sales'].sum().unstack()
      grouped = grouped[['Regular', 'Low Fat']]

      ax = grouped.plot(kind='bar', figsize=(8,5), title='Outlet Tier by Item Fat Content')
      plt.xlabel('Outlet location Tier')
      plt.ylabel('Total Sales')
      plt.legend(title='Item Fat Content')

      plt.tight_layout()
      plt.show()

- 📆 Total Sales by Year of Outlet Establishment

       sales_by_year = df.groupby('Outlet Establishment Year')['Sales'].sum().sort_index()

       plt.figure(figsize=(9,5))
       plt.plot(sales_by_year.index, sales_by_year.values, marker='o',linestyle='-')

       plt.xlabel('Outlet Establishment Year')
       plt.ylabel('Total Sales')
       plt.title('Outlet Establishment')

       for x, y in zip(sales_by_year.index, sales_by_year.values):
           plt.text(x,y, f'{y:,.0f}', ha='center', va='bottom', fontsize=8)

       plt.tight_layout()
       plt.show()    

- 🏢 Sales by Outlet Size

       sales_by_size = df.groupby('Outlet Size')['Sales'].sum()

       plt.figure(figsize=(4,4))
       plt.pie(sales_by_size, labels=sales_by_size.index,
               autopct = '%1.1f%%',
               startangle=90)
       plt.title('Outlet Size')
       plt.tight_layout()
       plt.show()

- 🌍 Sales by Outlet Location

       sales_by_location = df.groupby('Outlet Location Type')['Sales'].sum().reset_index().sort_values('Sales',ascending=False)

       plt.figure(figsize=(8,3))
       ax= sns.barplot(x='Sales', y='Outlet Location Type', data=sales_by_location)


       plt.xlabel('Total Sales')
       plt.ylabel('Outlet Location Type')
       plt.title('Total Sales by Outlet Location Type')

       plt.tight_layout() #Ensures layout fits without scroll
       plt.show()
---

## 📈 Key Visualizations & Results
- #### Fat Content:

![Image](https://github.com/user-attachments/assets/833d5763-e6be-41d1-b739-dbc9f5ca155e)


- #### Item Type:

![Image](https://github.com/user-attachments/assets/115bfe11-5427-448e-a115-86a2a9725de0)


- #### Location Tier vs Fat Content (Bar)

![Image](https://github.com/user-attachments/assets/e8ec4639-23a4-45e9-9dee-1530f62c0bbc)

- #### Year Established vs Sales (Line)

![Image](https://github.com/user-attachments/assets/c62605d8-48da-42fb-85db-0b2e88887693)

- #### Outlet Size (Pie)

![Image](https://github.com/user-attachments/assets/39cde7cb-91a4-417a-8157-ac2b578b49eb)

- #### Location Type (Bar)

![Image](https://github.com/user-attachments/assets/1bb0053e-0507-419e-8b72-f3bbb2cbba0d)


----

## 🗂 Project Structure

       blinkit-analysis/
       │
       ├── blinkit_data.csv        # Raw data
       ├── Blink it Analysis.ipynb          # Jupyter notebook
       ├── blinkit_analysis.py     # Script for full analysis
       ├── charts/                 # Folder for generated images
       └── README.md               # This file!

## 🔍 Key Findings

- Total Sales: $1,201,681.5

- Average Sales per item: $141.0

- Number of items sold: 8,523.0

- Average consumer rating: 4.0

- Sales by Fat Content: Regular items contributed approx. 35.4%, Low Fat items 64.6%.

- Top-3 selling Item Types (examples): Fruits and Vegetables, Snack Foods, Household.

- Outlet Establishment Year vs Sales: Older outlets (est. earlier years) tend to have higher total sales.

- Outlet Size / Location insights: 

   Sales by Outlet : Size(Small : 37.0%, Medium : 42.3%, High : 20.7%)





