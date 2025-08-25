## 2 - Connecting to the MCP Server

In this part, you will learn about how to run a Model Context Protocol (MCP) server and how to connect it to Microsoft Copilot Studio. Zava has created an MCP server for inventory management. The Zava Inventory Management MCP consists of a bunch of tools that you can use:

| Category | Tool | Description |
|---|---|---|
| Product management | `get_products()` | List all products |
| Product management | `get_product_by_id(product_id: int)` | Retrieve a product by its ID |
| Product management | `add_product(name: str, category: str, price: float, description: str)` | Add a new product (auto-generates SKU) |
| Product management | `remove_product(product_id: int)` | Remove a product |
| Store management | `get_stores()` | List all stores |
| Store management | `get_store_by_id(store_id: int)` | Retrieve a store by its ID |
| Store management | `add_store(name: str, city: str, country: str, address: str)` | Add a new store |
| Store management | `remove_store(store_id: int)` | Remove a store |
| Inventory management | `list_inventory_by_store(store_id: int)` | Get inventory for a store (with product details) |
| Inventory management | `list_inventory_by_product(product_id: int)` | Get inventory for a product across stores (with store details and totals) |
| Inventory management | `get_inventory_by_product_and_store(product_id: int, store_id: int)` | Get inventory for a specific product at a specific store |
| Inventory management | `update_inventory_by_product_and_store(product_id: int, store_id: int, quantity: int)` | Update the quantity for a product at a store |

The MCP server is available on `C:\src\zava-inventory-mcp\`.

### Open the MCP Server in Visual Studio Code

1. Open Visual Studio Code by selecting Visual Studio Code in the taskbar
1. Select **File > Open Folder**
1. Navigate to `C:\src\zava-inventory-mcp`
1. Select **Select Folder**

This will open the Zava Inventory Management MCP server in Visual Studio Code. After this, we will install the dependencies so that we can run the server locally.

### Install dependencies

1. Open the terminal by selecting **Terminal > New Terminal**
1. Enter the following command:

    ```bash
    pip install -r src/requirements.txt
    ```

    This will install the dependencies. It might take a while, so wait a little while until it's finished.

1.
