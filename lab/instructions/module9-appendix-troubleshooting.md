# Appendix: Troubleshooting

## Common Issues and Solutions

### Issue 1: Agent Not Responding

**Symptoms:** Agent shows "typing" indicator but never responds

**Solutions:**

1. Check Power Automate flow status – ensure all flows are **turned on**
2. Verify connection authentication – connections may have expired
3. Check GPT-5 model availability in your region

### Issue 2: Document Extraction Fails

**Symptoms:** Error when uploading intake document

**Solutions:**

1. Verify file format is supported (PDF, DOCX, TXT)
2. Check file size is under 10MB
3. Ensure SharePoint connection has read permissions

### Issue 3: Missing Diagrams

**Symptoms:** Architecture views don't include Mermaid diagrams

**Solutions:**

1. Verify the knowledge file is properly loaded
2. Check that the generation prompt includes diagram instructions
3. Regenerate the document

### Issue 4: Connection Errors

**Symptoms:** "Connection not found" or authentication errors

**Solutions:**

1. Navigate to **Power Platform Admin Center** > **Connections**
2. Delete and recreate failed connections
3. Update connection references in all Power Automate flows
4. Republish the agent

## Analytics and Monitoring

Monitor agent performance in the **Analytics** section:

| Metric | Description | Target |
| -------- | ------------- | -------- |
| Runs | Total conversations | Trending ↑ |
| Successful runs | Percentage of completions | > 85% |
| Average duration | Time to generate document | < 90 sec |
