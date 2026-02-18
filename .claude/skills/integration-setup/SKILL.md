---
name: integration-setup
displayName: "Integration Setup Guide"
version: 1.0.0
description: Step-by-step CRM integration guides (HubSpot, Salesforce) and webhook configuration helpers
author: "ColdSend Team"
license: "MIT"
repository: "https://github.com/coldsendhq/coldsend-skills"

category: marketing
subcategory: integrations
type: command
difficulty: advanced

keywords:
- crm-integration
- hubspot-setup
- salesforce-setup
- webhook-configuration
- api-integration

minClaudeVersion: "1.0.0"
platforms:
- macos
- linux
- windows

filesystem:
read:
- "${PROJECT_ROOT}/**/*"
write:
- "${PROJECT_ROOT}/integrations/*"
- "${PROJECT_ROOT}/webhooks/*"
deny:
- "**/.env*"
- "**/*.key"

tools:
allowed:
- Read
- Write
- Bash
denied: []

input:
arguments:
- name: integration_type
type: string
description: Type of integration to set up
enum: ["hubspot", "salesforce", "pipedrive", "custom_webhook", "zapier", "make"]
required: true
- name: use_case
type: string
description: Primary use case
enum: ["lead_sync", "contact_creation", "deal_tracking", "activity_logging", "bidirectional"]
required: false
default: "lead_sync"
- name: technical_level
type: string
description: User's technical comfort level
enum: ["beginner", "intermediate", "advanced"]
default: "intermediate"
required: false

output:
format: markdown

behavior:
timeout: 300
cache:
enabled: true
ttlSeconds: 900
---

# Integration Setup Guide

You are a solutions architect specializing in cold email platform integrations and marketing automation.

## When to Use This Skill

Use this skill when:
- User wants to integrate ColdSend with CRM
- User asks about HubSpot/Salesforce setup
- User needs webhook configuration help
- User requests API integration guidance
- User wants to automate data sync between tools

## Integration Framework

### Step 1: Assess Requirements

#### Discovery Questions

Ask user:
1. **Which CRM/Platform?**
   - HubSpot
   - Salesforce
   - Pipedrive
   - Custom (via webhook/API)
   - Automation tool (Zapier, Make)

2. **What's the Primary Goal?**
   - Sync leads from ColdSend → CRM
   - Create contacts automatically
   - Track email activity in CRM
   - Update deal stages based on engagement
   - Bidirectional sync

3. **Technical Comfort Level?**
   - Beginner: Prefer no-code solutions
   - Intermediate: Can follow technical guides
   - Advanced: Comfortable with APIs/code

4. **Data Flow Direction?**
   - One-way (ColdSend → CRM)
   - One-way (CRM → ColdSend)
   - Bidirectional sync

5. **Trigger Events?**
   - On lead response
   - On meeting booked
   - On email open/click
   - Real-time vs batch updates

### Step 2: Choose Integration Method

#### Method Comparison

| Method | Difficulty | Cost | Flexibility | Best For |
|--------|------------|------|-------------|----------|
| **Native Integration** | Easy | Free | Medium | Standard use cases |
| **Zapier** | Easy-Medium | $20-50/mo | High | Quick setup, multiple apps |
| **Make (Integromat)** | Medium | $9-29/mo | High | Complex workflows |
| **Custom Webhook** | Medium-Hard | Free | Very High | Custom requirements |
| **Direct API** | Hard | Free | Maximum | Developers, custom apps |

#### Decision Matrix

**Choose Native Integration if:**
- ✅ Available for your CRM
- ✅ Meets all requirements
- ✅ Want simplest setup
- ✅ No custom logic needed

**Choose Zapier/Make if:**
- ✅ Need multi-step workflows
- ✅ Connecting multiple apps
- ✅ Want visual workflow builder
- ✅ Okay with monthly cost

**Choose Custom Webhook if:**
- ✅ Need real-time sync
- ✅ Have specific requirements
- ✅ Want to avoid monthly fees
- ✅ Technical resources available

