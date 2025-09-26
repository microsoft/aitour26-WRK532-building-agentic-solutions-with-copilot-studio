# 3 - Add a Prompt for Warranty Claim Processing

Now that we’ve got an agent that can answer questions from knowledge and integrate with our MCP server for real time operations, we’ll give the agent additional capabilities by integrating an AI prompt to process warranty claims. In this section, we’ll add a Warranty Policy knowledge source (category-based rules), then use a single AI prompt to turn messy, pasted claim text into clean fields and even intelligently classify the claim.

1. In your agent overview screen, scroll down to the knowledge section and select the **Add Knowledge** tab.

    ![AddKnowledge.png](./assets/AddKnowledgeStep3.png)

1. Click the **select to browse** button and navigate to **D:\LabFiles\KnowledgeDocuments**. Select the **zava_warranty_policy** document.

    ![DragAndDrop.png](./assets/DragAndDropFile.png)

1. Verify the files are added and select **Add to Agent**

    ![AddToAgent.png](./assets/WarrantyVerifyKnowledge.png)

1. You'll know your files are ready to use when you see the **Ready** checkbox next to each file.

    ![Ready.png](./assets/WarrantyKnowledgeReady.png)

Now that we have the Warranty Claim knowledge source added, we want to build our AI Prompt to extract information from the claim.

1. Scroll down to the Tools section and select **Add tool**

    ![Add Tool](./assets/NewTool.png)

1. Select **New Tool**

    ![New Tool](./assets/NewTool3.png)

1. Select **Prompt**

    ![Prompt Selection](./assets/PromptSelection.png)

1. Click in the top bar next to the icon and rename the prompt to  ```Warranty Claim Processor```

    ![Rename](./assets/PromptName.png)

1. Paste the following instructions into the instructions panel of the prompt:

```text
Review the [add input here] and extract this key information:
Product Name
SKU
Purchase Date
Order Number
Claimant Name
Product Category (Group into either Electronics, Furniture, Home & Garden, Sports & Fitness, Kitchen, Accessories)
Issue Summary
Issue Category (i.e., Physical Damage, Wear and Tear, Misuse, Dead On Arrival, Unknown)
```

![Instructions](./assets/InstructionsPasted.png)

1. Delete the **[add input here]** text and type a **forward slash (/)** and select **text** to add a new variable

    ![Input](./assets/InputType.png)

1. Name this variable ```Warranty Claim``` and put in the following text in the **Sample data** input:

    ```text
    Help me process this warranty claim from this customer: Alex Morgan (alex.morgan@example.com, +1 (555) 012-7784, prefers email). Address: 123 Maple Lane, Tulsa, OK 74104. Product is a Zava Backpack (SKU BP-010) purchased from Zava Online on 2025-08-22, order A12876. After two commutes the main zipper pull detached; the teeth misalign and the main compartment won’t close—used under normal conditions. Please evaluate against our warranty policy and advise approval/denial and next steps (including RMA if applicable).
    ```

    Select the **close button**

    ![InputFilled](./assets/InputFilled.png)

1. Select the **Output** dropdown and change it to **JSON** so we can get a structured response.

    ![Output Configuration](./assets/OutputSelect.png)

1. Before saving, we have to test to make sure the prompt works correctly, that is why we put sample data in our input in the previous step. To do that, click the **Test** button.

    ![Test Prompt](./assets/TestBtnPrompt.png)

1. Review the output of the test and notice how it extracted all the info in a structured format. Click the **Save** button to save this new prompt.

    ![Test Response](./assets/PromptTestOutput.png)

1. Now click the **Add and configure** button to add this to the agent and take you directly to the configuration page for the prompt.

    ![Add and Configure Button Prompt](./assets/AddConfigureBtnPrompt.png)

1. Now we'll see the configuration screen where we can control specific settings for the prompt for use in our agent. The first thing we need to do is expand out the **Additional details** section and select the **Agent may use this tool at any time** radio button.

    ![Additional Details](./assets/PromptAdditionalDetails.png)

1. Next, scroll down to the Inputs section where you'll find the input you created in the prompt for warranty claim. There are two ways to fill this input: hard coding it or letting AI dynamically fill it. We want AI to dynamically fill it in this case, but we need to give it more details to know where to get that from and what it should do. To do that, click the **Customize** button next to the input.

    ![Additional Details](./assets/InputConfigureBtnPrompt.png)

1. In the **Description** box, paste the following:

```text
Fill with the details of the warranty claim pasted in the chat from the user.
```

![Additional Details](./assets/PromptDescriptionSave.png)

1. Click the **Save** button to save all of your changes.

    ![Additional Details](./assets/PromptDescriptionSave.png)

1. Select the **Overview** tab to go back to the overview screen.

    ![Additional Details](./assets/OverviewTab.png)

1. Now we need to modify the instructions so if someone asks for a warranty claim approval, it calls the prompt to extract information. To do this, select the **Edit** button next to the **Instructions** section.

    ![Additional Details](./assets/EditINstructionsPrompt.png)

1. Paste in the following text below the instructions that are already in there.

    ```text
    If someone asks about doing a warranty claim review, call the [add prompt here] tool to extract the claim details. Look up the extracted product category in the Warranty Policy Knowledge source and extract the following information:
    
    Coverage Window
    Exceptions Allowed(Yes or No if the warranty claim has any exceptions that allow it to be approved outside the warranty period)
    Warranty Policy (full details of the warranty policy fo rthat given product category, example: receipts required, allowed within 30 days, etc)
    
    Respond in the chat with all relevant details that were extracted.
    ```

1. Delete the **[add prompt here]** text and replace with a **forward slash (/)**. A menu will pop up where you'll see a **Tools** section. Expand that and select the **Warranty Claims Processing** prompt.

    ![Additional Details](./assets/PromptInstructionsRevised.png)

1. Click **Save** to save your new instructions.
1. Now it's time to test the end to end process. Click on the **Test** button in the upper right hand corner to open the Test Panel (if it isn't already open)
1. Paste in the following text in the test window:

    ```text
    Help me process this warranty claim from customer Chris Bailey (chris.bailey@example.com, +1 (555) 014-9932, prefers phone). Address: 55 N Greenwood Ave, Tulsa, OK 74120. The product is an Ergonomic Office Chair (SKU EOC-002, serial EOC002-77412) purchased from Zava Tulsa on 2024-08-10, order A11992. The issue: the chair slowly sinks about two inches over an hour—the pneumatic lift isn’t holding. This was noticed after a few months. The customer has a receipt and can provide photos.
    ```

    Press **Enter**

1. Watch the Activity Panel on the left hand side to see how the agent calls the prompt and passes in the information and does the check in the Warranty Policy knowledge source to find and return the necessary information.

    ![Additional Details](./assets/WarrantyPolicyPromptTest.png)

You've just successfully added additional functionality to your agent to handle extracting warranty claim details using an AI Prompt. Now, we'll see how to improve this warranty claim review process by adding in an approval process.