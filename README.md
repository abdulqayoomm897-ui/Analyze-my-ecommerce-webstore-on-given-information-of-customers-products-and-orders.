
## 🛒 E-Commerce Store Analysis
📋 Project Overview

This project analyzes an e-commerce webstore using three datasets:

customers.csv → contains customer details

products.csv → contains product information

orders.csv → contains order records

The analysis helps identify customer behavior, sales performance, and revenue insights.

# 📊 Objectives

Find how many customers are repeating in the store.

Identify which product is the top-selling (most sold).

Identify which product should be discontinued (least sold).

Find customers who should get discounts (visited more than 5 times).

Calculate total store income.

Generate yearly and monthly sales reports.

# Key Analysis Steps
1️⃣ Repeating Customers
merged_data = pd.merge(order, customer, on="customer_id", how="left")
order_counts = merged_data["customer_id"].value_counts()
repeating_customers = order_counts[order_counts > 1]
print("Total repeating customers:", len(repeating_customers))

# 2️⃣ Customers with More Than 5 Orders
loyal_customers = order_counts[order_counts > 5]
print("Customers who ordered more than 5 times:")
print(loyal_customers)

# 3️⃣ Least Sold Product
product_sales = order["product_id"].value_counts()
least_sold_product_id = product_sales.idxmin()
least_sold_product = product[product["product_id"] == least_sold_product_id]
print("Least sold product:")
print(least_sold_product)

# 4️⃣ Total Store Income
merged_orders = pd.merge(order, product, on="product_id", how="left")
merged_orders["total_price"] = merged_orders["quantity"] * merged_orders["price"]
total_revenue = merged_orders["total_price"].sum()
print("Total Revenue:", total_revenue)

5️⃣ Yearly Sales Report
merged_orders["order_date"] = pd.to_datetime(merged_orders["order_date"])
yearly_sales = merged_orders.groupby(merged_orders["order_date"].dt.year)["total_price"].sum().reset_index()
yearly_sales.columns = ["Year", "Total_Revenue"]
print(yearly_sales)

# 6️⃣ Monthly Sales Report
monthly_sales = merged_orders.groupby([
    merged_orders["order_date"].dt.year,
    merged_orders["order_date"].dt.month
])["total_price"].sum().reset_index()
monthly_sales.columns = ["Year", "Month", "Total_Revenue"]
print(monthly_sales)

## 📈 Insights

Shows which customers are most loyal.

Identifies underperforming products to discontinue.

Provides total and yearly/monthly revenue for business planning.

#⚙️ Requirements

Install pandas before running:

pip install pandas

💡 Author

## Abdul Qayoom Mangi
AI & Data Science Student @ SMIT Hyderabad
