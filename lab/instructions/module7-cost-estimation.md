# Module 7:  Design Agent adding Cost Estimation Topic

## 📘 Lab Option 1: Add Cost Estimation Section

**Difficulty:** Level 300 | **Duration:** 10 minutes

🎯 Learning Objectives

- Add a new generative AI action to an existing Topic to include Azure Resources Cost Estimation
- Chain outputs between Topic actions
- Modify document assembly logic

Step 1: Open the Topic in Copilot Studio (1 min)

- Navigate to Copilot Studio → Topics
- Open the "Generate and save Azure architecture doc" Topic
- Scroll down to the GenerateAzureResourcesTable Action 
- Click + to add a new Action, select Advanced -> Generative Answers ![alt text](image-1.png)
- Name the Action as GenerateCostEstimation
- Click on the Input and add the following expression by clicking on the Formula tab 
  - Topic.varApp & " " & Topic.varAzureResourceTable.Text.MarkdownContent

- ![alt text](image.png)
- Click on the Properties and under Customize in the Properties pane, insert the generative AI instruction. 

```yaml
        You are an Azure cost estimation expert generating a cost analysis section.

        APPLICATION NAME: {Topic.varApp}

        AZURE RESOURCES IDENTIFIED:
        {Topic.varAzureResourceTable.Text.MarkdownContent}

        Generate ONLY the Cost Estimation section.

        COST ESTIMATION SECTION:
        Use exact heading: ## 💰 Estimated Monthly Costs

        INSTRUCTIONS:
        1. Analyze each Azure resource from the resource table
        2. Provide estimated monthly cost ranges based on the SKU tiers identified
        3. Group costs by category

        CREATE A COST TABLE:
        | Category | Resource | SKU | Est. Monthly Cost (USD) |
        |----------|----------|-----|-------------------------|

        Include these categories:
        - **Compute:** App Services, Functions, Container Apps
        - **Data:** SQL Database, Cosmos DB, Storage Accounts
        - **Networking:** Front Door, Firewall, Private Link, Bandwidth
        - **Security:** Key Vault, WAF, DDoS Protection
        - **Monitoring:** Application Insights, Log Analytics, Sentinel

        AFTER THE TABLE ADD:

        ### 📊 Cost Summary
        - **Estimated Monthly Total:** $X,XXX - $X,XXX
        - **Estimated Annual Total:** $XX,XXX - $XX,XXX

        ### 💡 Cost Optimization Recommendations
        Add 3-4 bullet points with cost-saving recommendations such as:
        - Reserved Instances for predictable workloads
        - Auto-scaling policies to reduce off-peak costs
        - Lifecycle policies for storage
        - Right-sizing based on actual usage

        PRICING GUIDELINES (use these estimates):
        - App Service P2v2: $150-200/month per instance
        - App Service P3v2: $300-400/month per instance
        - SQL Database Business Critical: $400-800/month
        - SQL Database Standard: $150-300/month
        - Event Hubs Standard: $20-50/month per TU
        - Event Hubs Premium: $100-200/month per PU
        - Key Vault Standard: $0.03 per 10,000 operations
        - Application Insights: $2.30 per GB ingested
        - Log Analytics: $2.76 per GB ingested
        - Azure Firewall Standard: $900-1,100/month
        - Azure Firewall Premium: $1,500-1,800/month
        - Front Door Standard: $35/month + $0.01/request
        - Front Door Premium: $330/month + usage
        - Azure Sentinel: $2.46 per GB analyzed
        - Storage Account (Hot): $0.018 per GB/month
        - Data Lake Storage: $0.02 per GB/month

        Add citation [1] at end.
```

- Create a new Variable named varCostEstimate as shown in the image
![alt text](image-2.png)
- Update Set Variable action to include the newly added Generative AI response.
![alt text](image-3.png)
- ![alt text](image-4.png)
- Also, update the Message action shown in the image to add Topic.varCostEstimate.Text.MarkdownContent
- Save the Topic. 
- Start a New Test Session in the chat window to test the new feature as shown in the Image. ![alt text](image-5.png)

---

### 📎 Document Input Support

