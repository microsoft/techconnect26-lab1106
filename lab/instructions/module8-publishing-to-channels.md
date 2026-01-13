# Module 8: Publishing to Channels

Once you have configured and tested the Design Agent, you can publish it to various channels to make it accessible to architects and consultants across your organization.

## Step 8.1: Understanding Channels

Copilot Studio supports publishing to multiple channels:

| Channel | Use Case | Audience |
|---------|----------|----------|
| **Microsoft Teams** | Internal collaboration | Architects, Consultants |
| **SharePoint** | Embedded in project sites | Project teams |
| **Power Apps** | Custom applications | Field consultants |
| **Web (Demo Website)** | External demos | Customer presentations |
| **Azure Bot Service** | Custom integrations | Developers |
| **Microsoft 365 Copilot** | Copilot integration | Enterprise users |

## Step 8.2: Publish the Agent

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

## Step 8.3: Deploy to Microsoft Teams

Microsoft Teams is the recommended channel for internal use by architects and consultants.

### 8.3.1 Configure Teams Channel

1. Navigate to **Channels** tab in Copilot Studio
2. Click **Microsoft Teams**
3. Click **Turn on Teams**

### 8.3.2 Customize Teams App

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

### 8.3.3 Set Availability

1. Under **Availability options**, select:
   - ☑️ **Show to my teammates and shared users** (for testing)
   - ☑️ **Show to everyone in my org** (for production)

2. Click **Share**

### 8.3.4 Admin Approval (If Required)

For organization-wide deployment:

1. Click **Submit for admin approval**
2. Provide business justification
3. Wait for Teams admin approval
4. Once approved, the agent appears in the Teams app store

### 8.3.5 Using in Teams

Once deployed, users can access the Design Agent:

1. Open **Microsoft Teams**
2. Click **Apps** in the left sidebar
3. Search for "Design Agent"
4. Click **Add** to install
5. Start a conversation with the agent

## Step 8.4: Deploy to SharePoint

Embed the Design Agent in SharePoint sites for easy access from project workspaces.

### 8.4.1 Get the Embed Code

1. In Copilot Studio, go to **Channels** > **Custom website**
2. Copy the **Embed code**:

```html
<iframe 
  src="https://copilotstudio.microsoft.com/environments/[env]/bots/[botId]/webchat"
  frameborder="0"
  style="width: 100%; height: 600px;">
</iframe>
```

### 8.4.2 Add to SharePoint Page

1. Navigate to your SharePoint project site
2. Edit the page where you want to embed the agent
3. Add an **Embed** web part
4. Paste the iframe code
5. Adjust dimensions as needed
6. **Publish** the page

## Step 8.5: Deploy as Power Apps Component

Integrate the Design Agent into custom Power Apps for field consultants.

### 8.5.1 Add Copilot Control

1. Open your Power App in **Power Apps Studio**
2. Insert a **Copilot** control from the Insert menu
3. Configure the control:
   - Select **Application Design Agent** as the source
   - Set dimensions and position

### 8.5.2 Configure Context Passing

Pass context from your app to the agent:

```powerfx
// Set initial context for the agent
Copilot1.Context = {
    CustomerName: CustomerDropdown.Selected.Name,
    EngagementId: EngagementIdTextBox.Text,
    PreferredRegion: RegionDropdown.Selected.Value
}
```

## Step 8.6: Deploy to Demo Website

Create a standalone demo website for customer presentations.

### 8.6.1 Configure Demo Website

1. Go to **Channels** > **Demo website**
2. Click **Copy** to get the demo URL:
   ```
   https://copilotstudio.microsoft.com/environments/[env]/bots/[botId]/webchat
   ```

3. Customize appearance:
   - Welcome message
   - Suggested actions
   - Color theme

### 8.6.2 Share Demo URL

Share the demo URL with customers for presentations:

> 🔗 **Demo URL:** `https://copilotstudio.microsoft.com/environments/.../webchat`

## Step 8.7: Deploy to Microsoft 365 Copilot (Preview)

For organizations with Microsoft 365 Copilot, the Design Agent can be integrated as a plugin.

### 8.7.1 Enable Copilot Integration

1. Go to **Channels** > **Microsoft 365 Copilot**
2. Click **Enable**
3. Configure plugin settings:
   - Plugin name: "Design Agent"
   - Description: "Generate Azure architectures"
   - Trigger phrases: "design architecture", "generate Azure design"

### 8.7.2 User Access

Once enabled, users can invoke the Design Agent from Microsoft 365 Copilot:

```
User: @Design Agent generate an Azure architecture for the attached intake document

Copilot: I'll help you generate an Azure architecture. Let me connect you 
         with the Design Agent...
```

## Step 8.8: Channel Management Best Practices

| Practice | Recommendation |
|----------|----------------|
| Version control | Note published version in channel description |
| Access control | Use Azure AD groups to control channel access |
| Monitoring | Enable analytics for each channel |
| Updates | Communicate changes before republishing |
| Testing | Test in dev channel before production deployment |

## Step 8.9: Post-Publishing Checklist

After publishing to channels, verify:

- [ ] Agent responds correctly in each channel
- [ ] File upload works (where supported)
- [ ] Connections function properly
- [ ] Email notifications are sent
- [ ] SharePoint integration works
- [ ] Analytics are being captured