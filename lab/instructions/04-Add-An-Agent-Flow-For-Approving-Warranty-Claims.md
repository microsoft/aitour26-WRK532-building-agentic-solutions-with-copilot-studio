# 4 - Add an Agent Flow for Approving Warranty Claims

Now that we have an AI prompt that can classify warranty claims and extract key info, we’re going to wrap this process in a formal, approval path based off of certain conditions like if it's in the warranty period. This is exactly what Agent Flows are for: augmenting your agents with a configurable and predictable decision path. In this section, you’ll build an agent flow that reads the extracted fields, evaluates the policy conditions, and triggers an auto approval if those conditions are met.

1. To create a new agent flow, scroll down to the Tools section and select **New Tool**
    ![New Tool](./assets/NewToolAgentFlow1.png)

1. Select **New Tool** in the dialog

    ![New Tool](./assets/NewTool2.png)

1. Select **Agent Flow**. This will route you to a new agent flow that you'll need to configure.

    ![Agent Flow](./assets/AgentFlowBtn.png)

1. You'll see two items on the screen, the trigger which kicks off the flow and the response which returns data back to the agent. The first thing we need to do is configure any inputs that we want to pass into our flow from the agent to use in the flow. To add these inputs, select the **When an agent calls the flow** trigger.

    ![Flow](./assets/SelectFlowTrigger.png)

1. Select **Add an input**

    ![Add Input](./assets/FlowAddInput1.png)

1. Select the **Text** option

    ![Text Input](./assets/FlowTriggerInputType.png)

1. In the Text input type ```Issue Category```

    ![Issue Category](./assets/FlowIssueCat.png)

1. Select **Add an input**

    ![Add Input](./assets/FlowIssueCatAddInput.png)

1. Select the **Text** option

    ![Text Input](./assets/FlowIssueCatText.png)

1. In the Text input type ```Purchase Date```

    ![Product Input](./assets/FlowPurchaseDateFilled.png)

1. Select **Add an input**

    ![Product Input](./assets/FlowPurDateAddInput.png)

1. Select the **Number** option

    ![Text Input](./assets/FlowPurDateNumb.png)

1. In the Text input type ```Coverage Window Days```

    ![Product Input](./assets/FlowCovDayInputFilled.png)

1. You should see three inputs as configured below. Once you confirm your inputs match the screenshot below, click the arrow to hide this panel.

    ![Inputs](./assets/FlowInputsConfig.png)

1. Select the **plus button** between the when an agent calls a flow and respond to agent to add a new action.

    ![Plus Button](./assets/PlusBtn.png)

1. Search for ```variable``` and select **initialize variable**

    ![Initialize Variable](./assets/FlowInitializeVariable.png)

1. In the **Name** field type ```Approval Outcome```. And in the **Type** dropdown select **String**. Click the **arrow** to close out of this panel.

    ![Approval Outcome Varable](./assets/FlowVarApprovOutcome.png)

1. Select the **plus button** again below the initialize variable action you just added

    ![Plus Button](./assets/FlowPlusSecondVar.png)

1. Search for ```variable``` and select **initialize variable**

    ![Initialize Variable](./assets/FlowInitializeVariable.png)

1. In the **Name** field type ```Approval Message```. And in the **Type** dropdown select **String**. Click the **arrow** to close out of this panel.

    ![Days Since Purchase Varable](./assets/FlowVarApprovalMessage.png)

1. Select the **plus button** again below the initialize variable action you just added

    ![Days Since Purchase Varable](./assets/FlowVar2Plus.png)

1. Search for ```variable``` and select **initialize variable**

    ![Initialize Variable](./assets/FlowInitializeVariable.png)

1. In the **Name** field type ```Days Since Purchase```. And in the **Type** dropdown select **Integer**.

    ![Days Since Purchase Varable](./assets/FlowDaysSincePurchase.png)

1. In the **Value** Input of the Initialize Variable, select the **Fx** Button.

    ![Days Since Purchase Varable](./assets/FlowDaysPurcFx.png)

1. Select the **Create Expression with Copilot** Button

    ![Expression with Copilot](./assets/FlowCreateExpressionCopilot.png)

If you don't see the **Create Expression with Copilot** button you can copy and paste the following formula in the formula input.

```text
sub(int(div(sub(ticks(utcNow()), ticks(triggerBody()?['text_4'])),864000000000)),0)
```

1. In the box type the following:
```Calculate the number of days difference between the current date and the Purchase Date Input```

Select **Create Expression**

![Expression with Copilot](./assets/FlowCreateExpBtn.png)

1. Verify the formula in the **Suggested expression** box and select the **OK** button.

    ![OK Button](./assets/FlowCreateExpOK.png)

1. Verify the formula is added to the expression box and select the **Add** button

    ![Add Button](./assets/FlowCreateExpAdd.png)

1. Verify the expression shows in the value input as shown below, and click the **arrow** to close out of this panel.

    ![Verify and Close](./assets/FlowVarDaysConfig.png)

