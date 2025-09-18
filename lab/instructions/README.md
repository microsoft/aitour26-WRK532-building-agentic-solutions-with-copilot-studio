# @lab.Title

In this 75-minute hands-on workshop, you'll experience the complete journey of building an intelligent agent using Microsoft Copilot Studio. Through a practical inventory and order management scenario, you'll learn how to create a sophisticated AI assistant capable of handling real-world business operations.

## What You'll Learn

By the end of this workshop, you'll have practical experience with:

- **Agent Design & Architecture**: Understanding how to design purpose-driven agents that solve specific business problems
- **Knowledge Integration**: Adding and managing knowledge bases to make your agent contextually aware
- **Advanced Automation**: Building Agent Flows to handle deterministic, complex, multi-step business processes
- **External System Integration**: Connecting your agent to external services using Model Context Protocol (MCP) servers
- **Production Deployment**: Publishing and configuring your agent for real-world use

## Workshop Scenario

You are a solutions architect tasked with modernizing the customer service experience for Zava Retail Store, a regional retailer serving suburban communities.
Currently, customers call or email to check inventory, place orders, and track shipments which creates bottlenecks for both customers and staff. Your mission is to build an intelligent Inventory Assistant that can:

- Answer product availability questions instantly
- Guide customers through the ordering process
- Provide real-time inventory updates
- Handle order modifications and cancellations
- Escalate complex issues to human agents when needed

The green text with the +++icon+++ can be clicked on and will be typed automatically into the VM, For example, please click in the password text box and then click the password: <+++@lab.VirtualMachine>(WRK532).Password+++

> [!note] To ensure text is entered accurately avoid interacting or clicking in the VM until the text has finished being typed

===

## 1 - Build your agent

To start, you're going to setup the foundation for your agent in Copilot Studio.

1. Open Microsoft Edge and navigate to

    +++<https://copilotstudio.microsoft.com+++>

1. Log in with

    <!-- markdownlint-disable-next-line MD034 -->
    **Username:** +++@lab.CloudCredential(CSBatch1).UserPrincipalName+++

    <!-- markdownlint-disable-next-line MD034 -->
    **Password:** +++@lab.CloudCredential(CSBatch1).Password+++

    <!-- markdownlint-disable-next-line MD034 -->
    **Temporary Access Password:** +++@lab.Variable(TAP)+++

1. If you see a welcome screen like is shown below, select the country/region that you’re in from the dropdown and select Get Started

    ![pic2.png](./assets/pic2.png)

1. If you see a welcome message as shown in the screenshot below, select Skip.

    ![step6.png](./assets/step6.png)

1. Click the Environment drop down in the top right and then select the Dev environment ENV{LAB_INSTANCE_ID}

    ![create.png](./assets/step3.png)

1. In the left nav click **+ Create** button to start creating a new agent

    ![create.png](./assets/CreateLeftNav.png)

1. Click **New agent**

    ![create-new-agent.png](./assets/NewAgent.png)

1. While we could use natural language to setup the agent for this exercise, we will skip and configure it manually by selecting the **Configure** tab.

    ![step9.jpg](./assets/ConfigreTab.png)

1. In the name field, type +++Zava Order Support+++ and then click the **Create** button

    ![AgentName.png](./assets/ConfigureName.png)

1. Now that our agent is created, we need to equip it with knowledge so it can answer questions about our company background, shipping policies, etc. This information is stored in two PDF documents which you need to download, the [Zava FAQ Doc](./assets/zava_faq.pdf) and [Zava Policies Doc](./assets/zava_returns_shipping_policy.pdf).

1. In your agent overview screen, scroll down to the knowledge section and select the **Add Knowledge** tab.

    ![AddKnowledge.png](./assets/AddKnowledgeBtn.png)

1. Drag and drop the [Zava FAQ Doc](./assets/zava_faq.pdf) and [Zava Policies Doc](./assets/zava_returns_shipping_policy.pdf) files you downloaded in the step above into the canvas

    ![DragAndDrop.png](./assets/DragAndDropFile.png)

1. Verify the files are added and select **Add to Agent**

    ![AddToAgent.png](./assets/UploadedFiles.png)

1. You'll know your files are ready to use when you see the **Ready** checkbox next to each file.

    ![Ready.png](./assets/Ready.png)

1. Now we need to tell the agent what it's supposed to do. To do this, scroll up to the Instructions section and select the **Edit** button and paste in the following instructions:

