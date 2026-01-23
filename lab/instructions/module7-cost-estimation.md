# Module 7:  Design Agent adding Cost Estimation Topic (10 minutes)

## Option 1: Add Cost Estimation Section

### Step 1: Enable Web Search and Topic changes Copilot Studio

1. Hover over the Agent icon on the left ribbon to show the list of the Agents and click on **Application Design Agent**

    ![ApplicationDesignAgent](7.1_1-ApplicationDesignAgent.png)

2. Navigate to Overview tab on the top
3. Scroll down to Knowledge and Enable **Web Search**

    ![webSearch](7.1_3-WebSearch.png)

4. Go to Topics on the top and click **Generate and save Azure architecture doc** from the list of Topics.

    ![Topics](7.1_4-Topics.png)

5. Scroll down to **GenerateAzureResourcesTable** Node and click **Add node** right after. 
6. Select Advanced -> Generative Answers

    ![GenerativeAnswers](7.1_6-GenerativeAnswers.png)

7. Click on the name and replace by **GenerateCostEstimation**
8. Click on the **elipses (...)** in the **Input** section
9. Add the following expression by clicking on the Formula tab 

        Topic.varApp & " Azure cost estimation pricing monthly compute data networking"

   and click on **Insert**

    ![Formula](7.1_9-Formula.png)

10. Stay in the Node, click on **elipses (...)** then **Properties**. 
11. In the Properties Pane, click on *Search only selected sources* and mark all of them clicking on *Name* checkbox. Then scroll down to **Content moderation level**, under **Customize**  insert the generative AI instruction. *(Copy/Paste the text below)* 

    ```yaml
            You are an Azure cost estimation expert generating a cost analysis section.

            IMPORTANT: Use ONLY the information provided in this prompt. Do NOT rely on external knowledge sources for the application-specific content.

            APPLICATION NAME: {Topic.varApp}

            ================== APPLICATION REQUIREMENTS ==================
            {Topic.varIntakeText}
            ================== END REQUIREMENTS ==================

            ================== AZURE RESOURCES ==================
            {Topic.varAzureResourceTable.Text.MarkdownContent}
            ================== END AZURE RESOURCES ==================

            Generate ONLY the Cost Estimation section.

            COST ESTIMATION SECTION:
            Use exact heading: ## 💰 Estimated Monthly Costs

            INSTRUCTIONS:
            1. Analyze the intake document to identify Azure resources needed
            2. Provide estimated monthly cost ranges based on business criticality and SKU tiers
            3. Group costs by category

            CREATE A COST TABLE:
            | Category | Resource | SKU | Est. Monthly Cost (USD) |
            |----------|----------|-----|-------------------------|

            Include these categories based on intake requirements:
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
            - SQL Database Business Critical: $400-800/month
            - Event Hubs Standard: $20-50/month per throughput unit
            - Key Vault: $0.03 per 10,000 operations
            - Application Insights: $2.30 per GB ingested
            - Log Analytics: $2.76 per GB ingested
            - Azure Firewall: $900-1,100/month
            - Front Door: $35/month base + $0.01 per request

            Add citation [1] at end.
      ```

     ![PropertiesPane](7.1_11-PropertiesPane.png)

12. Stay in the **Properties Pane** scroll down and expand **Advanced**. We are going to create a variable to add the Cost estimation value
13. Select **Complete (recommended)** from the list in **Save LLM response** field
14. Click on the display button of the **Save bot response as**
15. Click on **{x} Create a new variable** to create a new Variable named **varCostEstimate**

    ![Variable](7.1_15-Variable.png)


16. Close the Properties pane.

Now let's update two nodes (_Set variable value_ and _Message_) in this flow with this new variable

- Set variable value

  1. In the Flow go to **Set variable value** Node (two nodes after the GenerateCostEstimation node recently created)
  2. Click on the **elipses (...)** in **To value** field into the **Set variable value** node
  
      ![SetValue](7.1_16.1-SetValue.png)
  
  3. Expand the form and enter at the end of the formula
      
        & Char(10) & Char(10)                  
        & Topic.varCostEstimate.Text.MarkdownContent

    as shown in the image
      
  4. Click **Insert**

      ![Insert](7.1-16.4-Insert.png)

- Message

  1. In the Flow go to **Message** Node (on the right of the **Set variable value** Node of the prior step) and click on **Target Azure Architecture Document for**

      ![Message](7.2-16.1-Message.png)

  2. Click on variable Icon
  3. In the text field type the name of the created variable **varCostEstimate**
  4. Scroll down and select **varCostEstimate.Text.MarkdownContent**

      ![Variable](7.1-16.4-Variable.png)

  5. Click on _Save_ on the top right

17. Start a New Test Session in the chat window to test the new feature as shown in the Image. 

      ![Response](7.1-17-Response.png)

---