**Choose Direct API if:**
- ✅ Building custom application
- ✅ Need maximum control
- ✅ Have development team
- ✅ High volume/custom logic

### Step 3: HubSpot Integration

#### Option A: Native Integration (Recommended)

**Setup Steps:**

**1. In ColdSend Dashboard:**
```
Settings → Integrations → HubSpot → Connect
```

**2. Authenticate:**
- Log into HubSpot account
- Grant permissions
- Select portal (if multiple)

**3. Configure Field Mapping:**
```
ColdSend Field → HubSpot Property
------------------------------------
Email → email
First Name → firstname
Last Name → lastname
Company → company
Title → jobtitle
Phone → phone
Lead Score → lead_score (custom)
Campaign → campaign_name (custom)
```

**4. Set Up Automation Rules:**
```
When [Event] occurs in ColdSend:
→ [Action] in HubSpot

Examples:
- Lead replies → Create task for owner
- Meeting booked → Update deal stage
- Email clicked → Add to workflow
- Unsubscribed → Add to suppression list
```

**5. Test Connection:**
- Send test lead through
- Verify appears in HubSpot
- Check field mapping accuracy
- Confirm automation triggers

#### Option B: Zapier Integration

**Prerequisites:**
- Zapier account ($20+/month)
- ColdSend API access
- HubSpot account

**Step-by-Step:**

**Zap 1: New Reply → Create Contact in HubSpot**

1. **Trigger: ColdSend - "New Reply"**
   - Connect ColdSend account (API key)
   - Select campaign(s) to monitor
   - Test trigger

2. **Action: HubSpot - "Create Contact"**
   - Connect HubSpot account
   - Map fields:
     ```
     Email → email
     First Name → firstname
     Last Name → lastname
     Company → company
     Reply Content → recent_note
     Campaign → source_campaign
     ```
   - Test action

3. **Configure Settings:**
   - Enable duplicate checking (by email)
   - Set owner assignment rules
   - Add tags/properties

4. **Turn On Zap**
   - Monitor for first few runs
   - Check for errors

**Zap 2: Meeting Booked → Update Deal Stage**

1. **Trigger: ColdSend - "Meeting Booked"**
2. **Action: HubSpot - "Find Deal"** (by email)
3. **Action: HubSpot - "Update Deal"**
   - Set stage to "Meeting Scheduled"
   - Add meeting date property
   - Create task for sales rep

**Estimated Setup Time:** 30-45 minutes
**Monthly Cost:** $20-50 (Zapier subscription)

#### Option C: Custom Webhook

**For Advanced Users:**

**Webhook Endpoint Setup:**

```python
from flask import Flask, request, jsonify
import requests

app = Flask(__name__)

HUBSPOT_API_KEY = "your_api_key"
HUBSPOT_PORTAL_ID = "your_portal_id"

@app.route('/webhook/coldsend', methods=['POST'])
def handle_coldsend_webhook():
    data = request.json
    
    # Parse ColdSend event
    event_type = data.get('event')
    contact_data = data.get('data')
    
    if event_type == 'reply':
        create_hubspot_contact(contact_data)
        log_activity(contact_data)
    
    elif event_type == 'meeting_booked':
        update_deal_stage(contact_data)
        create_task(contact_data)
    
    return jsonify({"status": "success"}), 200

def create_hubspot_contact(data):
    url = f"https://api.hubapi.com/crm/v3/objects/contacts"
    
    headers = {
        'Authorization': f'Bearer {HUBSPOT_API_KEY}',
        'Content-Type': 'application/json'
    }
    
    body = {
        "properties": {
            "email": data['email'],
            "firstname": data['first_name'],
            "lastname": data['last_name'],
            "company": data['company'],
            "phone": data.get('phone', ''),
            "hs_lead_status": "New",
            "coldsend_campaign__c": data.get('campaign', ''),
            "recent_note": f"Replied to ColdSend campaign on {data.get('date')}"
        }
    }
    
    response = requests.post(url, headers=headers, json=body)
    return response.json()

if __name__ == '__main__':
    app.run(port=5000, debug=True)
```

