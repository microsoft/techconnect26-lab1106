# Module 2: Connection Configuration (11 minutes)

After importing the solution, you must establish connections for the agent to function correctly.

## Step 2.1: Identify Required Connections

### Step 2.1.1 Intake Agent Connections

1. Click on **App Intake Agent v1.3.4** from the list of **My Agents**

   click **Settings**

![Imported](1.4.1_00-Intake-Agent-Settings.png)

2. Click on **Connection Settings** on the left menu, select one of the two connections and click **Connect** 

![IntakeAgentConnections](1.4.1_01-Intake-Agent-Connections.png)

3. Click **Submit**

![Submit](1.4.1_02-Intake-Agent-Submit.png)

4. Close (Do the same steps with the other connection)

### Step 2.1.2 Design Agent Connections
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

#### Step 2.1.2.1: Configure SharePoint Connection (1 minute)

1. Locate the **Save Design Document** connection reference
2. Click **Connect**

![SharePointConnection](2.1.2.1_00-Design-Agent-SharePoint-Connection.png)

3. Confirm is signed with the credentials that have access to your target SharePoint site, click **Submit**

![SharePointConnection](2.1.2.1_01-Design-Agent-SharePoint-Connection.png)

#### Step 2.1.2.2: Configure Email Connection (1 minute)

1. Locate the **Office 365 Outlook** connection reference
2. Click **Connect**

![OutlookConnection](2.1.2.1_02-Design-Agent-Outlook-Connection.png)

3. Confirm is signed with the credentials that have access to your target SharePoint site, click **Submit**

![outlookConnection](2.1.2.1_03-Design-Agent-Outlook-Connection.png)

#### Step 2.1.2.2: Configure MCP Connection (1 minute)

1. Locate the **Microsoft LearnDocs MCP** connection reference
2. Click **Connect**

![MCP](2.1.2.1_04-Design-Agent-MCP-Connection.png)

3. Confirm is signed with the credentials that have access to your target SharePoint site, click **Submit**

![MCP](2.1.2.1_05-Design-Agent-MCP-Connection.png)

#### Step 2.1.2.3: Verify All Connections (''20)

2. Verify all connections show **Connected** status:

| Connection | Status |
|------------|--------|
| Office 365 Outlook | ✅ Connected |
| Microsoft Learn Docs MCP | ✅ Connected |
| Save Design Document | ✅ Connected |

Then Close **Settings** window

![Connections](2.1.2.3-Connections.png)

## Step 2.2: Review Flow Connections

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