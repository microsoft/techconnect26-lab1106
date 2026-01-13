# Design Agent Lab Instructions

## Microsoft Copilot Studio – Azure Architecture Generator

**Version:** 1.0  
**Last Updated:** January 7, 2026  
**Audience:** Microsoft Architects and Consultants  
**Duration:** 90 minutes

---

## 📋 Table of Contents

1. [Lab Overview](#lab-overview)
2. [Prerequisites](#prerequisites)
3. [Module 1: Solution Import](#module-1-solution-import)
4. [Module 2: Connection Configuration](#module-2-connection-configuration)
5. [Module 3: Knowledge Base Setup](#module-3-knowledge-base-setup)
6. [Module 4: Testing the Agents](#module-4-using-the-design-agent-interactive-mode)
7. [Module 5: Autonomous Agent Mode](#module-5-autonomous-agent-mode)
8. [Module 6: Topic Walkthrough – Generate and Save Azure Architecture Doc](#module-6-topic-walkthrough--generate-and-save-azure-architecture-doc)
9. [Module 7: Design Agent Lab 300-400] (#module-7-Design-Agent-adding-Cost-Estimation-Topic)
10. [Module 8: Understanding the Output](#module-8-understanding-the-output)
11. [Module 9: Publishing to Channels](#module-9-publishing-to-channels)
12. [Appendix: Troubleshooting](#appendix-troubleshooting)

===

## Lab Overview

### Introduction

The **Intake Agent** and **Design Agent** are a Microsoft Copilot Studio–built architecture generator that leverages deep-reasoning capabilities (GPT-5 Reasoning model) to transform application intake data into comprehensive Azure architectural designs. This solution enables rapid generation of baseline Azure architectures, significantly accelerating the design phase of cloud migration and modernization engagements.

### What You Will Learn

By the end of this lab, you will be able to:

- ✅ Import the Intake Agent and Design Agent solutions into your Copilot Studio environment
- ✅ Configure required connections (SharePoint, Email)
- ✅ Upload and configure knowledge base files
- ✅ Generate complete Azure architecture documents from intake data
- ✅ Understand the five standardized architecture views
- ✅ Interpret the Azure Resource Configuration tables

### Key Capabilities

The Design Agent produces:

| Output | Description |
|--------|-------------|
| **Formal Introduction** | Application overview and context |
| **Data Flows** | Main data movement and processing patterns |
| **Architecture Overview** | High-level technical summary |
| **Five Architecture Views** | Logical, High-Level Technical, Detailed Infrastructure, Networking, Observability |
| **Rationales** | Design decisions aligned with WAF and SCF |
| **Resource Configuration Table** | Deployment-ready Azure resource specifications |

===

## Prerequisites (10 minutes)

### Required Access

- [ ] Microsoft 365 account with Copilot Studio license
- [ ] Power Platform environment with Dataverse
- [ ] SharePoint site for document storage
- [ ] Power Automate premium connectors access
- [ ] GPT-5 Reasoning (Preview) model access in Copilot Studio

### Required Files

- [ ] Design Agent solution package (`.zip` file)
- [ ] Azure Resource Table Sample.txt (Knowledge file)
- [ ] Sample intake document (PDF or Word format)

### Environment Setup Checklist

| Component | Status |
| ----------- | -------- |
| Copilot Studio access | ⬜ Verified |
| Power Platform environment | ⬜ Created |
| SharePoint document library | ⬜ Configured |
| Email connector | ⬜ Available |

#### Step 1: SharePoint Site Configuration
1. Open the Edge browser
2. Click on waffle icon first, then click on Microosft 365 and click Sign in in the top right:

![Browser](<0.1_00-Sign-in-Office 365.png>)

![Office365](<0.1_02-Sign-in-Office 365.png>)

**Username: +++@lab.CloudPortalCredential(User1).Username+++**

For the **user's password**, provide the following value:

**Password: +++@lab.CloudPortalCredential(User1).Password+++**

> [!TIP]
> If the login UI prompts you for the user's **temporary password**, provide the following value:
> 
> **Temporary Access Pass: +++@lab.CloudPortalCredential(User1).AccessToken+++**

2. On the left pannel, click on Apps/SharePoint/Open in new tab

![Sharepoint](0.2_01-Open-SharePoint.png)

3. Close the Welcome window
4. Click on **Create site** then click on **Team site**

![Site](0.2_02-Create-Site.png)

> [!TIP]
> If window in blank refresh browser

5. Select **Standard team**
6. Click **Use template**
7. Type name of your site and click on **Next**

![SiteName](0.2_07-Create-Site.png)

8. Click on **Create**
9. Let **Add members** box in blak and click on **Finish**
10. Create the Folder Structure 
 ```
📁 Documents
├── 📁 Intake-Documents                   
│   └── 📄 [AppName]-Intake.pdf
├── 📁 Architecture-Documents   
│   └── 📄 [AppName]-Target-Azure-Architecture-v1.0.md
```

On the left menu click on **Document**, click on **+ Create or upload**, click on **Folder**. Type Name of the folder
   
![Folders](0.2_10-Create-Folders.png)





===
## Module 1: Solution Import (10 minutes)

### Step 1.1: Access Copilot Studio

1. Open the Edge browser and navigate to +++https://copilotstudio.microsoft.com+++ and login with the following suggested Microsoft 365 work or school account:

**Username: +++@lab.CloudPortalCredential(User1).Username+++**

For the **user's password**, provide the following value:

**Password: +++@lab.CloudPortalCredential(User1).Password+++**

> [!TIP]
> If the login UI prompts you for the user's **temporary password**, provide the following value:
> 
> **Temporary Access Pass: +++@lab.CloudPortalCredential(User1).AccessToken+++**

2. Wait between 10 and 15 seconds for the process to configure your personal developer environment to start. You will see a dialog informing you about the ongoing process of creating your personal environment.

![The dialog informing about the developer environment creation.](https://raw.githubusercontent.com/microsoft/ignite25-LAB564-architect-a-goal-driven-ai-agent-with-copilot-studio/refs/heads/main/img/mcs-creating-environment-01.png)

3. If this is the very first time you run Copilot Studio you will need to select your country and to select the **Get Started** button.

![The web page to start using Copilot Studio. You need to provide your country, to choose whether you want to receive messages from Microsoft about offerts, and to select to "Get Started".](https://raw.githubusercontent.com/microsoft/ignite25-LAB564-architect-a-goal-driven-ai-agent-with-copilot-studio/refs/heads/main/img/mcs-get-started-01.png)

4. Skip, or go through, the "Welcome to Copilot Studio!" dialog window

### Step 1.2: Navigate to Solutions

1. Click on **Create** on the top right 

![Refresh](1.2_00-Navigate-to-Solutions.png)

2. In the left navigation pane, click on **Solutions**
> [!TIP]
> If Solutions is not visible, click **More** (•••) to expand the menu

### Step 1.3: Import the Solution

![Refresh](1.3_00-Import-solutions.png)


#### Step 1.3.1: Import Intake agent

1. Click **Import solution** from the command bar
2. Click **Browse** select the Design Agent solution package (`AIMigrateIntakeAgent_1_0_0_7.zip` file)

![Browse](1.3.1_00-Import-Intake-Agent-Solution.png)

3. Click **Open**
4. Click **Next**
5. Click **Next**
6. When green check is in all services then click **Import**

![Import](1.3.1_01-Import-Intake-Agent-Solution.png)

#### Step 1.3.2: Import Design agent

1. Click **Import solution** from the command bar
2. Click **Browse** select the Design Agent solution package (`AIMigrateDesignAgent_1_0_0_9.zip` file)

![Browse](1.3.2_00-Import-Design-Agent-Solution.png)

3. Click **Open**
4. Click **Next**
5. Click **Next**
6. When green check is in all services then click **Import**

![Import](1.3.2_01-Import-Design-Agent-Solution.png)


**5. Wait until the solutions are imported**

![Import](1.3_01-Import-Solutions.png)

> [!TIP]
> Refresh the browser if don't see the agents

### Step 1.4: Configure Import Settings
#### Step 1.4.1: Configure Intake Agent Settings
1. Select the Intake Agent
2. Click on **Copilot Studio icon**

![IntakeAgentSettings](1.4.1_00-Intake-Agent-Settings.png)

2. On the left menu click on Agents
3. Click on **Tools** on the top ribbon

![Outlook](1.4.1_02-Intake-Agent-Outlook.png)

4. Scroll down to **Inputs** and in Input Name **To**, **Value field** replace it by **Username: +++@lab.CloudPortalCredential(User1).Username+++**

5. **Save**

![Outlook](1.4.1_03-Intake-Agent-Outlook.png)

#### Step 1.4.2: Configure Design Agent Settings

1. Once imported, locate **Application Design Agent** in your Agents list
2. Click on the Agent name
3. Verify the agent overview displays correctly:

![DesignAgent](1.4.2_00-Design-Agent.png)

**Expected Overview Screen:**

![Welcome](008-Welcome-message.png)

===
## Module 2: Connection Configuration (11 minutes)

After importing the solution, you must establish connections for the agent to function correctly.

### Step 2.1: Identify Required Connections

#### Step 2.1.1 Intake Agent Connections

1. Click on **App Intake Agent v1.3.4** from the list of **My Agents**

   click **Settings**

![Imported](1.4.1_00-Intake-Agent-Settings.png)

2. Click on **Connection Settings** on the left menu, select one of the two connections and click **Connect** 

![IntakeAgentConnections](1.4.1_01-Intake-Agent-Connections.png)

3. Click **Submit**

![Submit](1.4.1_02-Intake-Agent-Submit.png)

4. Close (Do the same steps with the other connection)

#### Step 2.1.2 Design Agent Connections
The Design Agent requires the following connections:

| Connection | Purpose |
|------------|---------|
| **SharePoint** | Store and retrieve intake documents and generated architectures |
| **Office 365 Outlook** | Send generated documents via email |
| **Microsoft Learn Docs MCP** | Knowledge |

Click **Application Design Agent** from the list of Agents

![DesignAgent](1.4.2_00-Design-Agent.png)

navigate to **Settings** > **Connections**

![Settings](2.1_00-Settings.png)

![Connections](2.1_01-Connection-settings.png)

##### Step 2.1.2.1: Configure SharePoint Connection (1 minute)

1. Locate the **Save Design Document** connection reference
2. Click **Connect**

![SharePointConnection](2.1.2.1_00-Design-Agent-SharePoint-Connection.png)

3. Confirm is signed with the credentials that have access to your target SharePoint site, click **Submit**

![SharePointConnection](2.1.2.1_01-Design-Agent-SharePoint-Connection.png)


##### Step 2.1.2.2: Configure Email Connection (1 minute)

1. Locate the **Office 365 Outlook** connection reference
2. Click **Connect**

![OutlookConnection](2.1.2.1_02-Design-Agent-Outlook-Connection.png)

3. Confirm is signed with the credentials that have access to your target SharePoint site, click **Submit**

![outlookConnection](2.1.2.1_03-Design-Agent-Outlook-Connection.png)

##### Step 2.1.2.2: Configure MCP Connection (1 minute)

1. Locate the **Microsoft LearnDocs MCP** connection reference
2. Click **Connect**

![MCP](2.1.2.1_04-Design-Agent-MCP-Connection.png)

3. Confirm is signed with the credentials that have access to your target SharePoint site, click **Submit**

![MCP](2.1.2.1_05-Design-Agent-MCP-Connection.png)

##### Step 2.1.2.3: Verify All Connections (''20)

2. Verify all connections show **Connected** status:

| Connection | Status |
|------------|--------|
| Office 365 Outlook | ✅ Connected |
| Microsoft Learn Docs MCP | ✅ Connected |
| Save Design Document | ✅ Connected |

Then Close **Settings** window

![Connections](2.1.2.3-Connections.png)



### Step 2.2: Review Flow Connections

1. Navigate to **Flows** on the left menu in Copilot Studio
2. Review connection references:
   - **Save Design Document** - SharePoint connection - **Status:Published**
         ##### 2.2.1 Edit the Flow

   - **ExtractDocumentText** – SharePoint connection - **Status:Published**
   - **Invoke Design Agent** - Sharepoint, Copilot Studio connection - **Status:Draft**
        ##### 2.2.2 Edit the Flow
        ![InvokeDesignAgentFlow](2.2_00-Invoke-Agent-Flow.png)

        Click on **When a file is created or modified (properties only)** and **Get file content**

        ![InvokeDesignAgentFlow](2.2_01-Invoke-Agent-Flow.png)

        In the action **When a file is created or modified (properties only)** delete content in *Site Address* and click on display button, select site address from the list (the one created in step 10 of Prerequisites) and Select Intake Folder. 
        In the action **Get file content** delete content in *Site Address* and click on display button, select site address from the list (the one created in step 10 of Prerequisites). Once is done click on **Publish**

        ![InvokeDesignAgentFlow](2.2_02-Invoke-Agent-Flow.png)

   - **Save Design to SharePoint v1** – SharePoint, Outlook connections
         
        ##### 2.2.3 Edit the Flow
        ![SaveDesigntoSharepoint_v1](2.2_03-SaveDesigntoSharepoint_v1-Flow.png)

        Click on **Create file** and **Get file properties**

        ![SaveDesigntoSharepoint_v1](2.2_04-SaveDesigntoSharepoint_v1-Flow.png)

        In the action **Create file** delete content in *Site Address* and click on display button, select site address from the list (the one created in step 10 of Prerequisites). Delete content in *Folder Path*, click on folder icon and select Generated Architectures folder. 
        In the action **Get file properties** delete content in *Site Address* and click on display button, select site address from the list (the one created in step 10 of Prerequisites). Delete content in *Library Name*, click on display button and select *Document*. Once is done click on **Publish**

        ![SaveDesigntoSharepoint_v1](2.2_05-SaveDesigntoSharepoint_v1-Flow.png)

3. Review all flows status = **Published**
![ConnectionReferences](2.2_06-SaveDesigntoSharepoint_v1-Flow.png)

===

## Module 3: Knowledge Base Setup (1 minute)

The Intake Agent and Design Agent use a knowledge file to ensure output structure matches deployment requirements.

### Step 3.1: Navigate to Knowledge (30 seconds)

1. In Copilot Studio, open the **App Intake AGent v1.3.4** from the list of Agents
2. Click the **Knowledge** tab in the top navigation

![IntakeAgentKnowledge](3.1_00-IntakeAgentKnowledge.png)

> ℹ️ The knowledge is **not mandatory**. If absent, the agent proceeds using the data points and instructions.

3. Open the **Application Design Agent** from the list of Agents
4. Click the **Knowledge** tab in the top navigation

![DesignAGentKnowledge](3.1_01-IntakeAgentKnowledge.png)

> 📄 **Knowledge File Purpose:** This text-based file guides the agent to produce resource configuration tables in a format compatible with the deployment agent.

### Step 3.3: Add Additional Knowledge (Optional)

To add custom knowledge sources:

1. Click **+ Add knowledge**
2. Select source type:
   - **Files** – Upload PDF, Word, or text documents
   - **SharePoint** – Connect to document libraries
   - **Public website** – Enable web search (if required)

3. Upload your file and wait for processing to complete
4. Verify status shows **Ready**

### Step 3.4: Configure Web Search (Optional)

Web Search allows the agent to reference public documentation:

```
Web Search: Disabled (Recommended for secure environments)
```

> ⚠️ **Security Note:** Keep Web Search disabled for engagements involving sensitive customer data.

===

## Module 4: Testing the Agents (25 minutes)
### 4.1 Intake Agent
1. Select the App Intake Agent v1.3.4 from the list of Agents

![TestingIntakeAgent](4.1_00-TestIntakeAgent.png)

2. Start with:

   "Here is the architectural document for 'SmartLogistics'. Please review it and only ask what's missing."
   Before send the prompt attached the App Overview - Smartlogistic.pdf file

   ![TestingIntakeAgent](4.1_01-TestIntakeAgent.png)

  
   Other prompts: 
      "Begin intake. I have an architecture document to upload."

      "Create a migration intake report for 'CRM Gateway' and email it to the migration team when done."

   

#### Conversation Flow & Behavior

   The agent follows these **core instructions**:
   *   **Greet and start** the conversation.
   *   During the introduction, **request the architectural document** for the application.
   *   If provided, **review its contents** and **only ask** questions **not answered** in the document, based on targeted data points for Azure migration.
   *   If not available, proceed to ask **up to 20 targeted questions** to gather essential data.
   *   **Collect details** about application infrastructure, dependencies, and **timeline dependencies in the next 6–12 months**.
   *   **Do not ask** about **migration timeline** (owners cannot decide it).
   *   Use these **data points** (see below) and ensure they are included in the **final report**.
   *   Maintain a **friendly and efficient** conversation, respecting the owner’s time.
   *   **Reference** the attached **questionnaire** (if configured) as a knowledge source for questions or report compilation.
   *   **Never list** all questions upfront; ask **one by one**.
   *   **Never ask** about **Treatment type** or **Complexity**; the agent **assesses** them based on collected data and presents them with justification.
   *   For **region**, ask **where the app is hosted** and **where users are**, with **user count ranges**.
   *   Always collect or extract **volumes**; if unknown/not in the doc, mark as **Missing Info** (avoid “large/small”).
   *   At the end, create a **filterable table** with all data points and **notes**, **grouped by categories**, visually emphasized where helpful.
   *   After the table, ask if the user is ready to **send intake data to the migration team**; if **Yes**, **convert to JSON** and **send via email**.
#### Data Points Captured & Report Structure

   **Categories & Fields** (extracted/asked; displayed in a filterable table with a **Notes** column):
   *   **📋 Overview**
      *   Application overview (max 10 lines)
      *   Business Criticality
      *   Customer Impact
      *   Assessed complexity (**0–100**) _(assessed by agent)_
      *   Suggested treatment _(refactor, rehost, replatform, rearchitect — minimal effort, max value; assessed by agent)_
   *   **🔐 Data & Privacy**
      *   Data Privacy requirements
      *   Data Volume
      *   Real-time data streaming requirements
      *   Batch data processing requirements
   *   **🧩 Architecture & Integrations**
      *   Current Tech / Integrations (internal & external)
      *   Dependency on other apps/data sources
      *   Service Integration Partners
      *   Automation
   *   **🌐 Environment & Regions**
      *   Regions/Locations (hosting & users; user count ranges)
      *   Network Access details
      *   Identity Providers
      *   Number of Environments and details
   *   **📅 Release & Dependencies**
      *   Release dependencies on corporate release cycle
      *   Timeline dependencies (next **6–12 months**)
   The final table is filterable/sortable in-channel, with **bold headers** and optional **icons** for quick scanning.


### 4.2 Design Agent (Interactive Mode)

The Design Agent supports two operational modes: **Interactive Mode** (covered in this module) and **Autonomous Mode** (covered in Module 5). This module focuses on the interactive conversation-based approach.

#### Step 4.1: Test the Agent

1. Select the **Application Design Agent** from the list of Agents
![TestingDesignAgent](4.2_00-TestingDesignAgent.png)

2. In the agent overview, locate the **Test your agent** panel on the right side
3. Review the agent's welcome message:
![TestingDesignAgent](4.2_01-TestingDesignAgent.png)

3. In the test panel, type one of the trigger phrases:
   ```
   Generate target Azure architecture details for the attached Application
   ```
4. Enter the application name when prompted:
   ```
   SmartLogistics
   ```
![alt text](4.2_01-TestingDesignAgent.png)

4. **Upload the intake document:**
   - Click **Browse** or drag and drop your file *Smar Logistics-Intake-2025-12-02.md*
   - Supported formats: PDF, DOCX, TXT
   - Select your intake document
   - Click **Open**

   ![TestDesignAgent](4.1_00-TestDesignAgent.png)

5. Wait for the agent to process (Average duration: ~71 seconds)

6. Don't move from the window until the response is completed

**Sample Intake Document Structure:**

```
Application Name: SmartLogistics
Business Criticality: High/Mission Critical
Regions: Primary - eastus2, Failover - westeurope
Compliance: GDPR, CCPA

Requirements:
- Real-time GPS telemetry processing
- Integration with SAP ERP
- Mobile and web client support
- 24x7 operations support
```

### Step 4.3: Generate Architecture Document



### Step 4.4: Review Generated Output

The agent will generate a comprehensive architecture document with the following structure:

**Document Structure:**

```
📦 [AppName] — Target Azure Architecture Details

├── 📋 Introduction
├── 🔄 Data Flows  
├── 🏗️ Architecture Overview
├── 📐 Detailed Description of Each View
│   ├── 1) Logical View — Conceptual
│   ├── 2) High-Level Technical View
│   ├── 3) Detailed Infrastructure View
│   ├── 4) Networking View
│   └── 5) Observability View
├── 📝 Rationales
├── ⚠️ Limitations
└── 📊 Azure Resource Table
```

===

## Module 5: Autonomous Agent Mode

The Design Agent can operate as a fully autonomous agent, automatically processing intake documents without user intervention. This mode is ideal for high-volume environments or when architects want to batch-process multiple application assessments.

### Step 5.1: Understanding Autonomous Mode

In Autonomous Mode, the agent:

```
┌─────────────────────────────────────────────────────────────────┐
│                    AUTONOMOUS WORKFLOW                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────────┐                                           │
│  │ 📁 SharePoint   | ← Intake document uploaded to             │
│  │  Intake-Documents│     designated folder
      Folder          │
│  └────────┬─────────┘                                           │
│           │                                                      │
│           ▼ (Trigger)                                           │
│  ┌──────────────────┐                                           │
│  │ 🤖 Design Agent  │ ← Automatically activated                 │
│  │    Triggered     │                                           │
│  └────────┬─────────┘                                           │
│           │                                                      │
│           ▼                                                      │
│  ┌──────────────────┐                                           │
│  │ 📄 Extract       │ ← App name extracted from filename        │
│  │    Document Data │   or document metadata                    │
│  └────────┬─────────┘                                           │
│           │                                                      │
│           ▼                                                      │
│  ┌──────────────────┐                                           │
│  │ 🏗️ Generate      │ ← Full architecture document              │
│  │    Architecture  │   created automatically                   │
│  └────────┬─────────┘                                           │
│           │                                                      │
│           ▼                                                      │
│  ┌──────────────────┐                                           │
│  │ 💾 Save to       │ ← Output stored in designated             │
│  │    SharePoint    │   output folder                           │
│  └────────┬─────────┘                                           │
│           │                                                      │
│           ▼                                                      │
│  ┌──────────────────┐                                           │
│  │ 📧 Email         │ ← Notification sent to                    │
│  │    Notification  │   stakeholders                            │
│  └──────────────────┘                                           │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Step 5.2: Configure SharePoint Intake Folder

#### 5.2.1 Access Triggers Configuration

1. In Copilot Studio, open the **Application Design Agent**
2. In the agent overview, locate the **Triggers** section
3. Click **+ Add trigger**

![SharepointTrigger](5.2_00-SharepointTrigger.png)

#### 5.2.2 Set Up SharePoint File Upload Trigger

1. Select **When an item is created** and click **Next**

![SharepointTrigger](5.2_01-SharepointTrigger.png)

2. Review the green checks in the apps and Click **Next**

![SharepointTrigger](5.2_02-SharepointTrigger.png)

2. Configure the trigger settings:

![SharepointTrigger](5.2_03-SharepointTrigger.png)

```
┌─────────────────────────────────────────────────────────────────┐
│  TRIGGER CONFIGURATION                                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Trigger Type:     When a file is created in SharePoint         │
│                                                                  │
│  Site Address:     https://[tenant].sharepoint.com/sites/       │
│                    DesignAgentSite                              │
│                                                                  │
│  Library Name:     Design Agent Documents                       │
│                                                                  │
│  Folder Path:      /Intake                                      │
│                                                                  │
│  File Filter:      *.pdf, *.docx, *.txt                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

3. Click **Save**

### Step 5.4: Automatic Data Extraction

When triggered autonomously, the agent extracts information without user intervention:

#### 5.4.1 Application Name Extraction

The agent extracts the application name using the following priority:

| Priority | Source | Example |
|----------|--------|--------|
| 1 | File name pattern | `SmartLogistics-Intake.pdf` → "SmartLogistics" |
| 2 | Document metadata | Title property in PDF/DOCX |
| 3 | Document content | First heading or "Application Name:" field |

**File Naming Convention:**
```
[ApplicationName]-Intake.[extension]
[ApplicationName]-Application-Intake-Summary.[extension]
[ApplicationName]-PRD.[extension]
```

#### 5.4.2 Intake Content Extraction

The Power Automate flow **ExtractDocumentText** automatically:

1. Retrieves the file from SharePoint
2. Extracts text content using AI Builder or document parsing
3. Passes the content to the Design Agent for processing

### Step 5.5: Automatic Document Generation and Storage

#### 5.5.1 Generation Process

Once triggered, the agent:

1. Processes the intake document through all generation nodes
2. Creates the complete architecture document with all five views
3. Generates the Azure Resource Configuration table

#### 5.5.2 Output Storage

The generated document is automatically saved to SharePoint:

```
Output Location: /Design Agent Documents/Generated Architectures/
File Name:       [AppName]-Target-Azure-Architecture-v1.0.md
Format:          Markdown with embedded Mermaid diagrams
```

**Metadata Updated:**
- Processing Status → "Completed"
- Processed Date → Current timestamp
- Generated Document → Link to output file



### Step 5.7: Testing Autonomous Mode

1. **Prepare a test intake document** with proper naming:
   ```
   TestApp-Intake.pdf
   ```

2. **Upload to the Intake folder:**
   - Navigate to SharePoint > Design Agent Documents > Intake
   - Upload the test document

3. **Monitor processing:**
   - Check the **Processing Status** column in SharePoint
   - View Power Automate flow run history for details

4. **Verify outputs:**
   - Check the **Generated Architectures** folder for the output
   - Confirm email notification was received

### Step 5.8: Autonomous Mode Best Practices

| Best Practice | Recommendation |
|---------------|----------------|
| File naming | Use consistent `[AppName]-Intake` pattern |
| Document format | PDF works best for text extraction |
| Batch processing | Upload multiple files; they process sequentially |
| Error handling | Monitor the Archive folder for failed documents |
| Notifications | Configure team distribution list for visibility |

===

## Module 6: Topic Walkthrough – Generate and Save Azure Architecture Doc

This module provides a detailed walkthrough of the main topic flow that powers the Design Agent.

### Step 6.1: Access the Topic

1. In Copilot Studio, open the **Application Design Agent**
2. Click the **Topics** tab in the top navigation
3. Locate and click on **"Generate and save Azure architecture doc"**

### Step 6.2: Understanding the Topic Flow

The topic consists of several key components arranged in a logical flow:

```
┌─────────────────────────────────────────────────────────────────┐
│                        TOPIC FLOW DIAGRAM                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌─────────┐                                                    │
│  │ Trigger │ ← "The agent chooses"                              │
│  └────┬────┘   Generates a target Azure architecture design...  │
│       │                                                          │
│       ▼                                                          │
│  ┌────────────────────┐                                         │
│  │ Set variable value │ ← Initialize variablesText = ""         │
│  └────────┬───────────┘                                         │
│           │                                                      │
│       ┌───┴───┐                                                 │
│       ▼       ▼                                                  │
│  ┌─────────┐  ┌──────────────────┐                              │
│  │Condition│  │All other conditions│                            │
│  │varApp   │  │                    │                            │
│  │is Blank │  │Set variablesText = │                            │
│  └────┬────┘  │"ActivityText"      │                            │
│       │       └────────────────────┘                            │
│       ▼                                                          │
│  ┌──────────┐                                                   │
│  │ Question │ ← "Enter the App Name"                            │
│  │ Identity:│   Save response as: var1 (string)                 │
│  │ User's   │                                                   │
│  │ entire   │                                                   │
│  │ response │                                                   │
│  └────┬─────┘                                                   │
│       │                                                          │
│       ▼                                                          │
│  ┌────────────────────┐                                         │
│  │ Set variable value │ ← varApp = var1                         │
│  └────────┬───────────┘                                         │
│           │                                                      │
│           ▼                                                      │
│  ┌──────────┐                                                   │
│  │ Question │ ← "Please upload the intake requirements..."      │
│  │ Identity:│   Save response as: varFile (record)              │
│  │ File     │                                                   │
│  └────┬─────┘                                                   │
│       │                                                          │
│       ▼                                                          │
│  ┌──────────────────────────┐                                   │
│  │ Action                   │                                   │
│  │ Power Automate Input(s): │                                   │
│  │   NoContent (Record) ←   │                                   │
│  │   varFile: record        │                                   │
│  │                          │                                   │
│  │ ┌──────────────────────┐ │                                   │
│  │ │ ExtractDocumentText  │ │                                   │
│  │ │ View flow details    │ │                                   │
│  │ └──────────────────────┘ │                                   │
│  │                          │                                   │
│  │ Outputs:                 │                                   │
│  │   intakeDocumentN..string│                                   │
│  │   intakeDocumentC..string│                                   │
│  └────────┬─────────────────┘                                   │
│           │                                                      │
│           ▼                                                      │
│  ┌────────────────────┐                                         │
│  │ Set variable value │ ← variablesText = intakeDocumentC...    │
│  └────────┬───────────┘                                         │
│           │                                                      │
└───────────┼─────────────────────────────────────────────────────┘
            │
            ▼
        [Continued in Step 5.3]
```

### Step 6.3: Generation Nodes

After document extraction, the flow continues with a series of generation nodes:

```
┌─────────────────────────────────────────────────────────────────┐
│                    GENERATION NODES                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌───────────────────────────┐                                  │
│  │ 🤖 GenerateIntroAndOverview│                                  │
│  │   Input: varApp (string)   │                                  │
│  │   Data source: Text        │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                  │
│               ▼                                                  │
│  ┌───────────────────────────┐                                  │
│  │ 🤖 GenerateDataFlows       │                                  │
│  │   Input: varApp (string)   │                                  │
│  │   Data source: Text        │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                  │
│               ▼                                                  │
│  ┌───────────────────────────┐                                  │
│  │ 🤖 GenerateDetailedViews   │                                  │
│  │   Input: varApp (string)   │                                  │
│  │   Data source: Text        │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                  │
│               ▼                                                  │
│  ┌───────────────────────────┐                                  │
│  │ 🤖 GenerateRationale       │                                  │
│  │   Input: varApp (string)   │                                  │
│  │   Data source: Text        │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                  │
│               ▼                                                  │
│  ┌───────────────────────────┐                                  │
│  │ 🤖 GenerateAzureResourceTable│                                │
│  │   Input: varApp (string)   │                                  │
│  │   Data source: Text        │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                  │
│               ▼                                                  │
│  ┌───────────────────────────┐                                  │
│  │ Set variable value        │                                  │
│  │   varArchitectureDoc =    │                                  │
│  │   [Combined outputs]      │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                  │
│               ▼                                                  │
│         [Save/Send Flow]                                        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Step 6.4: Key Topic Components Explained

#### 6.4.1 Trigger Node
- **Type:** Agent-initiated trigger
- **Description:** "Generates a target Azure architecture design document for a given application"
- **Activation:** The agent chooses when to invoke this topic based on user intent

#### 6.4.2 Variable Initialization
```
Set variable: variablesText
To value: ""
```
Initializes the text variable that will hold the intake document content.

#### 6.4.3 Condition Node
Checks if the application name (`varApp`) is already provided:
- **If Blank:** Prompts user for the application name
- **All Other Conditions:** Proceeds with existing value

#### 6.4.4 Question Nodes

**Application Name Question:**
```
Prompt: "Enter the App Name"
Identity: User's entire response
Save as: var1 (string)
```

**File Upload Question:**
```
Prompt: "Please upload the intake requirements..."
Identity: File
Save as: varFile (record)
```

#### 6.4.5 ExtractDocumentText Action
This Power Automate flow:
- **Input:** `varFile` (the uploaded document)
- **Process:** Extracts text content from PDF/DOCX
- **Outputs:**
  - `intakeDocumentName` (string) – File name
  - `intakeDocumentContent` (string) – Extracted text

#### 6.4.6 Generation Prompts
Each generation node uses the GPT-5 Reasoning model with specific prompts:

| Node | Purpose | Output |
|------|---------|--------|
| GenerateIntroAndOverview | Creates introduction and architecture overview | Markdown content |
| GenerateDataFlows | Documents data movement patterns | Markdown content |
| GenerateDetailedViews | Produces the five architecture views with Mermaid diagrams | Markdown + Mermaid |
| GenerateRationale | Explains design decisions | Markdown content |
| GenerateAzureResourceTable | Creates resource configuration table | Markdown table + plain text |

### Step 6.5: Modifying the Topic

To customize the topic for specific customer needs:

1. **Click on any node** to view its properties
2. **Edit prompts** by clicking the prompt text in generation nodes
3. **Add conditions** by clicking **+** between nodes
4. **Add actions** to integrate with additional Power Automate flows

**Common Customizations:**

| Customization | How To |
|---------------|--------|
| Add additional views | Duplicate a generation node and modify the prompt |
| Change output format | Edit the generation prompt to specify format requirements |
| Add approval workflow | Insert a Power Automate action before save |
| Email to multiple recipients | Modify the save/send flow in Power Automate |

===
## Module 7:  Design Agent adding Cost Estimation Topic

# 📘 Lab Option 1: Add Cost Estimation Section

**Difficulty:** Level 300 | **Duration:** 10 minutes


🎯 Learning Objectives
- Add a new generative AI action to an existing Topic to include Azure Resources Cost Estimation
- Chain outputs between Topic actions
- Modify document assembly logic


Step 1: Open the Topic in Copilot Studio (1 min)
- Navigate to Copilot Studio → Topics
- Open the "Generate and save Azure architecture doc" Topic
- Scroll down to the GenerateAzureResourcesTable Action 
- Click + to add a new Action, select Advanced -> Generative Answers ![alt text](image-1.png)
- Name the Action as GenerateCostEstimation
- Click on the Input and add the following expression by clicking on the Formula tab 
    - Topic.varApp & " " & Topic.varAzureResourceTable.Text.MarkdownContent

- ![alt text](image.png)
- Click on the Properties and under Customize in the Properties pane, insert the generative AI instruction. 
```yaml
        You are an Azure cost estimation expert generating a cost analysis section.

        APPLICATION NAME: {Topic.varApp}

        AZURE RESOURCES IDENTIFIED:
        {Topic.varAzureResourceTable.Text.MarkdownContent}

        Generate ONLY the Cost Estimation section.

        COST ESTIMATION SECTION:
        Use exact heading: ## 💰 Estimated Monthly Costs

        INSTRUCTIONS:
        1. Analyze each Azure resource from the resource table
        2. Provide estimated monthly cost ranges based on the SKU tiers identified
        3. Group costs by category

        CREATE A COST TABLE:
        | Category | Resource | SKU | Est. Monthly Cost (USD) |
        |----------|----------|-----|-------------------------|

        Include these categories:
        - **Compute:** App Services, Functions, Container Apps
        - **Data:** SQL Database, Cosmos DB, Storage Accounts
        - **Networking:** Front Door, Firewall, Private Link, Bandwidth
        - **Security:** Key Vault, WAF, DDoS Protection
        - **Monitoring:** Application Insights, Log Analytics, Sentinel

        AFTER THE TABLE ADD:

        ### 📊 Cost Summary
        - **Estimated Monthly Total:** $X,XXX - $X,XXX
        - **Estimated Annual Total:** $XX,XXX - $XX,XXX

        ### 💡 Cost Optimization Recommendations
        Add 3-4 bullet points with cost-saving recommendations such as:
        - Reserved Instances for predictable workloads
        - Auto-scaling policies to reduce off-peak costs
        - Lifecycle policies for storage
        - Right-sizing based on actual usage

        PRICING GUIDELINES (use these estimates):
        - App Service P2v2: $150-200/month per instance
        - App Service P3v2: $300-400/month per instance
        - SQL Database Business Critical: $400-800/month
        - SQL Database Standard: $150-300/month
        - Event Hubs Standard: $20-50/month per TU
        - Event Hubs Premium: $100-200/month per PU
        - Key Vault Standard: $0.03 per 10,000 operations
        - Application Insights: $2.30 per GB ingested
        - Log Analytics: $2.76 per GB ingested
        - Azure Firewall Standard: $900-1,100/month
        - Azure Firewall Premium: $1,500-1,800/month
        - Front Door Standard: $35/month + $0.01/request
        - Front Door Premium: $330/month + usage
        - Azure Sentinel: $2.46 per GB analyzed
        - Storage Account (Hot): $0.018 per GB/month
        - Data Lake Storage: $0.02 per GB/month

        Add citation [1] at end.
```
- Create a new Variable named varCostEstimate as shown in the image 
![alt text](image-2.png)
-Update Set Variable action to include the newly added Generative AI response. 
![alt text](image-3.png)
- ![alt text](image-4.png)
-Also, update the Message action shown in the image to add Topic.varCostEstimate.Text.MarkdownContent
-Save the Topic. 
-Start a New Test Session in the chat window to test the new feature as shown in the Image. ![alt text](image-5.png)
---

## 📎 Document Input Support

### How Users Provide Intake Documents

Both labs support the **existing intake document flow** in your Topic:

| Mode | Input Method | How It Works |
|------|--------------|--------------|
| **Chat Mode** | 📎 **File Upload** | User uploads Word/PDF via the `FilePrebuiltEntity` question node. A Power Automate Flow extracts the content. |
| **Chat Mode** | ⌨️ **Copy/Paste** | User can paste requirements text directly when prompted |
| **Autonomous Mode** | 🤖 **System.Activity.Text** | Intake content passed programmatically via API |

### Existing Topic Code That Handles This:

```yaml
# File Upload Support (already in your Topic)
- kind: Question
  id: question_CE78PI
  variable: init:Topic.varFile
  prompt: Please upload the intake requirements document
  entity:
    kind: FilePrebuiltEntity
    includeFileMetadata: true

# Flow extracts content from uploaded file
- kind: InvokeFlowAction
  id: invokeFlowAction_QDu2BN
  input:
    binding:
      file: =Topic.varFile
  output:
    binding:
      intakedocumentcontent: Topic.InTakeDocumentContent
```

> **✅ Both labs work with file uploads AND copy/paste** — no changes needed to the intake flow!

---

## 🧪 Sample Test Intake Document

Use this sample for testing. You can either:
- **Copy/paste** when prompted, OR
- **Save as Word document** and upload

```
APPLICATION NAME: Smart Logistics Platform

DESCRIPTION: 
Global shipment tracking and logistics management platform serving enterprise 
customers across North America and Europe. The platform provides real-time 
visibility into shipment status, predictive ETAs, and automated exception handling.

BUSINESS REQUIREMENTS:
- Support 50,000 daily active users across web and mobile channels
- Process 500GB of telemetry data daily from GPS tracking devices
- Real-time shipment tracking with sub-second update latency
- Batch analytics for daily operational reports
- Integration with partner systems for end-to-end visibility

TECHNICAL REQUIREMENTS:
- Primary Region: North America (East US)
- Failover Region: Europe (West Europe)
- Target SLA: 99.9% uptime
- Business Criticality: High

COMPLIANCE AND SECURITY:
- GDPR compliance for European customers
- CCPA compliance for California customers
- Data encryption at rest and in transit
- Zero Trust security model

INTEGRATIONS:
- GeoTrack Inc: GPS telemetry via Kafka streaming
- SAP ERP: Order and inventory data via REST APIs
- Okta: Enterprise SSO and identity federation
- Azure AD B2C: Customer identity management

DATA FLOWS:
- Real-time: WebSocket connections for live tracking updates
- Streaming: Kafka-compatible ingestion for GPS telemetry
- Batch: Nightly ETL for analytics and reporting
- API: REST endpoints for partner integrations

USERS:
- End Users: Customers tracking shipments via web/mobile
- Operations Users: Logistics coordinators managing exceptions
- Admin Users: IT administrators and compliance officers
```

---

# 📘 Lab Option 1: Add Cost Estimation Section

**Difficulty:** Level 300 | **Duration:** 10 minutes

## 🎯 Learning Objectives

By completing this lab, you will:
- Add a new generative AI action to an existing Topic
- Chain outputs between Topic actions
- Modify document assembly logic
- Generate Azure cost estimates based on architecture resources

---

## Step 1: Open the Topic in Copilot Studio (1 min)

1. Navigate to **Copilot Studio** (https://copilotstudio.microsoft.com)
2. Open your **Design Agent**
3. Go to **Topics** → Click on **"Generate Design Document"**
4. Click the **"</>Code Editor"** button to switch to YAML view

![Switch to Code Editor](https://learn.microsoft.com/en-us/microsoft-copilot-studio/media/authoring-create-edit-topics/code-editor-button.png)

---

## Step 2: Locate the Insertion Point (1 min)

Find the `GenerateAzureResourcesTable` action in your YAML. Look for:

```yaml
    - kind: SearchAndSummarizeContent
      id: tX91o2
      displayName: GenerateAzureResourcesTable
      variable: Topic.varAzureResourceTable
```

You will add the new cost estimation action **immediately after** this section and **before** the `ConditionGroup` that handles saving.

---

## Step 3: Add the Cost Estimation Action (4 mins)

**Copy and paste this YAML block** after `GenerateAzureResourcesTable`:

```yaml
    - kind: SearchAndSummarizeContent
      id: CostEst01
      displayName: GenerateCostEstimation
      variable: Topic.varCostEstimate
      userInput: =Topic.varApp & " " & Topic.varAzureResourceTable.Text.MarkdownContent
      additionalInstructions: |-
        You are an Azure cost estimation expert generating a cost analysis section.

        APPLICATION NAME: {Topic.varApp}

        AZURE RESOURCES IDENTIFIED:
        {Topic.varAzureResourceTable.Text.MarkdownContent}

        Generate ONLY the Cost Estimation section.

        COST ESTIMATION SECTION:
        Use exact heading: ## 💰 Estimated Monthly Costs

        INSTRUCTIONS:
        1. Analyze each Azure resource from the resource table
        2. Provide estimated monthly cost ranges based on the SKU tiers identified
        3. Group costs by category

        CREATE A COST TABLE:
        | Category | Resource | SKU | Est. Monthly Cost (USD) |
        |----------|----------|-----|-------------------------|

        Include these categories:
        - **Compute:** App Services, Functions, Container Apps
        - **Data:** SQL Database, Cosmos DB, Storage Accounts
        - **Networking:** Front Door, Firewall, Private Link, Bandwidth
        - **Security:** Key Vault, WAF, DDoS Protection
        - **Monitoring:** Application Insights, Log Analytics, Sentinel

        AFTER THE TABLE ADD:

        ### 📊 Cost Summary
        - **Estimated Monthly Total:** $X,XXX - $X,XXX
        - **Estimated Annual Total:** $XX,XXX - $XX,XXX

        ### 💡 Cost Optimization Recommendations
        Add 3-4 bullet points with cost-saving recommendations such as:
        - Reserved Instances for predictable workloads
        - Auto-scaling policies to reduce off-peak costs
        - Lifecycle policies for storage
        - Right-sizing based on actual usage

        PRICING GUIDELINES (use these estimates):
        - App Service P2v2: $150-200/month per instance
        - App Service P3v2: $300-400/month per instance
        - SQL Database Business Critical: $400-800/month
        - SQL Database Standard: $150-300/month
        - Event Hubs Standard: $20-50/month per TU
        - Event Hubs Premium: $100-200/month per PU
        - Key Vault Standard: $0.03 per 10,000 operations
        - Application Insights: $2.30 per GB ingested
        - Log Analytics: $2.76 per GB ingested
        - Azure Firewall Standard: $900-1,100/month
        - Azure Firewall Premium: $1,500-1,800/month
        - Front Door Standard: $35/month + $0.01/request
        - Front Door Premium: $330/month + usage
        - Azure Sentinel: $2.46 per GB analyzed
        - Storage Account (Hot): $0.018 per GB/month
        - Data Lake Storage: $0.02 per GB/month

        Add citation [1] at end.
      fileSearchDataSource:
        searchFilesMode:
          kind: SearchAllFiles
      knowledgeSources:
        kind: SearchAllKnowledgeSources
      responseCaptureType: FullResponse
```

---

## Step 4: Update the Document Assembly (2 mins)

Find the `setVariable_P3CNQA` action that assembles the final document:

**BEFORE (existing code):**
```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
```

**AFTER (add the cost estimate):**
```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varCostEstimate.Text.MarkdownContent
```

---

## Step 5: Update Display-Only Output (1 min)

Find the `sendActivity_displayOnly` section in the `elseActions` block:

**BEFORE:**
```yaml
        - kind: SendActivity
          id: sendActivity_displayOnly
          activity: |-
            **Target Azure Architecture Document for {Topic.varApp}**

            {Topic.varIntroOverview.Text.MarkdownContent}

            {Topic.varDataFlows.Text.MarkdownContent}

            {Topic.varDetailedViews.Text.MarkdownContent}

            {Topic.varRationale.Text.MarkdownContent}

            {Topic.varAzureResourceTable.Text.MarkdownContent}
```

**AFTER:**
```yaml
        - kind: SendActivity
          id: sendActivity_displayOnly
          activity: |-
            **Target Azure Architecture Document for {Topic.varApp}**

            {Topic.varIntroOverview.Text.MarkdownContent}

            {Topic.varDataFlows.Text.MarkdownContent}

            {Topic.varDetailedViews.Text.MarkdownContent}

            {Topic.varRationale.Text.MarkdownContent}

            {Topic.varAzureResourceTable.Text.MarkdownContent}

            {Topic.varCostEstimate.Text.MarkdownContent}
```

---

## Step 6: Save and Test (1 min)

1. Click **Save** in the Code Editor
2. Open the **Test Panel** (right side)
3. Type: `Generate and save design document`
4. When prompted, enter App Name: `Smart Logistics Platform`
5. When prompted, **upload** the sample intake document (Word file) OR **paste** the sample text
6. Wait for generation to complete
7. **Verify** the output includes the new **💰 Estimated Monthly Costs** section

---

## ✅ Lab 1 Success Criteria

| Checkpoint | Expected Result |
|------------|-----------------|
| Topic saves without errors | ✅ No YAML syntax errors shown |
| Cost section appears in chat output | ✅ Shows cost table with categories |
| Cost summary included | ✅ Monthly and annual totals displayed |
| Optimization recommendations present | ✅ 3-4 bullet points shown |
| SharePoint document includes costs | ✅ New section at end of saved document |

---

## 🔧 Troubleshooting Lab 1

| Issue | Solution |
|-------|----------|
| YAML syntax error on save | Check indentation (use 2 spaces, not tabs) |
| `varCostEstimate` is empty | Ensure the action ID `CostEst01` is unique |
| Costs not appearing in saved doc | Verify `& Topic.varCostEstimate.Text.MarkdownContent` was added |
| Action not executing | Check action is placed after `GenerateAzureResourcesTable` |

---

---

# 📘 Lab Option 2: Add WAF Compliance Checklist

**Difficulty:** Level 350 | **Duration:** 10 minutes

## 🎯 Learning Objectives

By completing this lab, you will:
- Implement Azure Well-Architected Framework validation
- Create automated compliance checklists with status indicators
- Integrate governance checks into document generation
- Provide actionable recommendations based on architecture analysis

---

## Step 1: Open the Topic in Copilot Studio (1 min)

1. Navigate to **Copilot Studio** (https://copilotstudio.microsoft.com)
2. Open your **Design Agent**
3. Go to **Topics** → Click on **"Generate Design Document"**
4. Click **"</>Code Editor"** to switch to YAML view

---

## Step 2: Locate the Insertion Point (1 min)

Find the `GenerateAzureResourcesTable` action. You will add the WAF Checklist action **immediately after** it.

```yaml
    - kind: SearchAndSummarizeContent
      id: tX91o2
      displayName: GenerateAzureResourcesTable
      variable: Topic.varAzureResourceTable
      ...
      responseCaptureType: FullResponse
    
    # <-- INSERT NEW ACTION HERE -->
    
    - kind: ConditionGroup
      id: conditionGroup_MoDYK2
```

---

## Step 3: Add the WAF Checklist Action (5 mins)

**Copy and paste this YAML block** after `GenerateAzureResourcesTable`:

```yaml
    - kind: SearchAndSummarizeContent
      id: WAFCheck01
      displayName: GenerateWAFChecklist
      variable: Topic.varWAFChecklist
      userInput: =Topic.varApp & " " & Topic.varIntakeText & " " & Topic.varAzureResourceTable.Text.MarkdownContent
      additionalInstructions: |-
        You are an Azure Well-Architected Framework (WAF) expert generating a compliance checklist.

        APPLICATION NAME: {Topic.varApp}

        INTAKE DOCUMENT:
        {Topic.varIntakeText}

        AZURE RESOURCES:
        {Topic.varAzureResourceTable.Text.MarkdownContent}

        Generate ONLY the WAF Compliance Checklist section.

        Use exact heading: ## ✅ Well-Architected Framework Compliance Checklist

        ANALYZE the intake document and resource table against each WAF pillar.
        Use these status indicators:
        - ✅ Fully addressed in the design
        - ⚠️ Partially addressed or needs clarification
        - ❌ Not addressed or missing

        CREATE CHECKLIST FOR EACH PILLAR:

        ### 🛡️ Reliability
        Evaluate and list 5 items with status indicators:
        - Multi-region deployment configured
        - Failover strategy defined (active-passive or active-active)
        - RTO and RPO requirements documented
        - Health probes and monitoring configured
        - Backup and disaster recovery plan included

        ### 🔐 Security
        Evaluate and list 5 items with status indicators:
        - Zero Trust architecture principles applied
        - Network segmentation with NSGs and Firewall
        - Data encryption at rest and in transit
        - Identity management with Azure AD or B2C
        - Secrets management using Key Vault
        - Threat detection with Sentinel or Defender

        ### ⚡ Performance Efficiency
        Evaluate and list 5 items with status indicators:
        - Auto-scaling configuration defined
        - Caching strategy for frequently accessed data
        - CDN or Front Door for global user access
        - Database tier appropriate for expected load
        - Async processing for heavy or batch workloads

        ### 💵 Cost Optimization
        Evaluate and list 5 items with status indicators:
        - Right-sized SKUs based on requirements
        - Reserved capacity opportunities identified
        - Auto-shutdown policies for non-production
        - Storage tiering and lifecycle policies
        - Cost monitoring and alerting configured

        ### 🔧 Operational Excellence
        Evaluate and list 5 items with status indicators:
        - Centralized logging with Log Analytics
        - Application performance monitoring with App Insights
        - Alerting rules and dashboards defined
        - Infrastructure as Code for deployments
        - Runbooks for common operational tasks

        AFTER THE CHECKLISTS ADD:

        ### 📊 Compliance Summary Table

        | Pillar | Status | Items Addressed | Score |
        |--------|--------|-----------------|-------|
        | Reliability | ✅/⚠️/❌ | X of 5 | X/5 |
        | Security | ✅/⚠️/❌ | X of 6 | X/6 |
        | Performance | ✅/⚠️/❌ | X of 5 | X/5 |
        | Cost Optimization | ✅/⚠️/❌ | X of 5 | X/5 |
        | Operational Excellence | ✅/⚠️/❌ | X of 5 | X/5 |
        | **Overall WAF Score** | | | **X/26** |

        STATUS DETERMINATION:
        - ✅ if score is 80% or higher
        - ⚠️ if score is 50-79%
        - ❌ if score is below 50%

        ### 🎯 Priority Recommendations

        List the top 3-5 items that need immediate attention before architecture approval.
        Format as numbered list with brief explanation for each.

        Add citation [1] at end.
      fileSearchDataSource:
        searchFilesMode:
          kind: SearchAllFiles
      knowledgeSources:
        kind: SearchAllKnowledgeSources
      responseCaptureType: FullResponse
```

---

## Step 4: Update the Document Assembly (2 mins)

Find the `setVariable_P3CNQA` action:

**BEFORE (existing code):**
```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
```

**AFTER (add WAF checklist):**
```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varWAFChecklist.Text.MarkdownContent
```

---

## Step 5: Update Display-Only Output (1 min)

Find the `sendActivity_displayOnly` section:

**BEFORE:**
```yaml
        - kind: SendActivity
          id: sendActivity_displayOnly
          activity: |-
            **Target Azure Architecture Document for {Topic.varApp}**

            {Topic.varIntroOverview.Text.MarkdownContent}

            {Topic.varDataFlows.Text.MarkdownContent}

            {Topic.varDetailedViews.Text.MarkdownContent}

            {Topic.varRationale.Text.MarkdownContent}

            {Topic.varAzureResourceTable.Text.MarkdownContent}
```

**AFTER:**
```yaml
        - kind: SendActivity
          id: sendActivity_displayOnly
          activity: |-
            **Target Azure Architecture Document for {Topic.varApp}**

            {Topic.varIntroOverview.Text.MarkdownContent}

            {Topic.varDataFlows.Text.MarkdownContent}

            {Topic.varDetailedViews.Text.MarkdownContent}

            {Topic.varRationale.Text.MarkdownContent}

            {Topic.varAzureResourceTable.Text.MarkdownContent}

            {Topic.varWAFChecklist.Text.MarkdownContent}
```

---

## Step 6: Save and Test (1 min)

1. Click **Save** in the Code Editor
2. Open the **Test Panel**
3. Type: `Generate design document`
4. Enter App Name: `Smart Logistics Platform`
5. **Upload** the sample intake Word document OR **paste** the sample text
6. **Verify** the WAF Checklist section appears with:
   - All 5 WAF pillars with status indicators
   - Compliance summary table with scores
   - Priority recommendations list

---

## ✅ Lab 2 Success Criteria

| Checkpoint | Expected Result |
|------------|-----------------|
| Topic saves without errors | ✅ No YAML syntax errors |
| All 5 WAF pillars displayed | ✅ Reliability, Security, Performance, Cost, Operations |
| Status indicators used correctly | ✅ Shows ✅, ⚠️, or ❌ based on analysis |
| Compliance summary table present | ✅ Shows scores per pillar |
| Overall WAF score calculated | ✅ Total score out of 26 shown |
| Priority recommendations listed | ✅ 3-5 actionable items |

---

## 🔧 Troubleshooting Lab 2

| Issue | Solution |
|-------|----------|
| WAF section empty | Ensure `Topic.varIntakeText` has content |
| Missing status indicators | Check the prompt includes status indicator instructions |
| Scores don't add up | This is generative; minor calculation errors are expected |
| Action not in correct position | Must be after `GenerateAzureResourcesTable` |

---

---

# 🏆 Bonus Challenge: Combine Both Labs

**Duration:** 5 additional minutes

If you completed both labs, combine them into a single comprehensive document:

## Update Document Assembly with Both Sections:

```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varCostEstimate.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varWAFChecklist.Text.MarkdownContent
```

## Final Document Structure:

```
📦 [App Name] — Target Azure Architecture Details
├── 🧭 Introduction
├── 🏗️ Architecture Overview
├── 🔄 Data Flows
├── 🧩 Detailed Description of Each View
│   ├── 1) Logical View
│   ├── 2) High-Level Technical View
│   ├── 3) Detailed Infrastructure View
│   ├── 4) Networking and Security View
│   └── 5) Monitoring and Logging View
├── 🧪 Rationales
├── ⚠️ Limitations
├── 📋 Azure Resource Table
├── 💰 Estimated Monthly Costs        ← Lab 1
└── ✅ WAF Compliance Checklist       ← Lab 2
```

---

# 📚 Additional Resources

| Resource | Link |
|----------|------|
| Azure Well-Architected Framework | https://learn.microsoft.com/azure/well-architected/ |
| Azure Pricing Calculator | https://azure.microsoft.com/pricing/calculator/ |
| Copilot Studio Documentation | https://learn.microsoft.com/microsoft-copilot-studio/ |
| Copilot Studio YAML Reference | https://learn.microsoft.com/microsoft-copilot-studio/authoring-create-edit-topics |

---

## 📝 Lab Completion Checklist

| Lab | Status |
|-----|--------|
| Lab 1: Cost Estimation | ⬜ Not Started / ⬜ In Progress / ⬜ Completed |
| Lab 2: WAF Checklist | ⬜ Not Started / ⬜ In Progress / ⬜ Completed |
| Bonus: Combined | ⬜ Not Started / ⬜ In Progress / ⬜ Completed |

**Instructor Sign-off:** _________________ **Date:** _____________

---

===
## Module 8: Understanding the Output

### Step 8.1: Introduction Section

The generated document begins with a formal introduction:

```markdown
# 📦 SmartLogistics — Target Azure Architecture Details

**Prepared for:** [Consultant Name]
**Regions:** primary eastus2, failover westeurope
**Compliance focus:** GDPR and CCPA
**Business criticality:** High mission critical

---

## 🧭 Introduction

SmartLogistics is a cloud-first logistics platform that provides 
real-time shipment tracking, analytics, and deep...
```

### Step 8.2: Data Flows Section

Documents the main data movement patterns:

```markdown
## 🔄 Data Flows

Real-time GPS telemetry is ingested through secure APIs and streaming 
endpoints, normalized, and persisted in a document database optimized 
for operational reads and writes. Operational dashboards and mobile 
clients consume this data via secure APIs with WebSockets for 
low-latency updates. Nightly batch pipelines extract operational 
data to an analytical store for historical analysis and reporting.

Enterprise integration uses private connectivity to ERP and corporate 
services. Secrets and keys are centrally managed, with encryption in 
transit and at rest by default. Observability signals flow to a unified 
logging and SIEM layer to support 24x7 operations and incident response.
```

### Step 8.3: Architecture Views

The agent generates five standardized architecture views:

#### View 1: Logical View — Conceptual

**Purpose:** Non-technical summary showing core actors and systems without binding to specific Azure services.

**Key Elements:**
- Trust boundaries (Cloud Provider Zone, Internet Zone, Corporate Network)
- Actor representations (End Users, GPS Providers, Enterprise Systems)
- Logical component flows
- Communication protocols (HTTPS:443, WebSockets, Kafka:9093)

**Description:**
> This conceptual view illustrates the core actors and systems without binding them to specific Azure services. Internet users access the solution via a web or mobile client, which communicates with a web gateway that enforces security and routes traffic to the API gateway.

#### View 2: High-Level Technical View

**Purpose:** Shows Azure components and their integrations at a technical level.

**Key Elements:**
- Azure service selections
- Integration patterns
- Technology rationale

#### View 3: Detailed Infrastructure View

**Purpose:** Provides infrastructure-level detail for resource isolation and SCF controls.

**Key Elements:**
- Resource boundaries
- SCF control mapping
- Security configurations

#### View 4: Networking View

**Purpose:** Illustrates virtual network connectivity and segmentation.

**Key Elements:**
- Hub-spoke network topology
- Trust boundary implementation
- Network security groups

#### View 5: Observability View

**Purpose:** Presents logging and monitoring strategy.

**Key Elements:**
- Application Insights integration
- Log Analytics workspace
- Azure Sentinel SIEM

### Step 8.4: Rationales Section

Explains design decisions aligned with best practices:

```markdown
## 📝 Rationales

**Security and Compliance:** The design adopts a zero trust posture with 
identity-driven access, Private Link for data plane isolation, and 
centralized egress via Azure Firewall. All traffic is TLS encrypted and 
governed by WAF policies at both the global and regional layers. GDPR and 
CCPA controls are supported through encryption at rest with customer-managed 
keys in Key Vault and Managed HSM, data minimization in analytics, and 
role-based access to sensitive data.

**Scalability and Availability:** Azure Front Door and regionally deployed 
services enable active-active or active-passive failover between eastus2 
and westeurope. Event Hubs partitions and Cosmos DB throughput allocation 
support bursty telemetry. App Service autoscale handles variable traffic, 
while the hub-spoke network isolates fault domains and enables independent 
scaling of app and data planes.

**Operations and Cost:** PaaS services reduce patching and maintenance 
overhead, letting the team focus on features. Centralized monitoring with 
Application Insights and Sentinel improves mean time to detect and remediate. 
API Management policies standardize throttling, caching, and transformation, 
reducing custom code and improving observability.
```

### Step 8.5: Azure Resource Table

The final section provides deployment-ready resource specifications:

```markdown
## 📊 Azure Resource Table — Visual

| Resource Name | Resource Type | SKU | Regions |
|---------------|---------------|-----|---------|
| FrontDoor-Global | Front-Door-Standard-Premium | standard-premium | global |
| DDoS-Plan-Hub | DDoS-Protection-Plan | standard | eastus2-westeurope |
| Hub-VNet | Virtual-Network | n-a | eastus2 |
| AzureFirewall-Hub | Azure-Firewall-Premium | premium | eastus2-westeurope |
| ExpressRoute-Gateway | Virtual-Network-Gateway | er-gateway | eastus2 |
| Bastion-Host | Azure-Bastion | standard | eastus2 |
| AppSpoke-VNet | Virtual-Network | n-a | eastus2-westeurope |
| DataSpoke-VNet | Virtual-Network | n-a | eastus2-westeurope |
```

> 📋 **Note:** The resource table is provided in both Markdown and plain text formats for compatibility with deployment automation tools.

===

## Module 9: Publishing to Channels

Once you have configured and tested the Design Agent, you can publish it to various channels to make it accessible to architects and consultants across your organization.

### Step 9.1: Understanding Channels

Copilot Studio supports publishing to multiple channels:

| Channel | Use Case | Audience |
|---------|----------|----------|
| **Microsoft Teams** | Internal collaboration | Architects, Consultants |
| **SharePoint** | Embedded in project sites | Project teams |
| **Power Apps** | Custom applications | Field consultants |
| **Web (Demo Website)** | External demos | Customer presentations |
| **Azure Bot Service** | Custom integrations | Developers |
| **Microsoft 365 Copilot** | Copilot integration | Enterprise users |

### Step 9.2: Publish the Agent

Before publishing to any channel, you must first publish the agent:

1. In Copilot Studio, open the **Application Design Agent**
2. Click the **Publish** button in the top-right corner
3. Review the publish summary:
   - Topics included
   - Knowledge sources
   - Connections configured
4. Click **Publish**
5. Wait for confirmation: "Your agent is published"

> ⚠️ **Important:** You must republish the agent whenever you make changes to topics, knowledge, or settings.

### Step 9.3: Deploy to Microsoft Teams

Microsoft Teams is the recommended channel for internal use by architects and consultants.

#### 9.3.1 Configure Teams Channel

1. Navigate to **Channels** tab in Copilot Studio
2. Click **Microsoft Teams**
3. Click **Turn on Teams**

#### 9.3.2 Customize Teams App

```
┌─────────────────────────────────────────────────────────────────┐
│  TEAMS APP CONFIGURATION                                         │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  App Name:        Design Agent                                  │
│                                                                  │
│  Short Description:                                             │
│  Generate Azure architecture documents from intake data         │
│                                                                  │
│  Long Description:                                              │
│  The Design Agent uses GPT-5 deep reasoning to transform        │
│  application intake documents into comprehensive Azure          │
│  architecture designs aligned with WAF and SCF.                 │
│                                                                  │
│  App Icon:        [Upload 192x192 PNG]                         │
│  Accent Color:    #0078D4 (Microsoft Blue)                     │
│                                                                  │
│  Developer:       Microsoft Consulting Services                 │
│  Website:         https://microsoft.com/consulting              │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

#### 9.3.3 Set Availability

1. Under **Availability options**, select:
   - ☑️ **Show to my teammates and shared users** (for testing)
   - ☑️ **Show to everyone in my org** (for production)

2. Click **Share**

#### 9.3.4 Admin Approval (If Required)

For organization-wide deployment:

1. Click **Submit for admin approval**
2. Provide business justification
3. Wait for Teams admin approval
4. Once approved, the agent appears in the Teams app store

#### 9.3.5 Using in Teams

Once deployed, users can access the Design Agent:

1. Open **Microsoft Teams**
2. Click **Apps** in the left sidebar
3. Search for "Design Agent"
4. Click **Add** to install
5. Start a conversation with the agent

### Step 8.4: Deploy to SharePoint

Embed the Design Agent in SharePoint sites for easy access from project workspaces.

#### 9.4.1 Get the Embed Code

1. In Copilot Studio, go to **Channels** > **Custom website**
2. Copy the **Embed code**:

```html
<iframe 
  src="https://copilotstudio.microsoft.com/environments/[env]/bots/[botId]/webchat"
  frameborder="0"
  style="width: 100%; height: 600px;">
</iframe>
```

#### 9.4.2 Add to SharePoint Page

1. Navigate to your SharePoint project site
2. Edit the page where you want to embed the agent
3. Add an **Embed** web part
4. Paste the iframe code
5. Adjust dimensions as needed
6. **Publish** the page

### Step 9.5: Deploy as Power Apps Component

Integrate the Design Agent into custom Power Apps for field consultants.

#### 9.5.1 Add Copilot Control

1. Open your Power App in **Power Apps Studio**
2. Insert a **Copilot** control from the Insert menu
3. Configure the control:
   - Select **Application Design Agent** as the source
   - Set dimensions and position

#### 9.5.2 Configure Context Passing

Pass context from your app to the agent:

```powerfx
// Set initial context for the agent
Copilot1.Context = {
    CustomerName: CustomerDropdown.Selected.Name,
    EngagementId: EngagementIdTextBox.Text,
    PreferredRegion: RegionDropdown.Selected.Value
}
```

### Step 9.6: Deploy to Demo Website

Create a standalone demo website for customer presentations.

#### 9.6.1 Configure Demo Website

1. Go to **Channels** > **Demo website**
2. Click **Copy** to get the demo URL:
   ```
   https://copilotstudio.microsoft.com/environments/[env]/bots/[botId]/webchat
   ```

3. Customize appearance:
   - Welcome message
   - Suggested actions
   - Color theme

#### 9.6.2 Share Demo URL

Share the demo URL with customers for presentations:

> 🔗 **Demo URL:** `https://copilotstudio.microsoft.com/environments/.../webchat`

### Step 9.7: Deploy to Microsoft 365 Copilot (Preview)

For organizations with Microsoft 365 Copilot, the Design Agent can be integrated as a plugin.

#### 9.7.1 Enable Copilot Integration

1. Go to **Channels** > **Microsoft 365 Copilot**
2. Click **Enable**
3. Configure plugin settings:
   - Plugin name: "Design Agent"
   - Description: "Generate Azure architectures"
   - Trigger phrases: "design architecture", "generate Azure design"

#### 9.7.2 User Access

Once enabled, users can invoke the Design Agent from Microsoft 365 Copilot:

```
User: @Design Agent generate an Azure architecture for the attached intake document

Copilot: I'll help you generate an Azure architecture. Let me connect you 
         with the Design Agent...
```

### Step 9.8: Channel Management Best Practices

| Practice | Recommendation |
|----------|----------------|
| Version control | Note published version in channel description |
| Access control | Use Azure AD groups to control channel access |
| Monitoring | Enable analytics for each channel |
| Updates | Communicate changes before republishing |
| Testing | Test in dev channel before production deployment |

### Step 9.9: Post-Publishing Checklist

After publishing to channels, verify:

- [ ] Agent responds correctly in each channel
- [ ] File upload works (where supported)
- [ ] Connections function properly
- [ ] Email notifications are sent
- [ ] SharePoint integration works
- [ ] Analytics are being captured

===

## Appendix: Troubleshooting

### Common Issues and Solutions

#### Issue 1: Agent Not Responding

**Symptoms:** Agent shows "typing" indicator but never responds

**Solutions:**
1. Check Power Automate flow status – ensure all flows are **turned on**
2. Verify connection authentication – connections may have expired
3. Check GPT-5 model availability in your region

#### Issue 2: Document Extraction Fails

**Symptoms:** Error when uploading intake document

**Solutions:**
1. Verify file format is supported (PDF, DOCX, TXT)
2. Check file size is under 10MB
3. Ensure SharePoint connection has read permissions

#### Issue 3: Missing Diagrams

**Symptoms:** Architecture views don't include Mermaid diagrams

**Solutions:**
1. Verify the knowledge file is properly loaded
2. Check that the generation prompt includes diagram instructions
3. Regenerate the document

#### Issue 4: Connection Errors

**Symptoms:** "Connection not found" or authentication errors

**Solutions:**
1. Navigate to **Power Platform Admin Center** > **Connections**
2. Delete and recreate failed connections
3. Update connection references in all Power Automate flows
4. Republish the agent

### Analytics and Monitoring

Monitor agent performance in the **Analytics** section:

| Metric | Description | Target |
|--------|-------------|--------|
| Runs | Total conversations | Trending ↑ |
| Successful runs | Percentage of completions | > 85% |
| Average duration | Time to generate document | < 90 sec |

===

## Summary

Congratulations! You have successfully completed the Design Agent lab. You are now able to:

✅ Import and configure the Design Agent solution  
✅ Establish required connections for SharePoint and email  
✅ Use the agent in **Interactive Mode** for conversation-based architecture generation  
✅ Configure **Autonomous Mode** with SharePoint triggers for automated processing  
✅ Understand automatic document extraction and email notifications  
✅ Generate comprehensive Azure architecture documents  
✅ Understand the five standardized architecture views  
✅ Interpret and use the Azure Resource Configuration tables  
✅ **Publish the agent** to Microsoft Teams, SharePoint, Power Apps, and other channels  

### Next Steps

1. **Practice** generating architectures with different intake documents
2. **Configure** autonomous mode for your team's SharePoint environment
3. **Deploy** the agent to Microsoft Teams for your consulting team
4. **Customize** the agent prompts for specific customer scenarios
5. **Integrate** with your deployment automation pipelines
6. **Share** the generated documents with project stakeholders

===

## Additional Resources

| Resource | Link |
|----------|------|
| Copilot Studio Documentation | [https://learn.microsoft.com/copilot-studio](https://learn.microsoft.com/copilot-studio) |
| Azure Well-Architected Framework | [https://learn.microsoft.com/azure/well-architected](https://learn.microsoft.com/azure/well-architected) |
| Power Automate Documentation | [https://learn.microsoft.com/power-automate](https://learn.microsoft.com/power-automate) |

===

**Document Version:** 1.0  
**Author:** Microsoft Consulting Services  
**Feedback:** Submit issues via your engagement manager

---

*© 2026 Microsoft Corporation. All rights reserved.*