**Deploy Options:**
- AWS Lambda + API Gateway
- Google Cloud Functions
- Heroku
- DigitalOcean App Platform

**Cost:** Free-$20/month depending on hosting

### Step 4: Salesforce Integration

#### Option A: Native Integration

**Setup Process:**

**1. Install ColdSend Package:**
```
Salesforce AppExchange → Search "ColdSend" → Install
```

**2. Configure Connection:**
```
Setup → Installed Packages → ColdSend → Configure
→ Enter ColdSend API credentials
→ Select sync direction
```

**3. Field Mapping:**
```
ColdSend → Salesforce Object/Field
-------------------------------------
Email → Contact.Email
First Name → Contact.FirstName
Last Name → Contact.LastName
Company → Account.Name
Title → Contact.Title
Campaign → CampaignMember.CampaignId
Lead Status → Lead.Status
```

**4. Automation Rules:**
```
Process Builder / Flow:
WHEN ColdSend_Event__c = 'Reply'
CREATE Task
ASSIGN TO Lead.Owner
PRIORITY = High
DUE DATE = TODAY
```

#### Option B: Zapier for Salesforce

Similar to HubSpot setup, but with Salesforce actions:
- Create Lead
- Create Contact
- Update Opportunity
- Create Task
- Add to Campaign

**Common Zaps:**
1. New Reply → Create Lead + Task
2. Meeting Booked → Update Opportunity Stage
3. Email Clicked → Log Activity
4. Unsubscribe → Update Do Not Contact flag

### Step 5: Webhook Configuration

#### ColdSend Webhook Setup

**In ColdSend Dashboard:**
```
Settings → Webhooks → Add Webhook
```

**Configuration:**
```
Endpoint URL: https://your-domain.com/webhook/coldsend
Events to Subscribe:
☑ Lead replied
☑ Meeting booked
☑ Email opened
☑ Email clicked
☑ Unsubscribed
☑ Bounced

Authentication: Bearer token or Basic Auth
Retry Policy: 3 attempts, exponential backoff
Timeout: 30 seconds
```

**Webhook Payload Format:**

```json
{
  "event": "reply",
  "timestamp": "2025-01-15T10:30:00Z",
  "campaign_id": "abc-123",
  "campaign_name": "Q1 Outreach",
  "data": {
    "lead_id": "xyz-789",
    "email": "prospect@company.com",
    "first_name": "John",
    "last_name": "Doe",
    "company": "Acme Inc",
    "reply_content": "Yes, I'm interested...",
    "reply_timestamp": "2025-01-15T10:29:45Z"
  }
}
```

#### Testing Webhooks

**Local Testing with ngrok:**
```bash
# Install ngrok
npm install -g ngrok

# Expose local server
ngrok http 5000

# Use the ngrok URL in ColdSend webhook settings
# https://abc123.ngrok.io/webhook/coldsend
```

**Testing Tools:**
- Postman (manual webhook testing)
- Webhook.site (temporary endpoint)
- RequestBin (payload inspection)

### Step 6: Error Handling & Monitoring

#### Common Issues & Solutions

**Issue 1: Authentication Failures**
**Symptoms:** 401/403 errors
**Solution:**
- Verify API keys/tokens
- Check expiration dates
- Regenerate credentials
- Review permission scopes

**Issue 2: Duplicate Records**
**Symptoms:** Same contact created multiple times
**Solution:**
- Implement deduplication logic
- Use external ID fields
- Check before create operations
- Enable native deduplication

**Issue 3: Field Mapping Errors**
**Symptoms:** Data not syncing correctly
**Solution:**
- Audit field mappings
- Check data type compatibility
- Verify required fields populated
- Test with sample data

**Issue 4: Rate Limiting**
**Symptoms:** 429 errors, failed syncs
**Solution:**
- Implement retry logic with backoff
- Batch operations where possible
- Respect API rate limits
- Upgrade plan if needed

#### Monitoring Best Practices

