# Module 5: Autonomous Agent Mode

The Design Agent can operate as a fully autonomous agent, automatically processing intake documents without user intervention. This mode is ideal for high-volume environments or when architects want to batch-process multiple application assessments.

## Step 5.1: Understanding Autonomous Mode

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

## Step 5.2: Configure SharePoint Intake Folder

### 5.2.1 Access Triggers Configuration

1. In Copilot Studio, open the **Application Design Agent**
2. In the agent overview, locate the **Triggers** section
3. Click **+ Add trigger**

![SharepointTrigger](5.2_00-SharepointTrigger.png)

### 5.2.2 Set Up SharePoint File Upload Trigger

1. Select **When an item is created** and click **Next**

![SharepointTrigger](5.2_01-SharepointTrigger.png)

2. Review the green checks in the apps and Click **Next**

![SharepointTrigger](5.2_02-SharepointTrigger.png)

2. Configure the trigger settings:

![SharepointTrigger](5.2_03-SharepointTrigger.png)

Trigger Configuration

| Type | Value |
| ---- | ----- |
| Trigger Type | When a file is created in SharePoint |
| Site Address | https://lodsprodmca.sharepoint.com/sites/usercreatedsite |
| Library Name | Documents |
| Folder Path | /Intake-Documents |
| File Filter | *.pdf, *.docx, *.txt |

3. Click **Save**

## Step 5.4: Automatic Data Extraction

When triggered autonomously, the agent extracts information without user intervention:

### 5.4.1 Application Name Extraction

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

### 5.4.2 Intake Content Extraction

The Power Automate flow **ExtractDocumentText** automatically:

1. Retrieves the file from SharePoint
2. Extracts text content using AI Builder or document parsing
3. Passes the content to the Design Agent for processing

## Step 5.5: Automatic Document Generation and Storage

### 5.5.1 Generation Process

Once triggered, the agent:

1. Processes the intake document through all generation nodes
2. Creates the complete architecture document with all five views
3. Generates the Azure Resource Configuration table

### 5.5.2 Output Storage

The generated document is automatically saved to SharePoint:

```
Output Location: /Documents/Architectures-Documents/
File Name:       [AppName]-Target-Azure-Architecture-v1.0.md
Format:          Markdown with embedded Mermaid diagrams
```

**Metadata Updated:**
- Processing Status → "Completed"
- Processed Date → Current timestamp
- Generated Document → Link to output file

## Step 5.7: Testing Autonomous Mode

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

## Step 5.8: Autonomous Mode Best Practices

| Best Practice | Recommendation |
|---------------|----------------|
| File naming | Use consistent `[AppName]-Intake` pattern |
| Document format | PDF works best for text extraction |
| Batch processing | Upload multiple files; they process sequentially |
| Error handling | Monitor the Archive folder for failed documents |
| Notifications | Configure team distribution list for visibility |
