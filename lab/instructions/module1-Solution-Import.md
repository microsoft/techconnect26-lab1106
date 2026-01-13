# Module 1: Solution Import (10 minutes)

Module 1 will show you how to import the AI Migrate Intake and Design agents into the Copilot Studio environment

## Step 1.1: Access Copilot Studio

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

## Step 1.2: Navigate to Solutions

1. Click on **Create** on the top right 

![Refresh](1.2_00-Navigate-to-Solutions.png)

2. In the left navigation pane, click on **Solutions**
> [!TIP]
> If Solutions is not visible, click **More** (•••) to expand the menu

## Step 1.3: Import the Solution

![Refresh](1.3_00-Import-solutions.png)


### Step 1.3.1: Import Intake agent

1. Click **Import solution** from the command bar
2. Click **Browse** select the Design Agent solution package (`AIMigrateIntakeAgent_1_0_0_7.zip` file)

![Browse](1.3.1_00-Import-Intake-Agent-Solution.png)

3. Click **Open**
4. Click **Next**
5. Click **Next**
6. When green check is in all services then click **Import**

![Import](1.3.1_01-Import-Intake-Agent-Solution.png)

### Step 1.3.2: Import Design agent

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

## Step 1.4: Configure Import Settings

### Step 1.4.1: Configure Intake Agent Settings

1. Select the Intake Agent: click on **Copilot Studio icon**

![IntakeAgentSettings](1.4.1_00-Intake-Agent-Settings.png)

2. On the left menu click on Agents
3. Click on **Tools** on the top ribbon

![Outlook](1.4.1_02-Intake-Agent-Outlook.png)

4. Scroll down to **Inputs** and in Input Name **To**, **Value field** replace it by **Username: +++@lab.CloudPortalCredential(User1).Username+++**

5. **Save**

![Outlook](1.4.1_03-Intake-Agent-Outlook.png)

### Step 1.4.2: Configure Design Agent Settings

1. Once imported, locate **Application Design Agent** in your Agents list
2. Click on the Agent name
3. Verify the agent overview displays correctly:

![DesignAgent](1.4.2_00-Design-Agent.png)

**Expected Overview Screen:**

![Welcome](008-Welcome-message.png)