**Set Up Alerts For:**
- Failed webhook deliveries (>5 failures)
- Authentication errors
- Sync delays (>15 minutes)
- Data validation errors

**Logging Requirements:**
- All webhook payloads
- API request/response logs
- Error messages with stack traces
- Success/failure counts

## Output Template

```
🔌 Integration Setup Guide
Integration Type: [HubSpot/Salesforce/Custom]
Use Case: [Lead Sync/Contact Creation/etc.]
Difficulty: [Easy/Medium/Hard]
Estimated Time: [X] minutes

## Overview

**Integration Method:** [Native/Zapier/Custom Webhook/API]

**What This Does:**
- [Capability 1]
- [Capability 2]
- [Capability 3]

**Prerequisites:**
- ✅ [Requirement 1]
- ✅ [Requirement 2]
- ✅ [Requirement 3]

**Cost:**
- Setup: Free / $[X]
- Ongoing: Free / $[X]/month

## Step-by-Step Instructions

### Phase 1: Preparation (15 minutes)

#### Step 1.1: Gather Credentials

**ColdSend:**
1. Go to Settings → API Keys
2. Generate new API key if needed
3. Copy and store securely: `[api_key_placeholder]`

**[CRM Platform]:**
1. Go to Settings → Integrations → API Access
2. Generate client ID and secret
3. Note your [account ID/portal ID/org ID]
4. Store credentials securely

#### Step 1.2: Verify Permissions

**Required ColdSend Permissions:**
- ☑ Read campaigns
- ☑ Read leads
- ☑ Read analytics
- ☑ Webhook access

**Required CRM Permissions:**
- ☑ Create/edit contacts
- ☑ Create/edit deals
- ☑ Create tasks
- ☑ API access

### Phase 2: Configuration ([X] minutes)

#### Step 2.1: [First Major Step]

**Detailed Instructions:**
1. [Action with screenshot description]
2. [Next action]
3. [Continue sequence]

**Expected Result:**
[What should happen after completing step]

**Troubleshooting:**
- If [problem]: Try [solution]
- If [other problem]: Check [setting]

#### Step 2.2: [Second Major Step]

[Repeat structure]

### Phase 3: Field Mapping (10 minutes)

#### Default Mapping

| ColdSend Field | [CRM] Field | Type | Required |
|----------------|-------------|------|----------|
| Email | [field_name] | Text | Yes |
| First Name | [field_name] | Text | Yes |
| Last Name | [field_name] | Text | No |
| Company | [field_name] | Text | No |
| Title | [field_name] | Text | No |
| Phone | [field_name] | Text | No |
| Campaign | [field_name] | Text | No |
| Lead Score | [field_name] | Number | No |

#### Custom Fields to Create

**In [CRM], create these custom fields:**

**Field 1:**
- Name: `ColdSend Campaign`
- Type: Text
- Object: Contact/Lead
- Required: No

**Field 2:**
- Name: `ColdSend Lead Score`
- Type: Number
- Object: Contact/Lead
- Required: No

[Add more as needed]

### Phase 4: Automation Rules (15 minutes)

#### Rule 1: New Reply → Create Task

**Trigger:**
- Event: Lead replies to ColdSend email
- Conditions: Reply is positive (contains keywords: interested, yes, sure, etc.)

**Action:**
- Create task in CRM
- Assign to: Lead owner
- Priority: High
- Due date: Today
- Subject: "Follow up with ColdSend reply"
- Description: Include reply content

#### Rule 2: Meeting Booked → Update Deal

**Trigger:**
- Event: Meeting scheduled via ColdSend

**Actions:**
1. Find existing deal by email
2. Update stage to "Meeting Scheduled"
3. Add meeting date to custom field
4. Create calendar event
5. Send notification to owner

### Phase 5: Testing (20 minutes)

#### Test Scenario 1: New Lead Sync

**Steps:**
1. Add test lead to ColdSend
2. Trigger manual sync (or wait for automatic)
3. Verify lead appears in CRM
4. Check all fields mapped correctly
5. Confirm no duplicates created

**Expected Result:**
✅ Lead created in CRM with correct data

**If Fails:**
- Check API credentials
- Verify field names match exactly
- Review error logs

#### Test Scenario 2: Reply Tracking

**Steps:**
1. Send email from test lead
2. Reply to it
3. Check CRM for task creation
4. Verify activity logged

**Expected Result:**
✅ Task created, activity history updated

#### Test Scenario 3: Meeting Booking

**Steps:**
1. Book meeting via test lead
2. Check CRM deal stage update
3. Verify task/notification created

**Expected Result:**
✅ Deal updated, task assigned

### Phase 6: Go-Live Checklist

**Before Activating:**
- ☐ All test scenarios passed
- ☐ Field mapping verified
- ☐ Automation rules tested
- ☐ Error handling in place
- ☐ Monitoring configured
- ☐ Team trained on new workflow
- ☐ Documentation shared

**Launch Plan:**
1. Enable integration for small pilot group
2. Monitor for 24-48 hours
3. Fix any issues discovered
4. Roll out to full team
5. Continue monitoring

## Troubleshooting Guide

### Common Issues

#### Issue: "Authentication Failed" Error

**Possible Causes:**
- Invalid API key
- Expired token
- Wrong credentials format

**Solutions:**
1. Regenerate API key in ColdSend
2. Re-authenticate in CRM
3. Check for extra spaces in credentials
4. Verify correct auth method (Bearer vs Basic)

#### Issue: Duplicate Contacts Created

**Possible Causes:**
- Deduplication not enabled
- Email matching not working
- Multiple zaps running

**Solutions:**
1. Enable "Check for duplicates" in Zapier
2. Use external ID for matching
3. Consolidate automation rules
4. Run deduplication cleanup

#### Issue: Data Not Syncing

**Possible Causes:**
- Webhook not firing
- API rate limit exceeded
- Field type mismatch
- Missing required fields

**Solutions:**
1. Check webhook delivery logs
2. Implement retry logic
3. Verify field types match
4. Add missing required fields

#### Issue: Slow Sync Delays

**Possible Causes:**
- Batch processing intervals
- API throttling
- Queue backups

**Solutions:**
1. Switch to real-time webhooks
2. Increase API rate limits (upgrade plan)
3. Optimize batch sizes
4. Add monitoring for queue depth

## Monitoring & Maintenance

### Daily Checks (5 minutes)
- [ ] Review sync success rate
- [ ] Check for failed webhooks
- [ ] Monitor error logs
- [ ] Verify data quality spot-checks

### Weekly Reviews (30 minutes)
- [ ] Full audit of synced records
- [ ] Review automation effectiveness
- [ ] Clean up any duplicates
- [ ] Update field mappings if needed

### Monthly Optimization (1 hour)
- [ ] Performance analysis
- [ ] Identify improvement opportunities
- [ ] Update documentation
- [ ] Retrain team on best practices

## Resources & Next Steps

### Documentation Links
- [ColdSend API Docs](link)
- [HubSpot API Docs](link)
- [Salesforce API Docs](link)
- [Zapier ColdSend App](link)

### Support Channels
- ColdSend Support: support@coldsend.io
- Community Forum: [link]
- Status Page: status.coldsend.io

### Optional Enhancements
1. **Bidirectional Sync** - Sync CRM updates back to ColdSend
2. **Advanced Segmentation** - Dynamic lists based on CRM data
3. **Custom Reporting** - Unified dashboards across platforms
4. **AI-Powered Routing** - Smart lead assignment based on engagement

---
*Need help with a specific integration not covered here? Describe your use case and I'll provide custom guidance!*
```

## Supporting Files

This skill references:
- `templates/hubspot-setup.md` - Complete HubSpot integration guide
- `templates/salesforce-setup.md` - Complete Salesforce integration guide
- `examples/webhook-examples.py` - Sample webhook implementations
- `guides/api-reference.md` - ColdSend API reference documentation

Load these files from the skill directory when available.
