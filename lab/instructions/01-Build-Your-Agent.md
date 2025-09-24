# 1 - Build your agent

To start, you're going to setup the foundation for your agent in Copilot Studio.

1. Open Microsoft Edge and navigate to

    <!-- markdownlint-disable-next-line MD034 -->
    +++https://copilotstudio.microsoft.com+++

    ![Open Edge](./assets/OpenEdge.png)

1. Log in with

    <!-- markdownlint-disable-next-line MD034 -->
    **Username:** +++@lab.CloudCredential(CSBatch1).Username+++

    <!-- markdownlint-disable-next-line MD034 -->
    **Password:** +++@lab.CloudCredential(CSBatch1).Password+++

    <!-- markdownlint-disable-next-line MD034 -->
    **Temporary Access Password:** +++@lab.Variable(TAP)+++

1. After logging in, you'll see a message letting you know it's configuring your developer environment. Wait until that finishes (shouldn't take more than a minute)

    ![Dev Environment Setup](./assets/DevEnvSetup.png)

1. If you see a welcome screen like is shown below, select the country/region that you’re in from the dropdown and select **Get Started**

    ![pic2.png](./assets/pic2.png)

1. If you see a welcome message as shown in the screenshot below, select **Skip**.

    ![step6.png](./assets/step6.png)

1. In the left nav click **+ Create** button to start creating a new agent

    ![create.png](./assets/CreateLeftNav.png)

1. Click **New agent**

    ![create-new-agent.png](./assets/NewAgent.png)

1. While we could use natural language to setup the agent for this exercise, we will skip and configure it manually by selecting the **Configure** tab.

    ![step9.jpg](./assets/ConfigreTab.png)

1. In the name field, type +++Zava Order Support+++ and then click the **Create** button

    ![AgentName.png](./assets/ConfigureName.png)

    > [!NOTE]
    > It could take a minute or two for the agent to fully configure. You'll see a message that says **Your agent is provisioned!** when it's ready.

1. Now that your agent is created, you need to equip it with knowledge so it can answer questions about the company, shipping policies, etc. To do this, in your agent overview screen, scroll down to the knowledge section and select the **Add Knowledge** tab.

    ![AddKnowledge.png](./assets/AddKnowledgeBtn.png)

1. Click the **select to browse** button and navigate to **D:\LabFiles\KnowledgeDocuments**. Select the **zava_faq** and **zava_returns_shipping_policy documents**.

    ![DragAndDrop.png](./assets/DragAndDropFile.png)

1. Verify the files are added and select **Add to Agent**

    ![AddToAgent.png](./assets/UploadedFiles.png)

1. You'll know your files are ready to use when you see the **Ready** checkbox next to each file.

    ![Ready.png](./assets/Ready.png)

> [!NOTE]
> The process of uploading the files can take around 5 minutes to complete.

1. Now we need to tell the agent what it's supposed to do. To do this, scroll up to the Instructions section and select the **Edit** button and paste in the following instructions:

    ```text
    Your job is to help customers with Zava’s policies, product FAQs, shipping, returns, and general company info. Use only the supplied knowledge documents. Your behavior: Always consult the Knowledge sources (FAQ, Returns & Shipping Policy) for answers to customer questions in those domains. When you answer, provide a citation (which document and section) whenever possible. If the user asks about something not in the knowledge bases, reply with: “I’m sorry, I don’t have that info yet. Can I help with something in our policy or FAQ?” Use a friendly, professional tone. Be clear but avoid any technical jargon unless user knows them. Keep answers focused and concise. Break up longer responses with bullet lists or numbered steps if helpful.
    ```

    Click **Save**

    ![SaveInstructions.png](./assets/SaveInstructions.png)

1. Now we need to test the agent. Ensure that the test panel is open on the right hand side of the page, type in the following and press **Enter**

    ```text
    What is your return policy?
    ```

    ![TestBefore.png](./assets/TestBeforeEnter.png)

1. Review the output and notice the Activity Pane that displays on the left hand side showing where it pulled the answer from.

    ![TestAfter.png](./assets/TestAfter.png)

    > [!TIP]
    > Given the nature of generative AI, your answer might differ from the answer shown in the screenshot above. That's ok and expected. The important thing here is to observe the Activity Map and how you can tell the agent is pulling from your knowledge.

Congratulations! You have setup an agent that can answer questions about static data from files! Next ,we'll integrate it with an MCP server.
