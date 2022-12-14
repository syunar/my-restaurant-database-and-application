
# My Restaurant Database and Application

Before using data science to help your business the most important thing should be the data right?, So I create the application that collects the transaction and then connects to the database, ER Diagram, Data model design, and Query will use here.

So this project is like Phase 1 to collect the data and then in Phase 2, I will use this data to analyze the customer behavior e.g. customer segmentation and contextual marketing, analyze the products, etc. the point is to maintain and increase customers and sales.
 
![Cover](https://github.com/syunar/my-restaurant-database-and-application/blob/ff9206a62f63902bf6912fcd1c8a39318ae8745b/cover.jpg)
 
## Authors

- [@fronksupakorn](https://github.com/syunar)


## Project's Goals
- to reduce the time for order capturing
- to reduce workload from duplicate workflow
- to collect the transaction data to the database
## Dependencies

- Google Sheet
    - use as the database
    - design data model & ER Diagram
    - query the data from the database to show on the application
- AppSheet (tl;dr No code, Low code platform by Google to deploy application)
    - connect to database / CRUD (create, read, update, delete)
    - to deploy the application
    
![erdia](https://github.com/syunar/my-restaurant-database-and-application/blob/ee91c906490aba709d69586cc95319bc68c8d9c0/ER_diagram.jpg)

## Features

On the application we have 5 menus here:
- Invoice
    - select the date you want and then
    - automatically generate invoices in PDF format
- Summary
    - to show the number of orders in each menu
    - so we can use to buy the raw materials and ingredients 
- Orders
    - add/edit/delete the orders
    - invoice button to generate the invoice by individual order
    - check the delivery status
    - check the payment status
- Menu
    - add/edit/delete the menus or products
    - have "open" and "close" status so when you add orders it will show only "open" menu
- Customers
    - add/edit/delete the customers

## Usage/Examples
### 1. Add some orders
![ex1](https://github.com/syunar/my-restaurant-database-and-application/blob/8f7f30e768d9e2f15129ba2c539252585e70fbf3/ex1.png)
### 2. Check the total sum orders to buy the raw material
This will show value count of product_name group by order_date on the googlesheet formula
```googlesheet
=QUERY(
    {OrderDetails!A1:D1,
    "delivery_date",
    "product_name",
    "category",
    "price";
    OrderDetails!A2:D,
    ARRAYFORMULA(
        IFERROR(VLOOKUP(OrderDetails!B2:B, Orders!$A:$D,4,0), "")),
    ARRAYFORMULA(
        IFERROR(VLOOKUP(OrderDetails!C2:C, Products!$A:$E,{2,3,4}, 0), ""))
    },
    
    "Select Col5,
            Col6,
            Col8, 
            SUM(Col4),
            Col8*SUM(Col4)
    WHERE Col5 is not null 
    GROUP BY Col5, Col6, Col8 
    LABEL Col8*SUM(Col4) 'total_prices'", 1)
```
![ex2](https://github.com/syunar/my-restaurant-database-and-application/blob/5808e333ddd65f4a7c9aa7c44419aa2c16076914/ex2.png)
### 3. Export invoice in PDF format
![ex3](https://github.com/syunar/my-restaurant-database-and-application/blob/814f853cb817917b725fce19fd0fde7fe1e80f5f/ex3.png)
### 4. Update Delivery & Payment Status
If you click on those 2 buttons, will have small icon appear in front of the row which means this order has already delivered or paid

![ex4](https://github.com/syunar/my-restaurant-database-and-application/blob/211dab8498be5c6c91341c8f8dd355c60425f594/ex4.png)
