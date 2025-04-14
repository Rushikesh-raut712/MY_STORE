# MY_STORE Database Schema

This repository contains the database schema for MY_STORE, an online retail clothing store. The database is designed to handle customer information, product management, orders, shopping bags, and various other aspects of an e-commerce platform.

## Database Overview

MY_STORE is a MySQL database that manages an online clothing retail store. It includes tables for customers, products, orders, shopping bags, and various supporting entities like colors, sizes, brands, and categories. The database also features a sophisticated recommendation system that implements "People who bought this also bought this" logic.

## Tables and Relationships

### Core Tables

#### 1. CUSTOMERS
Stores customer information and authentication details.
- `CUSTOMER_ID` (INT, PK): Unique identifier for each customer
- `NAME` (VARCHAR(45)): Customer's full name
- `EMAIL` (VARCHAR(45), UNIQUE): Customer's email address
- `PHONE` (INT(10), UNIQUE): Customer's phone number
- `ADDRESS` (TINYTEXT): Customer's shipping address
- `USERNAME` (VARCHAR(50)): Login username
- `PASSWORD` (VARCHAR(45)): Login password

#### 2. PRODUCTS
Main product information table.
- `PRODUCT_ID` (INT, PK): Unique identifier for each product
- `NAME` (VARCHAR(100)): Product name
- `PRICE` (DECIMAL(10,2)): Product price
- `DESCRIPTION` (TINYTEXT): Product description
- `STOCK_LEVEL` (INT): Current stock quantity
- `GENDER` (ENUM): 'Men', 'Women', or 'Unisex'
- `BRAND_ID` (INT, FK): Reference to BRAND table
- `CATEGORY_ID` (INT, FK): Reference to CATEGORY table
- `MATERIAL_ID` (INT, FK): Reference to MATERIAL table

#### 3. ORDERS
Stores order information.
- `ORDER_ID` (INT, PK): Unique identifier for each order
- `ORDER_DATE` (DATETIME): Date and time of order
- `TOTAL_AMOUNT` (INT): Total order amount
- `ORDER_STATUS` (SET): 'Pending', 'Shipped', 'Delivered', 'Cancelled'
- `PAYMENT_STATUS` (SET): 'Pending', 'Completed', 'Failed', 'Refunded'
- `CUSTOMER_ID` (INT, FK): Reference to CUSTOMERS table

### Supporting Tables

#### 4. Reference Tables
- **COLOUR**
  - `COLOUR_ID` (INT, PK)
  - `COLOUR_NAME` (VARCHAR(50))

- **BRAND**
  - `BRAND_ID` (INT, PK)
  - `BRAND_NAME` (VARCHAR(100))

- **CATEGORY**
  - `CATEGORY_ID` (INT, PK)
  - `CATEGORY_NAME` (VARCHAR(100))

- **SIZE**
  - `SIZE_ID` (INT, PK)
  - `SIZE_LABEL` (VARCHAR(20))

- **MATERIAL**
  - `MATERIAL_ID` (INT, PK)
  - `MATERIAL_NAME` (VARCHAR(100))

### Relationship Tables

#### 5. Product Relationships
- **PRODUCT_COLOUR**
  - Links products with available colors
  - `PRODUCT_COLOUR_ID` (INT, PK)
  - `PRODUCT_ID` (INT, FK)
  - `COLOUR_ID` (INT, FK)

- **PRODUCT_SIZE**
  - Links products with available sizes
  - `PRODUCT_SIZE_ID` (INT, PK)
  - `PRODUCT_ID` (INT, FK)
  - `SIZE_ID` (INT, FK)

### Shopping Bag System

#### 6. BAG and BAG_PRODUCT
- **BAG**
  - `BAG_ID` (INT, PK)
  - `CUSTOMER_ID` (INT, FK, UNIQUE)

- **BAG_PRODUCT**
  - `BAG_PRODUCT_ID` (INT, PK)
  - `BAG_ID` (INT, FK)
  - `PRODUCT_ID` (INT, FK)
  - `QUANTITY` (INT)

### Order Management