#### How Users Provide Intake Documents

Both labs support the **existing intake document flow** in your Topic:

| Mode | Input Method | How It Works |
|------|--------------|--------------|
| **Chat Mode** | 📎 **File Upload** | User uploads Word/PDF via the `FilePrebuiltEntity` question node. A Power Automate Flow extracts the content. |
| **Chat Mode** | ⌨️ **Copy/Paste** | User can paste requirements text directly when prompted |
| **Autonomous Mode** | 🤖 **System.Activity.Text** | Intake content passed programmatically via API |

#### Existing Topic Code That Handles This:

```yaml
# File Upload Support (already in your Topic)
- kind: Question
  id: question_CE78PI
  variable: init:Topic.varFile
  prompt: Please upload the intake requirements document
  entity:
    kind: FilePrebuiltEntity
    includeFileMetadata: true

# Flow extracts content from uploaded file
- kind: InvokeFlowAction
  id: invokeFlowAction_QDu2BN
  input:
    binding:
      file: =Topic.varFile
  output:
    binding:
      intakedocumentcontent: Topic.InTakeDocumentContent
```

> **✅ Both labs work with file uploads AND copy/paste** — no changes needed to the intake flow!

---

### 🧪 Sample Test Intake Document

Use this sample for testing. You can either:

- **Copy/paste** when prompted, OR
- **Save as Word document** and upload

```
APPLICATION NAME: Smart Logistics Platform

DESCRIPTION: 
Global shipment tracking and logistics management platform serving enterprise 
customers across North America and Europe. The platform provides real-time 
visibility into shipment status, predictive ETAs, and automated exception handling.

BUSINESS REQUIREMENTS:
- Support 50,000 daily active users across web and mobile channels
- Process 500GB of telemetry data daily from GPS tracking devices
- Real-time shipment tracking with sub-second update latency
- Batch analytics for daily operational reports
- Integration with partner systems for end-to-end visibility

TECHNICAL REQUIREMENTS:
- Primary Region: North America (East US)
- Failover Region: Europe (West Europe)
- Target SLA: 99.9% uptime
- Business Criticality: High

COMPLIANCE AND SECURITY:
- GDPR compliance for European customers
- CCPA compliance for California customers
- Data encryption at rest and in transit
- Zero Trust security model

INTEGRATIONS:
- GeoTrack Inc: GPS telemetry via Kafka streaming
- SAP ERP: Order and inventory data via REST APIs
- Okta: Enterprise SSO and identity federation
- Azure AD B2C: Customer identity management

DATA FLOWS:
- Real-time: WebSocket connections for live tracking updates
- Streaming: Kafka-compatible ingestion for GPS telemetry
- Batch: Nightly ETL for analytics and reporting
- API: REST endpoints for partner integrations

USERS:
- End Users: Customers tracking shipments via web/mobile
- Operations Users: Logistics coordinators managing exceptions
- Admin Users: IT administrators and compliance officers
```

---

## 📘 Lab Option 1: Add Cost Estimation Section

**Difficulty:** Level 300 | **Duration:** 10 minutes

### 🎯 Learning Objectives

By completing this lab, you will:
- Add a new generative AI action to an existing Topic
- Chain outputs between Topic actions
- Modify document assembly logic
- Generate Azure cost estimates based on architecture resources

---

### Step 1: Open the Topic in Copilot Studio (1 min)