1. Click the **Plus Button** below the initialize variable.

    ![Expression Filled](./assets/FlowPlusDayPurVar.png)

1. Search for ```condition``` and select **Condition** under the control header.

    ![Select Condition](./assets/FlowConditionSearch.png)

1. Now we need to fill out the conditions we want to check for. To do that, click in the first input and select the **lightning bolt** icon

    ![Select Condition](./assets/FlowCondition1LightningBolt.png)

1. Select the **Days Since Purchase** variable

    ![Select Condition](./assets/FlowDaysSincePurchaseSelect.png)

1. Select the **is less or equal to** dropdown

    ![Select Condition](./assets/FlowDayPurLessEq.png)

1. In the right text box select the **lightning bolt** icon.

    ![Select Condition](./assets/FlowDayPurLight.png)

1. Select the **Coverage Window Days** Input

    ![Select Coverage Window](./assets/FlowCovWindowSelect.png)

1. Your condition should look like the screenshot below. We need to add one more condtion to this. To do that, select the **New item** button.

    ![New Condition](./assets/FlowCondNewItem.png)

1. Select **Add Row**

    ![Add Row](./assets/FlowCondAddRow.png)

1. Select the **lightning bolt** icon in the left text input

    ![Add Condition Lightning Bolt](./assets/FlowSecondConditionLightningBolt.png)

1. Select the **Issue Category** input.

    ![Issue Category](./assets/FlowIssueCategorySelect.png)

1. Change the condition dropdown to **is not equal to**

    ![Not Equal To](./assets/FlowConditionNotEqual.png)

1. In the right text input type ```Unknown```. Verify that your Condition action matches the screenshot below. Click the **arrow** to close out of this panel.

    ![Condition Filled](./assets/FlowConditionFilled.png)

1. Now that we have our conditions we want to check for, we need to tell the flow what would happen if it meets those conditions and what to do if it doesn't. To do this, expand out the **True** dropdown and select the **Plus button**

    ![Yes Add](./assets/FlowYesAddBtn.png)

1. Search for ```variable``` and select the **Set Variable** action.

    ![Set Variable](./assets/FlowYesSetVarSelect.png)

1. In the **Name** Dropdown select the **Approval Outcome** variable.  In the **Value** input type ```Auto-Approved```. What we're doing here is for our process, we want to auto-approve any warranty claims that aren't unknown cateogry and are within the coverage window. Click the **arrow** to close out of this window.

    ![Approval Outcome Config](./assets/FlowApprovalOutcomeConfig.png)

1. Now we want to fill in the approval notes. To do this, expand out the **True** dropdown and select the **Plus button**

    ![Yes Add](./assets/FlowCondTruePlus2.png)

1. Search for ```variable``` and select the **Set Variable** action.

    ![Set Variable](./assets/FlowYesSetVarSelect.png)

1. In the **Name** Dropdown select the **Approval Message** variable.  In the **Value** input type ```The Warranty Claim has been reviewed and meets all requirements to be auto-approved```. Click the **arrow** to close out of this window.

    ![Approval Message Config](./assets/FlowCondTrueVar2Config.png)

1. Now we need to tell the flow what to do if it doesn't meet these conditions. To configure this, expand the **False** section and select the **Plus Button**

    ![False Condtion Add](./assets/FlowCondFalsePlus.png)

1. Search for ```variable``` and select the **Set Variable** action.

    ![Set Variable](./assets/FlowYesSetVarSelect.png)

1. In the **Name** Dropdown select the **Approval Outcome** variable.  In the **Value** input type ```Needs Exception Approval```. This will return back to the user informing them it couldn't be auto-approved and escalation is needed. Click the **arrow** to close out of this window.

    ![Approval Outcome Config](./assets/FlowApprovalOutcomeConfigFalse.png)

1. Now we want to fill in the approval notes. To do this, select the **Plus button** in the false condition right below the set variable you just added.

    ![Yes Add](./assets/FlowApprovalOutcomeConfigPlus.png)

1. Search for ```variable``` and select the **Set Variable** action.

    ![Set Variable](./assets/FlowNoSetVarSelect.png)

1. In the **Name** Dropdown select the **Approval Message** variable.  In the **Value** input type ```The Warranty Claim has been reviewed and it is not within the approved warranty policy guidelines. You can request a review for an exception if you'd like.```. Click the **arrow** to close out of this window.

    ![Approval Message Config](./assets/FlowFalseApprovMessageConfig.png)

1. We are in the home stretch now. All that's left is to pass the data of the approval outcome back to the agent. To do that, scroll to the bottom and click to expand the **Respond to the agent** action and select the **Add an output** button

    ![Variable Filled](./assets/FlowRespondOutputBtn1.png)

1. Select **Text** for the output type

    ![Variable Filled](./assets/FlowRespondOutput1Type.png)

1. Type ```Approval Outcome``` in the left text box. Click in the right text box and select the **lightning bolt** icon

    ![Variable Filled](./assets/FlowRespondOutput1Lightning.png)