#### 7. ORDER_DETAILS
- `ORDER_DETAILS_ID` (INT, PK)
- `QUANTITY` (INT)
- `PRICE_AT_PURCHASE` (DECIMAL(10,2))
- `PRODUCT_ID` (INT, FK)
- `ORDER_ID` (INT, FK)

### Additional Features

#### 8. Returns Management
- **RETURNS**
  - `RETURN_ID` (INT, PK)
  - `RETURN_REASON` (VARCHAR(100))
  - `RETURN_STATUS` (SET)
  - `PRODUCT_ID` (INT, FK)
  - `ORDER_DETAIL_ID` (INT, FK)
  - `CUSTOMER_ID` (INT, FK)
  - `ORDER_ID` (INT, FK)

#### 9. Recommendation System
The database implements a sophisticated recommendation system with "People who bought this also bought this" logic through two key tables:

- **PRODUCT_ASSOCIATION**
  - Tracks product relationships and purchase patterns
  - `ASSOCIATION_ID` (INT, PK)
  - `PRODUCT_ID` (INT, FK): The primary product
  - `ASSOCIATED_PRODUCT_ID` (INT, FK): The product that was also purchased
  - `FREQUENCY` (INT): How often these products are purchased together

- **RECOMMENDATIONS**
  - Stores personalized product recommendations for customers
  - `RECOMMENDATION_ID` (INT, PK)
  - `RECOMMENDATION_DATE` (DATETIME): When the recommendation was generated
  - `PRODUCT_ID` (INT, FK): The recommended product
  - `ORDER_DETAIL_ID` (INT, FK): Reference to the order that triggered the recommendation
  - `CUSTOMER_ID` (INT, FK): The customer who received the recommendation

#### 10. Stock Management
- **STOCK_UPDATES**
  - Tracks stock level changes
  - `STOCK_UPDATE_ID` (INT, PK)
  - `UPDATED_STOCK_LEVEL` (INT)
  - `UPDATE_DATE` (DATETIME)
  - `PRODUCT_ID` (INT, FK)

## Key Features

1. **Customer Management**
   - Secure customer authentication
   - Profile management
   - Order history tracking

2. **Product Management**
   - Comprehensive product categorization
   - Multiple attributes (color, size, material)
   - Stock level tracking
   - Brand management

3. **Order Processing**
   - Detailed order tracking
   - Order status management
   - Payment status tracking

4. **Shopping Experience**
   - Shopping bag functionality
   - Advanced product recommendations based on purchase patterns
   - "People who bought this also bought this" recommendations
   - Returns management

5. **Inventory Management**
   - Stock level tracking
   - Stock update history
   - Product availability monitoring

6. **Recommendation Engine**
   - Tracks product associations based on purchase patterns
   - Generates personalized recommendations for customers
   - Maintains frequency data for product associations
   - Supports "People who bought this also bought this" logic

## Database Relationships

- Customers can have multiple Orders (1:N)
- Products can have multiple Colors and Sizes (M:N)
- Each Order can have multiple Order Details (1:N)
- Each Customer has one Shopping Bag (1:1)
- Shopping Bags can contain multiple Products (M:N)
- Products can be associated with multiple other Products for recommendations (M:N)
- Product associations track which products are frequently purchased together

## Indexes

The database includes various indexes for optimizing query performance:
- Customer name and email lookups
- Product name and category searches
- Order date-based queries
- Stock level monitoring
- Product association frequency tracking

## Security Features

- Password storage for customer accounts
- Unique constraints on email and phone numbers
- Foreign key constraints for data integrity
- Cascading deletes where appropriate

## Usage

To use this database:

1. Create a new MySQL database named `MY_STORE`
2. Execute the provided SQL script to create all tables and relationships
3. Ensure proper MySQL configuration for character set (utf8) and storage engine (InnoDB)

## Contributing

Feel free to submit issues and enhancement requests.


[Untitled.pdf](https://github.com/user-attachments/files/19743368/Untitled.pdf)

## Database Schema

[Download MY_STORE.mwb] (https://github.com/Rushikesh-raut712/MY_STORE/tree/main/MY_STORE.mwb?raw=true)


















