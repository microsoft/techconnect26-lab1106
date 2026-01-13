# Prerequisites (10 minutes)

The following excercise is required to setup the lab environment for use with the AI Migrate 

## Required Access

- [ ] Microsoft 365 account with Copilot Studio license
- [ ] Power Platform environment with Dataverse
- [ ] SharePoint site for document storage
- [ ] Power Automate premium connectors access
- [ ] GPT-5 Reasoning (Preview) model access in Copilot Studio

## Required Files

- [ ] Design Agent solution package (`.zip` file)
- [ ] Azure Resource Table Sample.txt (Knowledge file)
- [ ] Sample intake document (PDF or Word format)

## Environment Setup Checklist

| Component | Status |
| ----------- | -------- |
| Copilot Studio access | ⬜ Verified |
| Power Platform environment | ⬜ Created |
| SharePoint document library | ⬜ Configured |
| Email connector | ⬜ Available |

### Step 1: SharePoint Site Configuration

1. Open the Edge browser, click on waffle icon first, then click on Microosft 365 and click Sign in in the top right:

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
📁 Design Agent Documents
├── 📁 Intake                    ← Upload intake documents here
│   └── 📄 [AppName]-Intake.pdf
├── 📁 Generated Architectures   ← Output documents stored here
│   └── 📄 [AppName]-Target-Azure-Architecture-v1.0.md
└── 📁 Archive                   ← Processed intake documents moved here
```

On the left menu click on **Document**, click on **+ Create or upload**, click on **Folder**. Type Name of the folder
   
![Folders](0.2_10-Create-Folders.png)

12. Configure SharePoint Site Settings

   1. Navigate to your SharePoint site
   2. Go to **Site Settings** > **Site Contents**
   3. Open the **Design Agent Documents** library
   4. Click **⚙️ Settings** > **Library settings**
   5. Under **Columns**, ensure the following metadata columns exist:

   | Column Name | Type | Purpose |
   |-------------|------|--------|
   | Application Name | Single line of text | Stores extracted app name |
   | Processing Status | Choice | Pending, Processing, Completed, Failed |
   | Processed Date | Date and Time | Timestamp of processing |
   | Generated Document | Hyperlink | Link to output document |