1. Select the **Approval Outcome** variable

    ![Variable Filled](./assets/FlowResponseOutput1Outcome.png)

1. Select **Add an Output** again

    ![Variable Filled](./assets/FlowResponseOutput2Btn.png)

1. Select **Text** as the Output Type

    ![Variable Filled](./assets/FlowResponseOutput2Type.png)

1. Type ```Approval Notes``` in the left text box. Click in the right text box and select the **Lightning bolt** icon.

    ![Variable Filled](./assets/FlowResponseOutput2Lightning.png)

1. Select the **Approval Message** variable

    ![Variable Filled](./assets/FlowResponseOutput2message.png)

1. Select the **Flow Checker** button to test your flow for errors and ensure no errors are found.

    ![Variable Filled](./assets/FlowCheckerBtn.png)

1. Select the **Save Draft** button

    ![Variable Filled](./assets/FlowSaveDraft.png)

1. Select the **Overview** button in the top navigation

    ![Variable Filled](./assets/FlowOverview.png)

1. Select the **Edit Button** in the Details section

    ![Variable Filled](./assets/FlowEditBtn.png)

1. Change the **Flow Name** to

    ```text
    Auto Approval Claims
    ```

1. In the **Description** input, type:

    ```text
    This agent flow evaluates a warranty claim against a condition to determine if it's eligible for auto-approval or needs escalation and returns a response to the agent.
    ```

1. Click the **Save** button.

    ![Variable Filled](./assets/FlowName.png)

1. Select the **Designer** tab in the top navigation to go back to the designer view.

    ![Variable Filled](./assets/FlowDesignerTab.png)

1. Select the **Publish** button

    ![Variable Filled](./assets/FlowPublish.png)

1. Select the **Agents** tab in the left hand side to get back to your agent.

    ![Variable Filled](./assets/FlowAgentsTab.png)

1. Select the **Zava Order Support** Agent

    ![Variable Filled](./assets/SelectZavaAgent.png)

1. Scroll down to the **Tools** section and select the **Add tool** button

    ![Variable Filled](./assets/FlowAddTool.png)

1. Select the **Flow** tab

    ![Variable Filled](./assets/FlowTab.png)

1. Select the **Auto Approval Claims** flow from the list

    ![Variable Filled](./assets/FlowSelect.png)

1. Select the **Add and Configure** button

    ![Variable Filled](./assets/FlowToolAdd.png)

1. Select the **Additional Details** section and select the **Agent may use this tool at any time** radio button.

    ![Variable Filled](./assets/FlowToolWhen.png)

1. Now we need to give additional details for how AI should pass the required inputs to the flow. To do this, scroll down to the **Inputs** section and select the **Customize** button next to the **Issue Category** input.

    ![Variable Filled](./assets/FlowToolCustIssue.png)

1. In the **Description** text box, type

     ```text
     Fill with the issue category extracted from the Claims Processing Tool
     ```

    ![Variable Filled](./assets/FlowToolIssDesc.png)

1. Select the **Customize** button next to the **Purchase Date** input.

    ![Variable Filled](./assets/FlowToolCustPurcDate.png)

1. In the **Description** text box, type

     ```text
     Fill with the Purchase Date extracted from the Claims Processing Tool
     ```

    ![Variable Filled](./assets/FlowToolCustPurDateDesc.png)

1. Select the **Customize** button next to the **Coverage Window Days** input.

    ![Variable Filled](./assets/FlowToolCustCoverage.png)

1. In the **Description** text box, type

     ```text
     Fill with the numeric (in days) value of the Coverage Window extracted from the Warranty Policy
     ```

    ![Variable Filled](./assets/FlowToolCustDesc.png)

1. Scroll down to the **Completion** section and select the **Write the response with generative AI** option from the **After Running** dropdown

    ![Variable Filled](./assets/FlowToolAfterRUnning.png)

1. Select the **Save** button

    ![Variable Filled](./assets/FlowToolSave.png)

1. Select the **Overview** tab

    ![Variable Filled](./assets/FlowToolOverview.png)

1. Select the **Instructions** section and select the **Edit** button

    ![Variable Filled](./assets/FlowInstructionsEditBtn.png)

1. Remove the last line about "respond in chat...". Type ```After all of the data is extracted, call the``` and put a forward slash (/) so the tool selection screen comes up and select the **Auto Approval Claims** tool.

    ![Variable Filled](./assets/InstructionsClaimApprovalToolSelection.png)

1. Finish drafting the additional instructions by pasting in the following after the tool selection:
```tool. Pass all the required info and return the approval outcome for the warranty claim and approval message to the user to finish the process. Inform the user that an approval process has been started and an answer should be given shortly while you are waiting for the approval to process.```.

Select the **Save** button in the instructions section when done.

![Variable Filled](./assets/FlowToolInstructionssave.png)

You've just added an agent flow to handle warranty claim auto-approvals to your agent! Now all that's left to do is test.
