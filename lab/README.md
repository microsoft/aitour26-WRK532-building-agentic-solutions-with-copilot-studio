# Building agentic solutions with Copilot Studio

These instructions are for participants of the **instructor-led** Workshop Building Agentic Solutions with Copilot Studio at Microsoft AI Tour 2026.  Register to attend in a city near you at [Microsoft AI Tour](https://aitour.microsoft.com/).

## Lab Overview

This hands-on session with Microsoft Copilot Studio guides you through the full agent lifecycle—from purpose-driven design to advanced capabilities. Learn how to build, integrate, automate, and deploy a fully functional agent using tools like Agent Flows and MCP. Walk away with practical skills to customize agents for real-world business needs.

## Pre-Requisites for AI Tour

To participate in this lab, you will need:

1. Your own laptop.
   * It need only be capable of running a browser, so almost any laptop will do.
   * A recent version of Edge, Chrome or Safari is recommended.

## Pre-Requisites for at home

If you want to run this lab by yourself, make sure to install the following software:
- [Visual Studio Code](https://code.visualstudio.com/download)
- [Python](https://www.python.org/downloads/)
- [DevTunnels CLI](https://learn.microsoft.com/en-us/azure/developer/dev-tunnels/get-started?tabs=windows)

> [!IMPORTANT]
> In the instructions you will see some content that has +++ around them, in the Skillable environment that transforms to clickable text that will autotype in the VM. That will not work when you work at home. Also, variables will resolve in the Skillable environment, but not when you run it at home. Those will be shown as the variable name. For instance +++@lab.CloudCredential(CSBatch1).Username+++ will show in the home version and in the Skillable environment this will show as an autotype field for the username. When you run this at home, use your own username for that. This will also apply to TAP / Password fields and other variables.

## Get Started

The lab consist of multiple sections:

- [00-Introduction](./instructions/00-Introduction.md)
- [01-Build Your Agent](./instructions/01-Build-Your-Agent.md)
- [02-Connect To An MCP Server](./instructions/02-Connect-To-An-MCP-Server.md)
- [03-Add A Prompt For Warranty Claim Processing](./instructions/03-Add-A-Prompt-For-Warranty-Claim-Processing.md)
- [04-Add An Agent Flow For Approving Warranty Claims](./instructions/04-Add-An-Agent-Flow-For-Approving-Warranty-Claims.md)
- [05-Test Your Agent](./instructions/05-Test-Your-Agent.md)

## Source code

The source code for this session can be found in the [src folder](../src) of this repo.