```Your job is to help customers with Zava’s policies, product FAQs, shipping, returns, and general company info. Use only the supplied knowledge documents.
    Your behavior:
    Always consult the Knowledge sources (FAQ, Returns & Shipping Policy) for answers to customer questions in those domains.
    When you answer, provide a citation (which document and section) whenever possible.
    If the user asks about something not in the knowledge bases, reply with: “I’m sorry, I don’t have that info yet. Can I help with something in our policy or FAQ?”
    Use a friendly, professional tone. Be clear but avoid any technical jargon unless user knows them.
    Keep answers focused and concise. Break up longer responses with bullet lists or numbered steps if helpful.
```

Click **Save**

![SaveInstructions.png](./assets/SaveInstructions.png)

1. Now we need to test the agent. Ensure that the test panel is open on the right hand side of the page, type in the following and press **Enter**

    > What is your return policy?

    ![TestBefore.png](./assets/TestBeforeEnter.png)

1. Review the output and notice the Activity Pane that displays on the left hand side showing where it pulled the answer from.

    ![TestAfter.png](./assets/TestAfter.png)

Congratulations! You have setup an agent that can answer questions about static data from files! Next ,we'll integrate it with an MCP server.

===

## 2 - Connect to an MCP Server

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

### Run the MCP Server

1. Now it's time to run the MCP Server. Use the following command to start the Zava Inventory MCP Server.

    ```bash
    python src/server.py
    ```

After running the MCP Server, you're not there yet. The MCP Server is only running locally right now, so you need to make sure the MCP Server is available through a public URL. This is a requirement for Microsoft Copilot Studio. Because it's a cloud service, it's not able to reach your localhost.

### Configure a dev tunnel

To make sure we can reach the MCP Server from Microsoft Copilot Studio, we'll add a dev tunnel. During these steps, you will be prompted to log in. Use the Entra ID account from this workshop when you are prompted to log in.

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

1. In the address bar, add `/mcp` behind the address and hit **Enter**

    Now your browser will display an error, because in the browser we didn't add the API Key.
    `🔒 Authentication Failed ⛔`

We are going to fix this error in the next steps.

### Add the MCP Server in Microsoft Copilot Studio

1. Open your browser and go back to the environment where you create the agent earlier
1. Open your agent
1. In the top navigation, select **Tools**
1. Select **+ Add a tool**
1. Select **+ New tool**
1. Select **Model Context Protocol**
1. Enter the **Name**:

      ```text
      Zava Inventory MCP
      ```

1. Enter the **Description**:

      ```text
      Zava Inventory MCP
      ```

1. Enter the **Server URL**. This should be the URL you opened from the ports tab in Visual Studio Code without the `https://` in front of it and with the `/mcp` behind it. For example: `something-3000.something.devtunnels.ms/mcp`.
1. For *Authentication*, select **API key**
1. Leave the *type* on *Header* and for *Header name* add the following value:

      ```text
      authorization
      ```

      ![Create MCP Tool](./assets/CreateMCPTool.png)

1. Check if all the values are correct and if so, select **Create** to add the MCP Server

    This will take a while, since in the background it is creating a custom connector for the MCP Server.

1. When it's done, select **Not connected** and **Create new connection**
1. Enter the **API Key**:

      ```text
      AITour2026!
      ```

1. Select **Add to agent**

    ![Add to agent](./assets/AddToAgent.png)

    Now it's time to test the agent with the MCP Server!

1. Select the **Map** icon in the top right corner of the *Test your agent* panel to activate the *Activity map*. This will help you understand what is happening when you are sending and receiving messages in the *Test your agent* panel.

    ![Activity Map](./assets/ActivityMap.png)

1. Now, enter the following message and send it in the *Test your agent* panel:

      ```text
      List the Zava Stores
      ```

    This should show you a whole bunch of Zava Stores as an answer in the *Test your agent* panel:

    ![List Zava Stores test pane](./assets/ListZavaStores.png)

    And on the left in the *Activity map*, you can see that the Zava Inventory MCP has been initialized and the *get_stores* tool has been triggered by our message. When you click on the *get_stores* tool, you're even able to see the output that the agent got from the MCP server. This means our agent made that text into the formatted output we saw in the *Test your agent* panel.

    ![Activity Map after asking to list the Zava Stores.](./assets/ListZavaStoresActivityMap.png)

    Let's experiment a bit more with the other tools as well.

