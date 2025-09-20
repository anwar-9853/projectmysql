# E-Commerce Database System

A complete MySQL database solution for e-commerce operations including customer management, product catalog, order processing, and inventory management.

## 🚀 Quick Start

### Prerequisites
- MySQL Server 8.0+ 
- MySQL client (command line or MySQL Workbench)

### Installation

1. **Download the database script**
   ```bash
   # Clone or download the project files
   git clone <your-repository-url>
   cd ecommerce-db
   ```

2. **Run the SQL script**
   ```bash
   # Method 1: Command line
   mysql -u your_username -p < ecommerce_db.sql
   
   # Method 2: MySQL Workbench
   # Open the SQL file and execute all statements
   ```

3. **Verify installation**
   ```sql
   SHOW DATABASES;
   USE ecommerce_db;
   SHOW TABLES;
   SELECT * FROM categories; -- Check sample data
   ```

## 📊 API Endpoints

### Base URL
`http://localhost:3000/api` (adjust based on your server configuration)

### Authentication Endpoints

| Method | Endpoint | Description | Parameters |
|--------|----------|-------------|------------|
| `POST` | `/auth/register` | Register new customer | `email`, `password`, `first_name`, `last_name` |
| `POST` | `/auth/login` | Customer login | `email`, `password` |

### Product Endpoints

| Method | Endpoint | Description | Parameters |
|--------|----------|-------------|------------|
| `GET` | `/products` | Get all products | `page`, `limit`, `category_id` (optional) |
| `GET` | `/products/:id` | Get product by ID | - |
| `GET` | `/categories` | Get all categories | - |

### Order Endpoints

| Method | Endpoint | Description | Parameters |
|--------|----------|-------------|------------|
| `POST` | `/orders` | Create new order | `customer_id`, `items[]`, `shipping_address_id` |
| `GET` | `/customers/:id/orders` | Get customer orders | - |
| `GET` | `/orders/:id` | Get order details | - |

### Customer Endpoints

| Method | Endpoint | Description | Parameters |
|--------|----------|-------------|------------|
| `GET` | `/customers/:id` | Get customer profile | - |
| `PUT` | `/customers/:id` | Update customer profile | `first_name`, `last_name`, `phone` |
| `POST` | `/customers/:id/addresses` | Add customer address | `street`, `city`, `postal_code`, `type` |

## 🗄️ Database Structure

The database includes 18 tables with relationships:
- **Customers** ↔ Customer_Profiles (One-to-One)
- **Customers** → Orders (One-to-Many) 
- **Products** ↔ Orders (Many-to-Many via Order_Items)
- **Categories** hierarchical structure (Self-referencing)

## 🔧 Configuration

Update your application's database connection:

```javascript
// Example configuration
const dbConfig = {
  host: 'localhost',
  user: 'your_username',
  password: 'your_password',
  database: 'ecommerce_db',
  port: 3306
};
```

## 📋 Sample Queries

```sql
-- Get all active products with categories
SELECT p.product_name, p.unit_price, c.category_name 
FROM products p
JOIN categories c ON p.category_id = c.category_id
WHERE p.is_active = TRUE;

-- Get customer order history
SELECT o.order_id, o.order_date, o.final_amount, o.order_status
FROM orders o
WHERE o.customer_id = 101
ORDER BY o.order_date DESC;
```

## 🆘 Troubleshooting

**Common issues:**
- Authentication failed: Check MySQL user permissions
- Connection refused: Verify MySQL server is running
- Database not found: Execute the SQL script again

**Need help?** 
- Check MySQL error logs
- Verify all prerequisite software is installed
- Ensure port 3306 is not blocked by firewall

## 📝 License

This project is available for use under the MIT License.