1. Navigate to **Copilot Studio** (https://copilotstudio.microsoft.com)
2. Open your **Design Agent**
3. Go to **Topics** → Click on **"Generate Design Document"**
4. Click the **"</>Code Editor"** button to switch to YAML view

![Switch to Code Editor](https://learn.microsoft.com/en-us/microsoft-copilot-studio/media/authoring-create-edit-topics/code-editor-button.png)

---

### Step 2: Locate the Insertion Point (1 min)

Find the `GenerateAzureResourcesTable` action in your YAML. Look for:

```yaml
    - kind: SearchAndSummarizeContent
      id: tX91o2
      displayName: GenerateAzureResourcesTable
      variable: Topic.varAzureResourceTable
```

You will add the new cost estimation action **immediately after** this section and **before** the `ConditionGroup` that handles saving.

---

### Step 3: Add the Cost Estimation Action (4 mins)

**Copy and paste this YAML block** after `GenerateAzureResourcesTable`:

```yaml
    - kind: SearchAndSummarizeContent
      id: CostEst01
      displayName: GenerateCostEstimation
      variable: Topic.varCostEstimate
      userInput: =Topic.varApp & " " & Topic.varAzureResourceTable.Text.MarkdownContent
      additionalInstructions: |-
        You are an Azure cost estimation expert generating a cost analysis section.

        APPLICATION NAME: {Topic.varApp}

        AZURE RESOURCES IDENTIFIED:
        {Topic.varAzureResourceTable.Text.MarkdownContent}

        Generate ONLY the Cost Estimation section.

        COST ESTIMATION SECTION:
        Use exact heading: ## 💰 Estimated Monthly Costs

        INSTRUCTIONS:
        1. Analyze each Azure resource from the resource table
        2. Provide estimated monthly cost ranges based on the SKU tiers identified
        3. Group costs by category

        CREATE A COST TABLE:
        | Category | Resource | SKU | Est. Monthly Cost (USD) |
        |----------|----------|-----|-------------------------|

        Include these categories:
        - **Compute:** App Services, Functions, Container Apps
        - **Data:** SQL Database, Cosmos DB, Storage Accounts
        - **Networking:** Front Door, Firewall, Private Link, Bandwidth
        - **Security:** Key Vault, WAF, DDoS Protection
        - **Monitoring:** Application Insights, Log Analytics, Sentinel

        AFTER THE TABLE ADD:

        ### 📊 Cost Summary
        - **Estimated Monthly Total:** $X,XXX - $X,XXX
        - **Estimated Annual Total:** $XX,XXX - $XX,XXX

        ### 💡 Cost Optimization Recommendations
        Add 3-4 bullet points with cost-saving recommendations such as:
        - Reserved Instances for predictable workloads
        - Auto-scaling policies to reduce off-peak costs
        - Lifecycle policies for storage
        - Right-sizing based on actual usage

        PRICING GUIDELINES (use these estimates):
        - App Service P2v2: $150-200/month per instance
        - App Service P3v2: $300-400/month per instance
        - SQL Database Business Critical: $400-800/month
        - SQL Database Standard: $150-300/month
        - Event Hubs Standard: $20-50/month per TU
        - Event Hubs Premium: $100-200/month per PU
        - Key Vault Standard: $0.03 per 10,000 operations
        - Application Insights: $2.30 per GB ingested
        - Log Analytics: $2.76 per GB ingested
        - Azure Firewall Standard: $900-1,100/month
        - Azure Firewall Premium: $1,500-1,800/month
        - Front Door Standard: $35/month + $0.01/request
        - Front Door Premium: $330/month + usage
        - Azure Sentinel: $2.46 per GB analyzed
        - Storage Account (Hot): $0.018 per GB/month
        - Data Lake Storage: $0.02 per GB/month

        Add citation [1] at end.
      fileSearchDataSource:
        searchFilesMode:
          kind: SearchAllFiles
      knowledgeSources:
        kind: SearchAllKnowledgeSources
      responseCaptureType: FullResponse
```

---

### Step 4: Update the Document Assembly (2 mins)

Find the `setVariable_P3CNQA` action that assembles the final document:

**BEFORE (existing code):**

```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
```

**AFTER (add the cost estimate):**

```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varCostEstimate.Text.MarkdownContent
```

---

### Step 5: Update Display-Only Output (1 min)

Find the `sendActivity_displayOnly` section in the `elseActions` block:

**BEFORE:**

```yaml
        - kind: SendActivity
          id: sendActivity_displayOnly
          activity: |-
            **Target Azure Architecture Document for {Topic.varApp}**

            {Topic.varIntroOverview.Text.MarkdownContent}

            {Topic.varDataFlows.Text.MarkdownContent}

            {Topic.varDetailedViews.Text.MarkdownContent}

            {Topic.varRationale.Text.MarkdownContent}

            {Topic.varAzureResourceTable.Text.MarkdownContent}
```

**AFTER:**

```yaml
        - kind: SendActivity
          id: sendActivity_displayOnly
          activity: |-
            **Target Azure Architecture Document for {Topic.varApp}**

            {Topic.varIntroOverview.Text.MarkdownContent}

            {Topic.varDataFlows.Text.MarkdownContent}

            {Topic.varDetailedViews.Text.MarkdownContent}

            {Topic.varRationale.Text.MarkdownContent}

            {Topic.varAzureResourceTable.Text.MarkdownContent}

            {Topic.varCostEstimate.Text.MarkdownContent}
```

---

### Step 6: Save and Test (1 min)

1. Click **Save** in the Code Editor
2. Open the **Test Panel** (right side)
3. Type: `Generate and save design document`
4. When prompted, enter App Name: `Smart Logistics Platform`
5. When prompted, **upload** the sample intake document (Word file) OR **paste** the sample text
6. Wait for generation to complete
7. **Verify** the output includes the new **💰 Estimated Monthly Costs** section

---

### ✅ Lab 1 Success Criteria

| Checkpoint | Expected Result |
|------------|-----------------|
| Topic saves without errors | ✅ No YAML syntax errors shown |
| Cost section appears in chat output | ✅ Shows cost table with categories |
| Cost summary included | ✅ Monthly and annual totals displayed |
| Optimization recommendations present | ✅ 3-4 bullet points shown |
| SharePoint document includes costs | ✅ New section at end of saved document |

---

### 🔧 Troubleshooting Lab 1

| Issue | Solution |
|-------|----------|
| YAML syntax error on save | Check indentation (use 2 spaces, not tabs) |
| `varCostEstimate` is empty | Ensure the action ID `CostEst01` is unique |
| Costs not appearing in saved doc | Verify `& Topic.varCostEstimate.Text.MarkdownContent` was added |
| Action not executing | Check action is placed after `GenerateAzureResourcesTable` |

---

---

## 📘 Lab Option 2: Add WAF Compliance Checklist

**Difficulty:** Level 350 | **Duration:** 10 minutes

### 🎯 Learning Objectives

By completing this lab, you will:
- Implement Azure Well-Architected Framework validation
- Create automated compliance checklists with status indicators
- Integrate governance checks into document generation
- Provide actionable recommendations based on architecture analysis

---

### Step 1: Open the Topic in Copilot Studio (1 min)

1. Navigate to **Copilot Studio** (https://copilotstudio.microsoft.com)
2. Open your **Design Agent**
3. Go to **Topics** → Click on **"Generate Design Document"**
4. Click **"</>Code Editor"** to switch to YAML view

---

### Step 2: Locate the Insertion Point (1 min)

Find the `GenerateAzureResourcesTable` action. You will add the WAF Checklist action **immediately after** it.

```yaml
    - kind: SearchAndSummarizeContent
      id: tX91o2
      displayName: GenerateAzureResourcesTable
      variable: Topic.varAzureResourceTable
      ...
      responseCaptureType: FullResponse
    
    # <-- INSERT NEW ACTION HERE -->
    
    - kind: ConditionGroup
      id: conditionGroup_MoDYK2
```

---

### Step 3: Add the WAF Checklist Action (5 mins)

**Copy and paste this YAML block** after `GenerateAzureResourcesTable`:

```yaml
    - kind: SearchAndSummarizeContent
      id: WAFCheck01
      displayName: GenerateWAFChecklist
      variable: Topic.varWAFChecklist
      userInput: =Topic.varApp & " " & Topic.varIntakeText & " " & Topic.varAzureResourceTable.Text.MarkdownContent
      additionalInstructions: |-
        You are an Azure Well-Architected Framework (WAF) expert generating a compliance checklist.

        APPLICATION NAME: {Topic.varApp}

        INTAKE DOCUMENT:
        {Topic.varIntakeText}

        AZURE RESOURCES:
        {Topic.varAzureResourceTable.Text.MarkdownContent}

        Generate ONLY the WAF Compliance Checklist section.

        Use exact heading: ## ✅ Well-Architected Framework Compliance Checklist

        ANALYZE the intake document and resource table against each WAF pillar.
        Use these status indicators:
        - ✅ Fully addressed in the design
        - ⚠️ Partially addressed or needs clarification
        - ❌ Not addressed or missing

        CREATE CHECKLIST FOR EACH PILLAR:

        ### 🛡️ Reliability
        Evaluate and list 5 items with status indicators:
        - Multi-region deployment configured
        - Failover strategy defined (active-passive or active-active)
        - RTO and RPO requirements documented
        - Health probes and monitoring configured
        - Backup and disaster recovery plan included

        ### 🔐 Security
        Evaluate and list 5 items with status indicators:
        - Zero Trust architecture principles applied
        - Network segmentation with NSGs and Firewall
        - Data encryption at rest and in transit
        - Identity management with Azure AD or B2C
        - Secrets management using Key Vault
        - Threat detection with Sentinel or Defender

        ### ⚡ Performance Efficiency
        Evaluate and list 5 items with status indicators:
        - Auto-scaling configuration defined
        - Caching strategy for frequently accessed data
        - CDN or Front Door for global user access
        - Database tier appropriate for expected load
        - Async processing for heavy or batch workloads

        ### 💵 Cost Optimization
        Evaluate and list 5 items with status indicators:
        - Right-sized SKUs based on requirements
        - Reserved capacity opportunities identified
        - Auto-shutdown policies for non-production
        - Storage tiering and lifecycle policies
        - Cost monitoring and alerting configured

        ### 🔧 Operational Excellence
        Evaluate and list 5 items with status indicators:
        - Centralized logging with Log Analytics
        - Application performance monitoring with App Insights
        - Alerting rules and dashboards defined
        - Infrastructure as Code for deployments
        - Runbooks for common operational tasks

        AFTER THE CHECKLISTS ADD:

        ### 📊 Compliance Summary Table

        | Pillar | Status | Items Addressed | Score |
        |--------|--------|-----------------|-------|
        | Reliability | ✅/⚠️/❌ | X of 5 | X/5 |
        | Security | ✅/⚠️/❌ | X of 6 | X/6 |
        | Performance | ✅/⚠️/❌ | X of 5 | X/5 |
        | Cost Optimization | ✅/⚠️/❌ | X of 5 | X/5 |
        | Operational Excellence | ✅/⚠️/❌ | X of 5 | X/5 |
        | **Overall WAF Score** | | | **X/26** |

        STATUS DETERMINATION:
        - ✅ if score is 80% or higher
        - ⚠️ if score is 50-79%
        - ❌ if score is below 50%

        ### 🎯 Priority Recommendations

        List the top 3-5 items that need immediate attention before architecture approval.
        Format as numbered list with brief explanation for each.

        Add citation [1] at end.
      fileSearchDataSource:
        searchFilesMode:
          kind: SearchAllFiles
      knowledgeSources:
        kind: SearchAllKnowledgeSources
      responseCaptureType: FullResponse
```

---

### Step 4: Update the Document Assembly (2 mins)

Find the `setVariable_P3CNQA` action:

**BEFORE (existing code):**

```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
```

**AFTER (add WAF checklist):**

```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varWAFChecklist.Text.MarkdownContent
```

---

### Step 5: Update Display-Only Output (1 min)

Find the `sendActivity_displayOnly` section:

**BEFORE:**
```yaml
        - kind: SendActivity
          id: sendActivity_displayOnly
          activity: |-
            **Target Azure Architecture Document for {Topic.varApp}**

            {Topic.varIntroOverview.Text.MarkdownContent}

            {Topic.varDataFlows.Text.MarkdownContent}

            {Topic.varDetailedViews.Text.MarkdownContent}

            {Topic.varRationale.Text.MarkdownContent}

            {Topic.varAzureResourceTable.Text.MarkdownContent}
```

**AFTER:**
```yaml
        - kind: SendActivity
          id: sendActivity_displayOnly
          activity: |-
            **Target Azure Architecture Document for {Topic.varApp}**

            {Topic.varIntroOverview.Text.MarkdownContent}

            {Topic.varDataFlows.Text.MarkdownContent}

            {Topic.varDetailedViews.Text.MarkdownContent}

            {Topic.varRationale.Text.MarkdownContent}

            {Topic.varAzureResourceTable.Text.MarkdownContent}

            {Topic.varWAFChecklist.Text.MarkdownContent}
```

---

### Step 6: Save and Test (1 min)

1. Click **Save** in the Code Editor
2. Open the **Test Panel**
3. Type: `Generate design document`
4. Enter App Name: `Smart Logistics Platform`
5. **Upload** the sample intake Word document OR **paste** the sample text
6. **Verify** the WAF Checklist section appears with:
   - All 5 WAF pillars with status indicators
   - Compliance summary table with scores
   - Priority recommendations list

---

### ✅ Lab 2 Success Criteria

| Checkpoint | Expected Result |
|------------|-----------------|
| Topic saves without errors | ✅ No YAML syntax errors |
| All 5 WAF pillars displayed | ✅ Reliability, Security, Performance, Cost, Operations |
| Status indicators used correctly | ✅ Shows ✅, ⚠️, or ❌ based on analysis |
| Compliance summary table present | ✅ Shows scores per pillar |
| Overall WAF score calculated | ✅ Total score out of 26 shown |
| Priority recommendations listed | ✅ 3-5 actionable items |

---

### 🔧 Troubleshooting Lab 2

| Issue | Solution |
|-------|----------|
| WAF section empty | Ensure `Topic.varIntakeText` has content |
| Missing status indicators | Check the prompt includes status indicator instructions |
| Scores don't add up | This is generative; minor calculation errors are expected |
| Action not in correct position | Must be after `GenerateAzureResourcesTable` |

---

---

## 🏆 Bonus Challenge: Combine Both Labs

**Duration:** 5 additional minutes

If you completed both labs, combine them into a single comprehensive document:

### Update Document Assembly with Both Sections:

```yaml
            - kind: SetVariable
              id: setVariable_P3CNQA
              variable: Topic.varArchitectureDoc
              value: |-
                =Topic.varIntroOverview.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varDataFlows.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varDetailedViews.Text.MarkdownContent 
                  & Char(10) & Char(10) 
                  & Topic.varRationale.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varAzureResourceTable.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varCostEstimate.Text.MarkdownContent
                  & Char(10) & Char(10) 
                  & Topic.varWAFChecklist.Text.MarkdownContent
```

### Final Document Structure:

```
📦 [App Name] — Target Azure Architecture Details
├── 🧭 Introduction
├── 🏗️ Architecture Overview
├── 🔄 Data Flows
├── 🧩 Detailed Description of Each View
│   ├── 1) Logical View
│   ├── 2) High-Level Technical View
│   ├── 3) Detailed Infrastructure View
│   ├── 4) Networking and Security View
│   └── 5) Monitoring and Logging View
├── 🧪 Rationales
├── ⚠️ Limitations
├── 📋 Azure Resource Table
├── 💰 Estimated Monthly Costs        ← Lab 1
└── ✅ WAF Compliance Checklist       ← Lab 2
```

---

## 📚 Additional Resources

| Resource | Link |
|----------|------|
| Azure Well-Architected Framework | https://learn.microsoft.com/azure/well-architected/ |
| Azure Pricing Calculator | https://azure.microsoft.com/pricing/calculator/ |
| Copilot Studio Documentation | https://learn.microsoft.com/microsoft-copilot-studio/ |
| Copilot Studio YAML Reference | https://learn.microsoft.com/microsoft-copilot-studio/authoring-create-edit-topics |

---

## 📝 Lab Completion Checklist

| Lab | Status |
|-----|--------|
| Lab 1: Cost Estimation | ⬜ Not Started / ⬜ In Progress / ⬜ Completed |
| Lab 2: WAF Checklist | ⬜ Not Started / ⬜ In Progress / ⬜ Completed |
| Bonus: Combined | ⬜ Not Started / ⬜ In Progress / ⬜ Completed |

**Instructor Sign-off:** _________________ **Date:** _____________

---
