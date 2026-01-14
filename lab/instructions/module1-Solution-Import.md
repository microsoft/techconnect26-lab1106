# Module 1: Solution Import (10 minutes)

## Step 1.1: Access Copilot Studio

## Module 1: Solution Import (10 minutes)

In this module we'll import the solutions to present in this Lab
   - **Intake Agent**
   - **Design Agent**

We'll access to Copilot Studio to Import the Solutions, then we'll review the Settings of the imported

### Step 1.1: Access Copilot Studio and Import Solutions

1. Open New Tab in the Edge browser
2. Navigate to +++https://copilotstudio.microsoft.com+++
3. Choose United States from the list of country/region
4. Don't Mark "I will receive information, tips, and offers about Microsoft Copilot Studio" checkbox
5. Click **Get Started**
6. Skip the Welcome window
7. Click on three dots on the top right
8. Click **X Cancel agent creation**
9. Click **Yes, continue**

Now we start the process to import the Solution packages
Let's start with the AIMigrateIntakeAgent package

10. On the left ribbon click on the three dots if don't see the **Solutions** icon
11. Click on **Solutions** (New tab is open in the Edge browser)
12. Click **Import Solution** from the command bar
13. Click **Browse** to select the solution to import
14. Select the zip file AIMigrateIntakeAgent_1_0_0_7.zip solution package
15. Click **Open**
16. Click **Next**
17. Click **Next**
18. When green checks are in all services then click **Import**

Let's continue importing the AIMigrateDesignAgent_1_0_0_11 package
Execute the above steps 10 to 13

19. Select the zip file AIMigrateDesignAgent_1_0_0_11.zip solution package 
20. Click **Open**
21. Click **Next**
22. Click **Next**
23. When green checks are in all services then click **Import**

This dialog when import the solution packages confirms the solution package is imported successfully with warnings

### Step 1.2: Update Imported Agents

In this step we are going to update some configuration in the Agents.
Let's start with the AI-Migrate_Intake_Agent

#### Step 1.2.1: Update Intake Agent Tools

1. In the Solution window from the prior Step 1.1, click on **AI-Migrate-Intake-Agent**
2. On the left menu, click **Agents (2)**
3. Validate there are 2 agents (App Intake Agent v1.3.4 and Azure Architecture Exper v0.6.1) and click on **App Intake Agent v1.3.4**
4. Click on **Tools** on the top ribbon
5. Click on **Sen and Email** connector Name

![Outlook](1.4.1_02-Intake-Agent-Outlook.png)

6. Click on **Inputs** on the left ribbon
7. Scroll down to **Inputs**
8. Replace the **Value** field content in the Input **To** by your username provided for this Lab **Username: +++@lab.CloudPortalCredential(User1).Username+++**
9. **Save**

![Outlook](1.4.1_03-Intake-Agent-Outlook.png)

Let's continues with the App Intake AGent v1.3.4 Agent. Don't need to close this window

#### Step 1.2.2: Configure Design Agent Settings

1. Keep the coursor on the Agent icon on the left ribbon to show the list of the Agents and click on **Application Design Agent**
![DesignAgent](1.4.2_00-Design-Agent.png)
2. Verify the agent overview displays correctly in the Test Agent window:
**Expected Overview Screen:**
![Welcome](008-Welcome-message.png)