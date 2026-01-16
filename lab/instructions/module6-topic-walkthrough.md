# Module 6: Topic Walkthrough – Generate and Save Azure Architecture Doc (3 minutes)

This module provides a detailed walkthrough of the main topic flow that powers the Design Agent.

## Step 6.1: Access the Topic

1. In Copilot Studio, open the **Application Design Agent**
2. Click the **Topics** tab in the top navigation
3. Locate and click on **"Generate and save Azure architecture doc"**

## Step 6.2: Understanding the Topic Flow

The topic consists of several key components arranged in a logical flow:

```
┌─────────────────────────────────────────────────────────────────┐
│                        TOPIC FLOW DIAGRAM                       │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────┐                                                    │
│  │ Trigger │ ← "The agent chooses"                              │
│  └────┬────┘   Generates a target Azure architecture design...  │
│       │                                                         │
│       ▼                                                         │
│  ┌────────────────────┐                                         │
│  │ Set variable value │ ← Initialize variablesText = ""         │
│  └────────┬───────────┘                                         │
│           │                                                     │
│       ┌───┴───┐                                                 │
│       ▼       ▼                                                 │
│  ┌─────────┐  ┌──────────────────┐                              │
│  │Condition│  │All other conditions│                            │
│  │varApp   │  │                    │                            │
│  │is Blank │  │Set variablesText = │                            │
│  └────┬────┘  │"ActivityText"      │                            │
│       │       └────────────────────┘                            │
│       ▼                                                         │
│  ┌──────────┐                                                   │
│  │ Question │ ← "Enter the App Name"                            │
│  │ Identity:│   Save response as: var1 (string)                 │
│  │ User's   │                                                   │
│  │ entire   │                                                   │
│  │ response │                                                   │
│  └────┬─────┘                                                   │
│       │                                                         │
│       ▼                                                         │
│  ┌────────────────────┐                                         │
│  │ Set variable value │ ← varApp = var1                         │
│  └────────┬───────────┘                                         │
│           │                                                     │
│           ▼                                                     │
│  ┌──────────┐                                                   │
│  │ Question │ ← "Please upload the intake requirements..."      │
│  │ Identity:│   Save response as: varFile (record)              │
│  │ File     │                                                   │
│  └────┬─────┘                                                   │
│       │                                                         │
│       ▼                                                         │
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
│           │                                                     │
│           ▼                                                     │
│  ┌────────────────────┐                                         │
│  │ Set variable value │ ← variablesText = intakeDocumentC...    │
│  └────────┬───────────┘                                         │
│           │                                                     │
└───────────┼─────────────────────────────────────────────────────┘
            │
            ▼
        [Continued in Step 5.3]
```

## Step 6.3: Generation Nodes

After document extraction, the flow continues with a series of generation nodes:

```
┌─────────────────────────────────────────────────────────────────┐
│                    GENERATION NODES                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌───────────────────────────┐                                  │
│  │🤖GenerateIntroAndOverview│                                   │
│  │   Input: varApp (string)  │                                  │
│  │   Data source: Text       │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                 │
│               ▼                                                 │
│  ┌───────────────────────────┐                                  │
│  │ 🤖 GenerateDataFlows      │                                  │
│  │   Input: varApp (string)  │                                  │
│  │   Data source: Text       │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                 │
│               ▼                                                 │
│  ┌───────────────────────────┐                                  │
│  │ 🤖 GenerateDetailedViews  │                                  │
│  │   Input: varApp (string)  │                                  │
│  │   Data source: Text       │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                 │
│               ▼                                                 │
│  ┌───────────────────────────┐                                  │
│  │ 🤖 GenerateRationale      │                                  │
│  │   Input: varApp (string)  │                                  │
│  │   Data source: Text       │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                 │
│               ▼                                                 │
│  ┌───────────────────────────┐                                  │
│  │ 🤖 GenerateAzureResourceTable│                               │
│  │   Input: varApp (string)   │                                 │
│  │   Data source: Text        │                                 │
│  └────────────┬──────────────┘                                  │
│               │                                                 │
│               ▼                                                 │
│  ┌───────────────────────────┐                                  │
│  │ Set variable value        │                                  │
│  │   varArchitectureDoc =    │                                  │
│  │   [Combined outputs]      │                                  │
│  └────────────┬──────────────┘                                  │
│               │                                                 │
│               ▼                                                 │
│         [Save/Send Flow]                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Step 6.4: Key Topic Components Explained

### 6.4.1 Trigger Node

- **Type:** Agent-initiated trigger
- **Description:** "Generates a target Azure architecture design document for a given application"
- **Activation:** The agent chooses when to invoke this topic based on user intent

### 6.4.2 Variable Initialization

```
Set variable: variablesText
To value: ""
```
Initializes the text variable that will hold the intake document content.

### 6.4.3 Condition Node

Checks if the application name (`varApp`) is already provided:
- **If Blank:** Prompts user for the application name
- **All Other Conditions:** Proceeds with existing value

### 6.4.4 Question Nodes

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

### 6.4.5 ExtractDocumentText Action

This Power Automate flow:
- **Input:** `varFile` (the uploaded document)
- **Process:** Extracts text content from PDF/DOCX
- **Outputs:**
  - `intakeDocumentName` (string) – File name
  - `intakeDocumentContent` (string) – Extracted text

### 6.4.6 Generation Prompts

Each generation node uses the GPT-5 Reasoning model with specific prompts:

| Node | Purpose | Output |
|------|---------|--------|
| GenerateIntroAndOverview | Creates introduction and architecture overview | Markdown content |
| GenerateDataFlows | Documents data movement patterns | Markdown content |
| GenerateDetailedViews | Produces the five architecture views with Mermaid diagrams | Markdown + Mermaid |
| GenerateRationale | Explains design decisions | Markdown content |
| GenerateAzureResourceTable | Creates resource configuration table | Markdown table + plain text |

## Step 6.5: Modifying the Topic

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
