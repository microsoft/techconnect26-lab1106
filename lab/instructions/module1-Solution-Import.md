# Module 1: Solution Import (10 minutes)

In this module we'll access to Copilot Studio to Import the Solutions, then we'll review the Settings of the imported

## Step 1: Access Copilot Studio and Import Solutions

1. Open New Tab in the Edge browser
2. Navigate to +++https://copilotstudio.microsoft.com+++
3. Choose United States from the list of country/region
4. Don't Mark **I will receive information, tips, and offers about Microsoft Copilot Studio** checkbox
5. Click **Get Started**

   ![CopilotStudio](1.1_5-CopilotStudio.png)

6. Skip the Welcome window
7. Click on three dots on the top right
8. Click **X Cancel agent creation**
9. Click **Yes, continue**

   ![Continue](1.1_9-Continue.png)

Now we start the process to import the Solution packages.
Let's start with the **IntakeAgent_1_0_0_7** package

10. On the left ribbon click on the three dots if don't see the **Solutions**
11.  Click on **Solutions** (New tab is open in the Edge browser)

      ![SolutionsIcon](1.1_11-SolutionsIcon.png)

12.  Click **Import Solution** from the command bar
13.  Click **Browse** to select the solution package to import
14.  Select the zip file **IntakeAgent_1_0_0_7.zip** solution package
15. Click **Open**

       ![OpenSolutionPackage](1.1_15-OpenSolutionPackage.png)

16. Click **Next**
17. Click **Next**
18. When green checks are in all services then click **Import**

     ![Import](1.1_18-Import.png)

Let's continue importing the **DesignAgent_1_0_0_11** package
*Execute the prior steps 12 and 13 again* and come back to step 19

19. Select the zip file **DesignAgent_1_0_0_11.zip** solution package
20. Click **Open**

     ![OpenSolutionPackage](1.1_19-OpenSolutionPackage.png)

21. Click **Next**
22. Click **Next**
23. When green checks are in all services then click **Import**

     ![OpenSolutionPackage](1.1_23-OpenSolutionPackage.png)

Wait for the packages to be imported. Once imported you will see the status change to **Solution "Intake-Agent" imported successfully with warnings**. Same for the Application-Design-Agent package. It's Ok

 ![Warning](1.1_23-Warning.png)

## Step 2: Update Imported Agents

In this step we are going to update some configuration in the Agents included in the imported packages.
Let's start with the **Intake-Agent**

### Step 2.1: Update Intake Agent Tools

1. In the Solution window from the prior Step 1.1, click on **Intake-Agent**

   ![IntakeAgent](1.2.1._1-IntakeAgent.png)

2. On the left menu, click **Agents (2)**
3. Validate there are 2 agents (App Intake Agent v1.3.4 and Azure Architecture Expert v0.6.1) and Click on **App Intake Agent v1.3.4**

   ![ValidateAgent](1.2.1_3-ValidateAgents.png)

4. Click on **Tools** on the top ribbon
5. Click on **Send an Email (V2)** connector Name

   ![Outlook](1.2.1_5-Outlook.png)

6. Click on **Inputs** on the left ribbon
7. Replace the **Value** field content in the Input **To** by your username provided for this Lab **Username: +++@lab.CloudPortalCredential(User1).Username+++**
8. **Save**

   ![SaveOutlook](1.2.1_8-SaveOutlook.png)

Let's continue with the Application Design Agent. Don't need to close this window

### Step 2.2: Configure Design Agent Settings

1. Hover over the Agent icon on the left ribbon to show the list of the Agents and click on **Application Design Agent**
2. Verify the agent overview displays correctly in the Test Agent window:
**Expected Overview Screen:**

   ![ApplicationDesignAgent](1.2.2_2-ApplicationDesignAgent.png)

3. In the Overview tab on the top, scroll down to Knowledge and verify **Web Search** is Disable

   ![WebSearch](1.2.2_3-WebSearch.png)

Congratulations! All Solutions are imported.
You can keep open the Edge browser and move to Module 2 - Connection configurataion