1. Send the following message to your agent via the *Test your agent* panel:

      ```text
      List the available products in the Zava Amsterdam store
      ```

    You will see the available products in the Zava Amsterdam store in the *Test your agent* panel:

    ![List Available Products in the Zava Amsterdam store in the test pane](./assets/ListAvailableProductsZavaAmsterdam.png)

    Now you can see in the *Activity map* more tools have been triggered. The *get_stores* tool has been triggered again, because it needs it for the *list_inventory_by_store* tool. This really shows the power of MCP: when used correctly, it can do a lot of calls for you, without having to build a flow for it or to give it more instructions.

    ![Activity Map after asking to list the available products in the Zava Amsterdam store.](./assets/ListAvailableProductsZavaAmsterdamActivityMap.png)

    But now - we only did get actions, wouldn't it be good to also add something?

1. Send the following message to your agent via the *Test your agent* panel:

    ```text
    Please add the following Zava Store:
    Zava Chicago
    1597 Virginia Street, Chicago, Illinois, IL 60618
    ```

    ![Add Zava store via message](./assets/AddZavaStore.png)

    As you can see, we didn't add United States to the message, but it automatically added that based on the details in the message.

    ![Add Zava store activity map](./assets/AddZavaStoreActivityMap.png)

This section was to help you understand how to use MCP in a Copilot Studio agent. If you have time left at the end of this workshop, feel free to play around with the other tools in the MCP Server.

===

## 3 - Add an agent flow

Customers and store staff sometimes ask for discounts. Zava’s policy is to only grant a discount when the item isn’t low in stock and a manager signs off. This makes a great use case for an Agent Flow.

1. Scroll down to the Tools section and select **New Tool**
    ![New Tool](./assets/NewTool.png)

1. Select **New Tool** in the dialog

    ![New Tool](./assets/NewTool2.png)

1. Select **Agent Flow**

    ![Agent Flow](./assets/AgentFlowBtn.png)

1. Select the **plus button** between the when an agent calls a flow and respond to agent.

    ![Plus Button](./assets/PlusBtn.png)

1. Scroll down to the Human in the Loop section and select the **Start and Wait for Approval**.

    ![Zava Inventory](./assets/StartWaitForApproval.png)

1. In the Approval Type dropdown select **Approve/Reject - First to Respond**

    ![First to respond](./assets/ApprovalType.png)

1. For the Title input put ```Approve New Store Onboarding```

    ![Approve New Onboarding](./assets/ApprovalTitle.png)

1. For the Assigned To enter your username

    ![Approval Assigned To](./assets/ApprovalAssignedTo.png)

1. Now we need to be sure we can pass relevant information about the new store to the flow to include in our approval request. To do that we need to scroll up and select the **When an agent calls a flow** trigger and select **Add Input**

    ![Approval Assigned To](./assets/AddInput.png)

1. Select **Text** from the list of input options

    ![Text Input](./assets/TextInput.png)

1. ddd

===

## 4 - Test and Publish Your Agent

Now that you have confirmed your agent is working as expected let’s publish the agent. We'll publish to the demo website which simulates what your agent would look like if it was published to a public website.

1. Now we need to confirm and configure some settings for our agent. To do that, select the **Settings** button in the top right hand corner

    ![step14.png](./assets/AgentSettingsBtn.png)

1. In the Generative AI tab, confirm that **Generative Orchestration** is set to **Yes** and turn **Connected Agents** to **On** then select **Save**

    ![AgentTest.png](./assets/OrchestrationSettings.png)

1. Select the **Security** tab in the left navigation

    ![AgentTest.png](./assets/SecurityTabLeftNav.png)

1. Select **Authentication**

    ![AgentTest.png](./assets/SelectAuthentication.png)

1. Select **No Authentication** and select the **Save** button to apply the settings.

    ![AgentTest.png](./assets/AuthenticationSettings.png)

1. Click the **Publish** button in the top right-hand corner

    ![AgentPublish.png](./assets/AgentPublish.png)

1. Click the **Publish** button to publish your agent

    ![publish-agent.png](./assets/publish-agent.png)

    The following dialog will be displayed you can close this and your agent will finish publishing in the background

    ![publishing-agent.png](./assets/publishing-agent.png)

1. Now that it’s published, we need to make this available to use within Microsoft Teams. Select the **Channels** tab in the top menu

   ![AgentChannels.png](./assets/AgentChannels.png)

Congratulations! You’ve now built and published an agent!

===

Nothing will be graded so feel free to submit and close out of the VM. If you finished the workshop you get an A+!
