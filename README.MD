<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD041 -->
<p align="center">
<img src="img/Banner-MS-AI-Tour-26.png" alt="decorative banner" width="1200"/>
</p>

# [Microsoft AI Tour 2026](https://aitour.microsoft.com)

## 🔥WRK532: Building Agentic Solutions with Copilot Studio

If you will be delivering this session, check the [session-delivery-sources](./session-delivery-resources/) folder for slides, scripts, and other resources.

### Session Description

This 75-minute hands-on workshop with Microsoft Copilot Studio guides you through building agentic solutions with Copiilot Studio. You'll learn how to build, integrate, automate, and deploy a fully functional agent using tools like Agent Flows and MCP. You'll walk away with practical skills to customize agents for real-world business needs.

### 🧠 Learning Outcomes

By the end of this session, learners will be able to:

- Create an agent from scratch in Copilot Studio
- Know when and how to integrate Agents Flows
- Understand MCP and how to integrate MCP Severs with agents
- See how to test and deploy an agent

### 💻 Technologies Used

- Microsoft Copilot Studio
- Agent Flows
- MCP

### 🔗 Session Resources

| Resource | Path |
|---|---:|
| Presenter Guide (full) | [session-delivery-resources/readme.md](session-delivery-resources/readme.md)
| Slides | [WRK532_Presentation.pptx](https://assetsmanagement952e.blob.core.windows.net/assets/WRK532%20Building%20agentic%20solutions%20with%20Copilot%20Studio/WRK532_Presentation_V1.0.pptx) |
| TTT Video | [WRK532-Full-Session.mp4](https://assetsmanagement952e.blob.core.windows.net/assets/WRK532%20Building%20agentic%20solutions%20with%20Copilot%20Studio/WRK532_Delivery_V1.0.mp4) |

### 📚 Continued Learning Resources

| Resources          | Links                             | Description        |
|:-------------------|:----------------------------------|:-------------------|
| Copilot Studio Resources | [https://aka.ms/copilotstudio-getstarted](https://aka.ms/copilotstudio-getstarted)
| AI Tour 2026 Resource Center | [https://aka.ms/AITour26-Resource-Center](https://aka.ms/AITour26-Resource-Center?ocid=AITour26_resourcecenter_cnl) | Links to all repos for AI Tour 26 Sessions |
| Azure AI Foundry Community Discord | [![Microsoft Azure AI Foundry Discord](https://dcbadge.limes.pink/api/server/ByRwuEEgH4)](https://discord.com/invite/ByRwuEEgH4)| Connect with the Azure AI Foundry Community! |
| Learn at AI Tour | [https://aka.ms/LearnAtAITour](https://aka.ms/LearnAtAITour?ocid=AITour26_resourcecenter_cnl) | Continue learning on Microsoft Learn |

## Content Owners

<table>
<tr>
    <td align="center"><a href="http://github.com/aprildunnam">
        <img src="https://github.com/aprildunnam.png" width="100px;" alt="April Dunnam"/><br />
        <sub><b> April Dunnam</b></sub></a><br />
            <a href="https://github.com/aprildunnam" title="talk">📢</a>
    </td>
    <td align="center"><a href="http://github.com/laskewitz">
        <img src="https://github.com/laskewitz.png" width="100px;" alt="Daniel Laskewitz"/><br />
        <sub><b>Daniel Laskewitz</b></sub></a><br />
            <a href="https://github.com/laskewitz" title="talk">📢</a>
    </td>
</tr></table>

##

## Responsible AI

Microsoft is committed to helping our customers use our AI products responsibly, sharing our learnings, and building trust-based partnerships through tools like Transparency Notes and Impact Assessments. Many of these resources can be found at [https://aka.ms/RAI](https://aka.ms/RAI).
Microsoft’s approach to responsible AI is grounded in our AI principles of fairness, reliability and safety, privacy and security, inclusiveness, transparency, and accountability.

Large-scale natural language, image, and speech models - like the ones used in this sample - can potentially behave in ways that are unfair, unreliable, or offensive, in turn causing harms. Please consult the [Azure OpenAI service Transparency note](https://learn.microsoft.com/legal/cognitive-services/openai/transparency-note?tabs=text) to be informed about risks and limitations.

The recommended approach to mitigating these risks is to include a safety system in your architecture that can detect and prevent harmful behavior. [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/overview) provides an independent layer of protection, able to detect harmful user-generated and AI-generated content in applications and services. Azure AI Content Safety includes text and image APIs that allow you to detect material that is harmful. Within Azure AI Foundry portal, the Content Safety service allows you to view, explore and try out sample code for detecting harmful content across different modalities. The following [quickstart documentation](https://learn.microsoft.com/azure/ai-services/content-safety/quickstart-text?tabs=visual-studio%2Clinux&pivots=programming-language-rest) guides you through making requests to the service.

Another aspect to take into account is the overall application performance. With multi-modal and multi-models applications, we consider performance to mean that the system performs as you and your users expect, including not generating harmful outputs. It's important to assess the performance of your overall application using [Performance and Quality and Risk and Safety evaluators](https://learn.microsoft.com/azure/ai-studio/concepts/evaluation-metrics-built-in). You also have the ability to create and evaluate with [custom evaluators](https://learn.microsoft.com/azure/ai-studio/how-to/develop/evaluate-sdk#custom-evaluators).

You can evaluate your AI application in your development environment using the [Azure AI Evaluation SDK](https://microsoft.github.io/promptflow/index.html). Given either a test dataset or a target, your generative AI application generations are quantitatively measured with built-in evaluators or custom evaluators of your choice. To get started with the azure ai evaluation sdk to evaluate your system, you can follow the [quickstart guide](https://learn.microsoft.com/azure/ai-studio/how-to/develop/flow-evaluate-sdk). Once you execute an evaluation run, you can [visualize the results in Azure AI Foundry portal](https://learn.microsoft.com/azure/ai-studio/how-to/evaluate-flow-results).
