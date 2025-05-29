# Computer Parts Store

A simple web application for browsing and purchasing computer parts, built with Flask and React, containerized with Docker, and with Snowflake integration for BI analytics.

## Features

- Browse computer parts by category
- Add products to shopping cart
- Checkout with shipping information
- Store order data in PostgreSQL
- Sync orders to Snowflake for BI analytics

## Project Structure
```
computer-parts-store/
├── docker-compose.yml        # Docker Compose
├── .env                      # Environment variables
├── README.md                 # Project documentation
│
├── frontend/                 # React frontend
│   ├── Dockerfile            # Frontend container
│   └── ...                   # React application files
│
├── backend/                  # Flask backend
│   ├── Dockerfile            # Backend container
│   └── ...                   # Flask application files
│
├── database/                 # Database setup
│   └── init.sql              # Initial database schema and seed data
│
└── snowflake/                # Snowflake integration
└── schema/                   # Snowflake schema definitions
```

## Prerequisites

- Docker and Docker Compose
- Snowflake account (optional for BI analytics)

## Getting Started

1. Clone the repository: git clone https://github.com/shawnppitts/Computer-Parts.git

2. Create a `.env` file with your Snowflake credentials (optional):
```
SNOWFLAKE_USER=your_username
SNOWFLAKE_PASSWORD=your_password
SNOWFLAKE_ACCOUNT=your_account
SNOWFLAKE_WAREHOUSE=your_warehouse
SNOWFLAKE_DATABASE=your_database
```
3. Start the application:
```
$ docker-compose up
```

4. Access the application:
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000/api

## API Endpoints

### Products

- `GET /api/products/` - Get all products
- `GET /api/products/?category=CPU` - Get products by category
- `GET /api/products/categories` - Get all categories
- `GET /api/products/<id>` - Get a specific product

### Orders

- `POST /api/orders/` - Create a new order
- `GET /api/orders/<id>` - Get a specific order

## Database Schema

### Products Table
- id: Primary key
- name: Product name
- description: Product description
- price: Product price
- category: Product category
- stock: Available stock
- image_url: URL to product image
- created_at: Creation timestamp

### Orders Table
- id: Primary key
- first_name: Customer's first name
- last_name: Customer's last name
- email: Customer's email
- address: Shipping address
- city: City
- country: Country
- zip_code: Zip/Postal code
- total: Order total
- status: Order status (pending, processing, shipped, etc.)
- created_at: Creation timestamp

### Order Items Table
- id: Primary key
- order_id: Reference to orders table
- product_id: Reference to products table
- quantity: Product quantity
- price: Product price at the time of purchase

## Snowflake Integration

The application syncs order data to Snowflake for BI analytics. If Snowflake credentials are not provided, this functionality is skipped without affecting the core application.

## License

This project is licensed under the MIT License - see the LICENSE file for details.