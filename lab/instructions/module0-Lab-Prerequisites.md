# Prerequisites (10 minutes)

## Environment Setup Checklist

| Component | Status |
| ----------- | -------- |
| Copilot Studio access | ⬜ Verified |
| Power Platform environment | ⬜ Created |
| SharePoint document library | ⬜ Configured |
| Email connector | ⬜ Available |

### Step 1: SharePoint Site Configuration
1. Open the Edge browser
2. Click on waffle icon first, then click on Microosft 365 and click Sign in in the top right:

![Browser](0.1_00-Sign-in-Office365.png)

![Office365](0.1_02-Sign-in-Office365.png)

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

8. Click on **Create site**
9. Keep the **Add members** box blank and click on **Finish**
10. Create the Folder Structure
 ```
📁 Documents
├── 📁 Intake-Documents
│   └── 📄 [AppName]-Intake.pdf
├── 📁 Architecture-Documents
│   └── 📄 [AppName]-Target-Azure-Architecture-v1.0.md
```

On the left menu click on **Document**, click on **+ Create or upload**, click on **Folder**. Type Name of the folder (+++Intake-Documents+++ or +++Architecture-Documents+++)
   
![Folders](0.2_10-Create-Folders.png)
