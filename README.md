# Data Cleaning & Reporting Automation Project

## Objective

Automate data cleaning and reporting workflows using Python. This project handles missing values, removes duplicates, fixes inconsistent data, generates automated reports, and creates dashboard visualizations.

---

# Python Code

```python
# Import Libraries
import pandas as pd
import matplotlib.pyplot as plt

# -----------------------------
# Create Dataset
# -----------------------------

data = {
    'Order_ID': [
        1001,1002,1003,1004,1005,1006,1007,1008,1009,1010,
        1011,1012,1013,1014,1015
    ],

    'Date': [
        '01-01-2025','02-01-2025','03-01-2025','04-01-2025','05-01-2025',
        '06-01-2025','07-01-2025','08-01-2025','09-01-2025','10-01-2025',
        '11-01-2025','12-01-2025','13-01-2025','14-01-2025','15-01-2025'
    ],

    'Customer_Name': [
        'Ravi','Priya','Kiran','Anu','Suresh',
        'Divya','Ramya','Ajay','Teja','Meena',
        'Ravi','Pooja','Karthik','Sneha','Arjun'
    ],

    'City': [
        'Hyderabad','Vijayawada','Guntur','Tirupati','Visakhapatnam',
        'Hyderabad','Guntur','Vijayawada','Tirupati','Hyderabad',
        'Visakhapatnam','Guntur','Tirupati','Vijayawada','Hyderabad'
    ],

    'Product': [
        'Laptop','Mouse','Keyboard','Monitor','Printer',
        'Tablet','Mouse','Keyboard','Laptop','Monitor',
        'Printer','Tablet','Mouse','Keyboard','Laptop'
    ],

    'Quantity': [
        2,3,1,1,2,
        1,5,2,1,2,
        1,2,4,3,1
    ],

    'Price': [
        50000,500,1500,12000,8000,
        25000,500,1500,55000,12000,
        8500,26000,600,1700,60000
    ]
}

# Create DataFrame
df = pd.DataFrame(data)

# Create Total Sales Column
df['Total_Sales'] = df['Quantity'] * df['Price']

# -----------------------------
# Data Cleaning
# -----------------------------

# Check Missing Values
print("Missing Values:")
print(df.isnull().sum())

# Remove Duplicates
df.drop_duplicates(inplace=True)

# Convert Date Format
df['Date'] = pd.to_datetime(df['Date'], dayfirst=True)

# Check Data Types
print("\nData Types:")
print(df.dtypes)

# -----------------------------
# Data Analysis
# -----------------------------

# Total Sales
total_sales = df['Total_Sales'].sum()

# Average Sales
average_sales = df['Total_Sales'].mean()

# Best Selling Product
best_product = df.groupby('Product')['Quantity'].sum().idxmax()

# Sales by City
city_sales = df.groupby('City')['Total_Sales'].sum()

# Sales by Product
product_sales = df.groupby('Product')['Total_Sales'].sum()

# -----------------------------
# Print Report
# -----------------------------

print("\n========== SALES REPORT ==========")

print("\nTotal Sales:", total_sales)

print("\nAverage Sales:", average_sales)

print("\nBest Selling Product:", best_product)

print("\nSales by City:")
print(city_sales)

print("\nSales by Product:")
print(product_sales)

# -----------------------------
# Export Report
# -----------------------------

# Export Cleaned Dataset
df.to_csv("cleaned_sales_data.csv", index=False)

# Export Excel Report
with pd.ExcelWriter("sales_report.xlsx") as writer:
    df.to_excel(writer, sheet_name='Cleaned Data', index=False)
    city_sales.to_excel(writer, sheet_name='City Sales')
    product_sales.to_excel(writer, sheet_name='Product Sales')

print("\nReports Generated Successfully!")

# -----------------------------
# Dashboard Visualizations
# -----------------------------

# 1. Sales by City
plt.figure(figsize=(8,5))
city_sales.plot(kind='bar')

plt.title("Sales by City")
plt.xlabel("City")
plt.ylabel("Total Sales")

plt.show()

# 2. Sales by Product
plt.figure(figsize=(8,5))
product_sales.plot(kind='pie', autopct='%1.1f%%')

plt.title("Sales by Product")

plt.ylabel("")

plt.show()

# 3. Quantity Sold by Product
quantity_product = df.groupby('Product')['Quantity'].sum()

plt.figure(figsize=(8,5))
quantity_product.plot(kind='line', marker='o')

plt.title("Quantity Sold by Product")
plt.xlabel("Product")
plt.ylabel("Quantity")

plt.grid(True)

plt.show()

# -----------------------------
# Final Dashboard Summary
# -----------------------------

print("\n========== FINAL DASHBOARD ==========")

print("Total Orders:", len(df))

print("Total Revenue:", total_sales)

print("Top Product:", best_product)

print("Top City:", city_sales.idxmax())
```

---


```
```
