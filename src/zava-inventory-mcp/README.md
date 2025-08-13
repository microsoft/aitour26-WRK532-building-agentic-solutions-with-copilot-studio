# Zava Inventory MCP Server

A comprehensive Model Context Protocol (MCP) server for managing inventory across multiple store locations. This server provides a complete suite of tools for managing products, stores, and inventory data for the fictional retail company "Zava".

## 🚀 Features

- **Product Management**: Add, remove, and retrieve product information
- **Store Management**: Manage store locations worldwide
- **Inventory Tracking**: Track product quantities across all store locations
- **Real-time Data**: JSON-based data storage with immediate updates
- **Global Coverage**: Support for international store locations

## 📊 Data Structure

The system manages three main data entities:

### Products (`data/products.json`)
- Product information including name, category, price, SKU, and description
- No stock quantities (handled separately in inventory)

### Stores (`data/stores.json`)
- Store locations with name, city, country, and address
- Global coverage across 10 major cities

### Inventory (`data/inventory.json`)
- Links products to stores with current quantities
- Tracks last updated timestamps
- Supports detailed inventory management

## 🛠️ Available Tools

### Product Management Tools

#### `get_products()`
Retrieves all products from the products.json file.
- **Returns**: List of all products with details
- **Use case**: Browse product catalog

#### `get_product_by_id(product_id: int)`
Retrieves a specific product by its ID.
- **Parameters**: `product_id` - The ID of the product to retrieve
- **Returns**: Product details or error if not found
- **Use case**: Get detailed information about a specific product

#### `add_product(name: str, category: str, price: float, sku: str, description: str)`
Adds a new product to the inventory system.
- **Parameters**:
  - `name` - Product name
  - `category` - Product category
  - `price` - Product price
  - `sku` - Product SKU/code
  - `description` - Product description
- **Returns**: Success confirmation with new product details
- **Use case**: Add new products to the catalog

#### `remove_product(product_id: int)`
Removes a product from the system.
- **Parameters**: `product_id` - The ID of the product to remove
- **Returns**: Success confirmation with removed product details
- **Use case**: Discontinue products

### Store Management Tools

#### `get_stores()`
Retrieves all store locations.
- **Returns**: List of all stores with location details
- **Use case**: View all store locations

#### `get_store_by_id(store_id: int)`
Retrieves a specific store by its ID.
- **Parameters**: `store_id` - The ID of the store to retrieve
- **Returns**: Store details or error if not found
- **Use case**: Get information about a specific store

#### `add_store(name: str, city: str, country: str, address: str)`
Adds a new store location.
- **Parameters**:
  - `name` - Store name (e.g., "Zava Tokyo")
  - `city` - City name
  - `country` - Country name
  - `address` - Full address
- **Returns**: Success confirmation with new store details
- **Use case**: Open new store locations

#### `remove_store(store_id: int)`
Removes a store from the system.
- **Parameters**: `store_id` - The ID of the store to remove
- **Returns**: Success confirmation with removed store details
- **Use case**: Close store locations

### Inventory Management Tools

#### `list_inventory_by_store(store_id: int)`
Gets inventory for a specific store with resolved product names and details.
- **Parameters**: `store_id` - The ID of the store
- **Returns**: List of inventory items with complete product information
- **Use case**: Check what products are available at a specific store

#### `list_inventory_by_product(product_id: int)`
Gets inventory for a specific product across all stores with resolved store names and details.
- **Parameters**: `product_id` - The ID of the product
- **Returns**: List of inventory items with complete store information and total quantity
- **Use case**: Check which stores have a specific product in stock

#### `get_inventory_by_product_and_store(product_id: int, store_id: int)`
Gets inventory for a specific product at a specific store with complete details.
- **Parameters**:
  - `product_id` - The ID of the product
  - `store_id` - The ID of the store
- **Returns**: Complete inventory, product, and store information
- **Use case**: Check exact quantity of a product at a specific store

#### `update_inventory_by_product_and_store(product_id: int, store_id: int, quantity: int)`
Updates inventory quantity for a specific product at a specific store.
- **Parameters**:
  - `product_id` - The ID of the product
  - `store_id` - The ID of the store
  - `quantity` - New quantity value
- **Returns**: Success confirmation with updated inventory
- **Use case**: Update stock levels after sales or restocking

##  Quick Start

### 1. Installation
```bash
# Clone the repository
git clone <repository-url>
cd inventory-mcp

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: .\venv\Scripts\activate

# Install dependencies
pip install -r src/requirements.txt
```

### 2. Start the Server
```bash
# Development mode
python src/server.py

# Production mode
RUNNING_IN_PRODUCTION=true python src/server.py
```

### 3. Test the Server
```bash
# Health check
curl http://localhost:3000/health

# View available endpoints
curl http://localhost:3000/
```

## 📁 Project Structure

```
inventory-mcp/
├── src/
│   ├── server.py          # Main MCP server
│   ├── requirements.txt   # Python dependencies
│   └── Dockerfile         # Docker configuration
├── data/
│   ├── products.json      # Product catalog
│   ├── stores.json        # Store locations
│   └── inventory.json     # Inventory tracking
├── .env.example           # Environment template
├── README.md             # This file
└── docker-compose.yml    # Docker Compose configuration
```

## 🌍 Sample Data

The system comes pre-loaded with:
- **10 Products**: Electronics, furniture, sports equipment, etc.
- **10 Stores**: Located in major cities worldwide (New York, London, Tokyo, Paris, Sydney, Rio de Janeiro, Singapore, Berlin, Toronto, Seoul)
- **34 Inventory Records**: Realistic distribution of products across stores

## 🔧 API Examples

### Get All Products
```bash
curl http://localhost:3000/api/products
```

### Check Store Inventory
```bash
curl http://localhost:3000/api/inventory/store/1
```

### Add New Product
```bash
curl -H "Content-Type: application/json" \
     -d '{
       "name": "Smart Watch",
       "category": "Electronics",
       "price": 299.99,
       "sku": "SW-001",
       "description": "Advanced fitness tracking smartwatch"
     }' \
     http://localhost:3000/api/products
```

## 🐳 Docker Support

```bash
# Build and run with Docker Compose
docker-compose up --build

# The server will be available at http://localhost:3000
```

## 📈 Use Cases

- **Retail Management**: Complete inventory management for retail chains
- **E-commerce**: Product and inventory tracking for online stores
- **Supply Chain**: Monitor product distribution across locations
- **Analytics**: Generate reports on product performance by location
- **Customer Service**: Check product availability for customers

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For questions or issues:
1. Review the health endpoints at `/health` and `/`
2. Check server logs for detailed error messages
3. Visit `/docs` for interactive API documentation

---

**Zava Inventory MCP Server** - Powering global retail inventory management 🌟
