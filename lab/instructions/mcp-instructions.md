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
1. Navigate to `C:\src\zava-inventory-mcp`
1. Create a new virtual environment by running the following command:

    ```bash
    python -m venv .venv
    ```

1. Now, you need to active the virtual environment. Run the following command to do that.

    ```bash
    .venv\Scripts\activate
    ```

1. Install all dependencies by running the command below. It might take a while, so wait a little while until it's finished.

    ```bash
    pip install -r src/requirements.txt
    ```

### Setup local environment variable for authentication

The Zava MCP Server uses API key authentication to avoid that people can get to the data that gets accessed by the MCP Server. In this case, the MCP Server is using a local environment variable called `MCP_API_KEY`. Later in this lab, the MCP Server will match the value of the environment variable with the incoming request from Microsoft Copilot Studio.

Let's setup the local environment variable now.

1. Run the following command to set the value of the `MCP_API_KEY` environment variable to `AI-tour-25`.

    ```bash
    $env:MCP_API_KEY = "AI-tour-26"
    ```

### Run the MCP Server

1. Now it's time to run the MCP Server. Use the following command to start the Zava Inventory MCP Server.

    ```bash
    python src/server.py
    ```

After running the MCP Server, you're not there yet. The MCP Server is only running locally right now, so you need to make sure the MCP Server is available through a public URL. This is a requirement for Microsoft Copilot Studio. Because it's a cloud service, it's not able to reach your localhost.

### Configure a dev tunnel

In the terminal at the bottom of Visual Studio Code, there are a couple of tabs:

- Problems
- Output
- Debug Console
- Terminal
- Ports
- Spell Checker
- Azure

1. Select the tab **Ports**
1. Select **Forward a Port**
1. Enter `3000` in the port field and press **Enter**
1. Right click on the line of your forwarded port and select **Port Visibility > Public**

    Now you made your server available to the outside world.

1. Hover over the **Forwarded Address** and select the 🌐 icon

    This will prompt you if you want Code to open an external website.

1. Select **Open**

    Now your browser will be opened with the MCP Server running. The following message should be displayed:
    `The Zava Inventory 📦 MCP Server 🧠 is running`

1. In the address bar, add `/MCP` behind the address and hit **Enter**

    Now your browser will display an error, because in the browser we didn't add the API Key.
    `🔒 Authentication Failed ⛔`

We are going to fix this error in the next steps.

### Add the MCP Server in Microsoft Copilot Studio

1. Open your browser and go back to the environment where you create the agent earlier
1. Open your agent
1. In the top navigation, select **Tools**
1.
