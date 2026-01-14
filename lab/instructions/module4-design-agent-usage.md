# Module 4: Testing the Agents (25 minutes)

## 4.1 Intake Agent

1. Select the App Intake Agent v1.3.4 from the list of Agents

![TestingIntakeAgent](4.1_00-TestIntakeAgent.png)

2. Start with:

`"Here is the architectural document for 'SmartLogistics'. Please review it and only ask what's missing."`

Before send the prompt attached the App Overview - Smartlogistic.pdf file

![TestingIntakeAgent](4.1_01-TestIntakeAgent.png)

Other prompts:

`"Begin intake. I have an architecture document to upload."`

`"Create a migration intake report for 'CRM Gateway' and email it to the migration team when done."`

### Conversation Flow & Behavior

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

### Data Points Captured & Report Structure

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

## 4.2 Design Agent (Interactive Mode)

The Design Agent supports two operational modes: **Interactive Mode** (covered in this module) and **Autonomous Mode** (covered in Module 5). This module focuses on the interactive conversation-based approach.

### Step 4.1: Test the Agent

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

## Step 4.3: Generate Architecture Document

## Step 4.4: Review Generated Output

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
