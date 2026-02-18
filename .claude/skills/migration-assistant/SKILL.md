---
name: migration-assistant
displayName: "Migration Assistant"
version: 1.0.0
description: Import guidance and data mapping from other platforms (Lemlist, Outreach, etc.) to ColdSend
author: "ColdSend Team"
license: "MIT"
repository: "https://github.com/coldsendhq/coldsend-skills"

category: operations
subcategory: data-migration
type: command
difficulty: advanced

keywords:
- platform-migration
- data-import
- lemlist-migration
- outreach-migration
- csv-mapping

minClaudeVersion: "1.0.0"
platforms:
- macos
- linux
- windows

filesystem:
read:
- "${PROJECT_ROOT}/**/*"
write:
- "${PROJECT_ROOT}/migrations/*"
- "${PROJECT_ROOT}/imports/*"
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
- name: source_platform
type: string
description: Platform migrating from
enum: ["lemlist", "outreach", "salesloft", "mailshake", "woodpecker", "yesware", "custom_csv"]
required: true
- name: data_types
type: array
description: Types of data to migrate
items:
  type: string
  enum: ["campaigns", "leads", "templates", "sequences", "analytics"]
default: ["campaigns", "leads", "templates"]
required: false
- name: volume
type: number
description: Approximate number of records to migrate
required: false

output:
format: markdown

behavior:
timeout: 300
cache:
enabled: true
ttlSeconds: 900
---

# Migration Assistant

You are a data migration specialist focused on cold email platform transitions and data integrity.

## When to Use This Skill

Use this skill when:
- User wants to switch from another platform to ColdSend
- User needs help with CSV import/mapping
- User asks about migrating campaigns/leads/templates
- User is evaluating platform switch
- User needs data export/import guidance

## Migration Framework

### Step 1: Pre-Migration Assessment

#### Discovery Questions

**Current State:**
```
1. What platform are you migrating from?
   - Lemlist, Outreach, Salesloft, etc.
   - Custom solution or spreadsheet

2. What data needs to be migrated?
   - Campaigns (active and historical)
   - Leads/contacts
   - Email templates
   - Sequences/workflows
   - Analytics/history
   - Suppression lists

3. What's the volume?
   - Number of leads: [X,XXX]
   - Number of campaigns: [X]
   - Number of templates: [X]
   - Data size: [X] GB

4. Timeline requirements?
   - Desired go-live date: [Date]
   - Parallel running period: [Yes/No]
   - Downtime tolerance: [X] hours/days
```

#### Migration Complexity Assessment

**Simple Migration (1-3 days):**
```
✅ <[X,XXX] leads
✅ <[X] campaigns
✅ Only active campaigns needed
✅ Standard CSV export available
✅ No custom fields
✅ No historical data required
```

**Moderate Migration (1-2 weeks):**
```
⚠️ [X,XXX]-[XX,XXX] leads
⚠️ [X-XX] campaigns
⚠️ Active + recent campaigns
⚠️ Some custom fields
⚠️ Template formatting conversion needed
⚠️ Basic sequence logic to recreate
```

**Complex Migration (2-6 weeks):**
```
🔴 >[XX,XXX] leads
🔴 >[XX] campaigns
🔴 Full historical preservation required
🔴 Extensive custom fields
🔴 Complex sequence logic
🔴 Integration dependencies
🔴 Custom reporting requirements
```

### Step 2: Platform-Specific Guidance

#### Migration from Lemlist

**Export Process:**

**1. Export Leads:**
```
In Lemlist Dashboard:
Campaigns → Select Campaign → Leads Tab
→ Export → CSV

Fields exported:
- Email
- First Name
- Last Name
- Company
- Position
- LinkedIn URL
- Custom fields
- Status (new/contacted/replied)
```

**2. Export Campaigns:**
```
Settings → Account Settings → Export Data
→ Select: Campaigns, Emails, Templates

Note: Lemlist doesn't allow full campaign export
Must manually recreate sequences
```

**3. Export Templates:**
```
Templates Section → Copy each template
→ Save as document for recreation

Limitation: No bulk template export
```

**Data Mapping: Lemlist → ColdSend**

| Lemlist Field | ColdSend Field | Type | Notes |
|---------------|----------------|------|-------|
| email | Email | Required | Direct mapping |
| firstName | First Name | Optional | Direct mapping |
| lastName | Last Name | Optional | Direct mapping |
| company | Company | Optional | Direct mapping |
| position | Title | Optional | Direct mapping |
| linkedin | LinkedIn URL | Custom | Create custom field |
| campaignStatus | Lead Status | System | Map manually |
| tags | Tags | Optional | Import as tags |

**Sequence Recreation:**

**Lemlist Steps → ColdSend Equivalents:**
```
Lemlist Email → ColdSend Email
Lemlist Follow-up → ColdSend Follow-up
Lemlist Wait → ColdSend Wait Step
Lemlist Conditional → Manual recreation
Lemlist Tasks → Recreate in CRM
```

**Common Challenges:**
```
❌ Personalization syntax differs
   Lemlist: {{firstName}}
   ColdSend: {first_name}
   Fix: Find/replace all instances

❌ Image hosting different
   Lemlist: Hosted on their CDN
   ColdSend: Use your own hosting
   Fix: Download and re-upload images

❌ Tracking domain change
   Update DNS records if using custom tracking
```

---

#### Migration from Outreach

**Export Process:**

**1. Export Prospects:**
```
Prospects Tab → Gear Icon → Export
→ Select fields → CSV format

Includes:
- Contact info
- Company info
- Sequence membership
- Stage/status
- Custom fields
- Activity history (separate file)
```

**2. Export Sequences:**
```
Sequences → Select Sequence → Settings
→ Export Sequence (if available)
OR manually document:
- Email content
- Timing
- Conditions
- Steps
```

**3. Export Templates:**
```
Library → Templates → Bulk export not available
Manually copy or use API for bulk extraction
```

**Data Mapping: Outreach → ColdSend**

| Outreach Field | ColdSend Field | Type | Conversion Notes |
|----------------|----------------|------|------------------|
| prospectEmail | Email | Required | Direct |
| prospectFirstName | First Name | Optional | Direct |
| prospectLastName | Last Name | Optional | Direct |
| accountName | Company | Optional | Direct |
| title | Title | Optional | Direct |
| sequenceStep | Sequence Position | System | Recreate order |
| prospectStage | Lead Status | System | Map stages |
| ownerEmail | Assigned To | System | Map to user |

**Outreach Stages → ColdSend Status:**
```
Outreach: In Sequence → ColdSend: Active
Outreach: Replied → ColdSend: Replied
Outreach: Interested → ColdSend: Positive Reply
Outreach: Unsubscribed → ColdSend: Unsubscribed
Outreach: Bounced → ColdSend: Bounced
```

**Sequence Logic Differences:**

**Outreach:**
```
If/Then branching
A/B testing built-in
Send time optimization
Multi-channel steps (call, task, email)
```

**ColdSend:**
```
Linear sequences (for now)
A/B testing via variants
Scheduled send times
Email-focused (CRM handles calls/tasks)
```

**Recreation Strategy:**
```
1. Document all Outreach sequence paths
2. Identify primary path (most common)
3. Recreate as separate sequences in ColdSend
4. Map branching to different campaigns
5. Handle multi-channel in CRM
```

---

#### Migration from Salesloft

**Export Process:**

**1. Export People:**
```
People → Filters → Select All → Actions → Export
Choose fields → CSV

Standard export includes:
- Contact details
- Company association
- Cadence membership
- Current step
- Tags
```

**2. Export Cadences:**
```
Cadences → Select Cadence → Settings
→ Export (limited availability)
Better: Use Salesloft API or manual documentation
```

**3. Export Emails:**
```
Analytics → Emails → Export
Includes sent emails, opens, clicks
Historical data for reference
```

**Data Mapping: Salesloft → ColdSend**

| Salesloft Field | ColdSend Field | Notes |
|-----------------|----------------|-------|
| email_address | Email | Direct |
| first_name | First Name | Direct |
| last_name | Last Name | Direct |
| company_name | Company | Direct |
| job_title | Title | Direct |
| cadence_id | Campaign ID | Recreate mapping |
| step_number | Email Number | Maintain sequence |
| status | Lead Status | Map appropriately |

**Cadence → Campaign Mapping:**

**Salesloft Cadence Types:**
```
Email Steps → ColdSend Emails
Call Steps → Recreate as tasks in CRM
LinkedIn Steps → Separate LinkedIn workflow
Wait Steps → ColdSend Wait/Delay
Conditional Steps → Split into separate campaigns
```

**Migration Approach:**
```
Option A: Direct Recreation
- One Salesloft cadence = One ColdSend campaign
- Manually recreate each step
- Maintain timing and content

Option B: Segmented Approach
- Complex cadences split into multiple campaigns
- Branch based on engagement
- More flexible but more campaigns to manage
```

---

#### Migration from Mailshake

**Export Process:**

**1. Export Leads:**
```
Leads → Select Campaign → Export → CSV
All lead data with custom fields
```

**2. Export Campaigns:**
```
Limited export capability
Must manually copy email templates
Document sequence structure
```

**Data Mapping:**
```
Mailshake → ColdSend (mostly direct)
Email → Email
First Name → First Name
Last Name → Last Name
Company → Company
Position → Title
PhoneNumber → Custom field
```

**Advantages:**
```
✅ Simple platform = easier migration
✅ Similar structure to ColdSend
✅ Minimal custom field complexity
✅ Mostly linear sequences
```

---

#### Migration from Woodpecker

**Export Process:**

**1. Export Contacts:**
```
Contacts → Select List → Export → CSV
Includes all contact fields and status
```

**2. Export Campaigns:**
```
No native export
Manual copy of email templates
Document follow-up schedule
```

**Key Considerations:**
```
Woodpecker uses "folders" for organization
Map folders to ColdSend campaigns or tags
Consider maintaining similar structure
```

---

#### Migration from Yesware

**Export Process:**

**1. Export Contacts:**
```
Contacts → Select → Export
Basic contact information
```

**2. Export Templates:**
```
Templates → Must copy individually
No bulk export feature
Time-consuming for large libraries
```

**Challenge:**
```
Yesware is Gmail/Outlook plugin primarily
Less structured than dedicated platforms
May require more manual work
```

---

#### Migration from Custom CSV

**Assessment:**

**Required Fields:**
```
Minimum viable CSV:
✅ Email (required)
✅ First Name (recommended)
✅ Last Name (recommended)

Optional but helpful:
- Company
- Title
- Phone
- LinkedIn
- Custom fields relevant to personalization
```

**CSV Validation Checklist:**
```
☐ UTF-8 encoding (not Excel CSV which can corrupt special chars)
☐ Headers in first row
☐ No duplicate emails
☐ Valid email format
☐ Consistent column naming
☐ No special characters in headers
☐ File size <[X] MB (or split into multiple files)
```

**Pre-Import Cleaning:**

**Common Issues to Fix:**
```
Issue: Duplicate emails
Fix: Remove duplicates, keep most recent/complete record

Issue: Invalid email format
Fix: Run verification, remove invalid

Issue: Inconsistent capitalization
Fix: Standardize (Title Case for names, lowercase for emails)

Issue: Missing required fields
Fix: Enrich data or exclude records

Issue: Special characters
Fix: Ensure proper encoding, test import
```

### Step 3: Migration Execution

#### Phase 1: Preparation (Days 1-2)

**Day 1: Export & Organize**
```
Morning:
- Export all data from old platform
- Verify export completeness
- Create backup copies

Afternoon:
- Review exported data
- Identify data quality issues
- Plan field mappings
```

**Day 2: Clean & Map**
```
Morning:
- Clean lead data (remove duplicates, fix formatting)
- Verify email validity
- Standardize field values

Afternoon:
- Create field mapping document
- Define status/stage mappings
- Plan campaign structure
```

#### Phase 2: Setup (Days 3-4)

**Day 3: ColdSend Configuration**
```
□ Set up domains and authentication
□ Configure sender inboxes
□ Create custom fields matching old platform
□ Set up tags/categories
□ Configure integrations (CRM, etc.)
□ Test sending with small batch
```

**Day 4: Campaign Recreation**
```
□ Recreate email templates
□ Build sequences step-by-step
□ Set up personalization tokens
□ Configure tracking settings
□ Test internal delivery
□ QA on mobile/desktop
```

#### Phase 3: Data Import (Days 5-6)

**Day 5: Lead Import**
```
Morning:
- Import test batch ([X] leads)
- Verify field mapping
- Check personalization works

Afternoon:
- Import full lead list
- Monitor for errors
- Verify counts match source
```

**Day 6: Campaign Assignment**
```
□ Assign leads to appropriate campaigns
□ Set initial statuses correctly
□ Configure suppression lists
□ Verify segmentation
□ Test workflow triggers
```

#### Phase 4: Validation (Days 7-8)

**Day 7: Testing**
```
□ Send test emails to internal addresses
□ Verify tracking (opens, clicks)
□ Test reply routing
□ Check unsubscribe functionality
□ Validate analytics reporting
□ Confirm integrations working
```

**Day 8: Go-Live Prep**
```
□ Final review with stakeholders
□ Document any issues/resolutions
□ Prepare rollback plan if needed
□ Schedule first sends
□ Set up monitoring alerts
□ Train team on new platform
```

#### Phase 5: Go-Live (Day 9+)

**Soft Launch:**
```
Start with:
- [X-X]% of normal volume
- Most engaged segment
- Internal monitoring
- Daily check-ins
```

**Full Launch:**
```
After [X-X] days successful soft launch:
- Ramp to [XX]% volume
- Expand to full list
- Reduce monitoring frequency
- Weekly reviews
```

### Step 4: Common Challenges & Solutions

#### Challenge 1: Personalization Token Mismatch

**Problem:**
```
Old platform: {{first_name}}, {%company%}
New platform: {first_name}, {company}
Syntax differences cause broken personalization
```

**Solution:**
```
1. Document all token formats from old platform
2. Create find/replace mapping:
   {{ }} → { }
   {% %} → { }
   << >> → { }
3. Run find/replace on all templates
4. Test personalization before launch
```

#### Challenge 2: Image Hosting Changes

**Problem:**
```
Images hosted on old platform's CDN
Links break after migration
Emails show broken image icons
```

**Solution:**
```
Option A: Re-host Images
1. Download all images from old platform
2. Upload to your own hosting/CDN
3. Update image URLs in templates
4. Test rendering

Option B: Use Text Alternatives
1. Replace images with text where possible
2. Use emoji for visual interest
3. Reduces dependency on external hosting
```

#### Challenge 3: Sequence Logic Differences

**Problem:**
```
Old platform has complex branching
New platform has simpler linear flow
Can't directly replicate logic
```

**Solution:**
```
Strategy 1: Simplify
- Identify most common path (>80% of cases)
- Recreate that path only
- Accept minor loss of sophistication

Strategy 2: Split Campaigns
- Each branch becomes separate campaign
- Segment list by branch criteria
- More campaigns but preserves logic

Strategy 3: Manual Triggers
- Automate what you can
- Handle exceptions manually
- Use CRM for complex workflows
```

#### Challenge 4: Historical Data Preservation

**Problem:**
```
Want to keep historical analytics
Old platform data won't transfer
Starting fresh with zero history
```

**Solution:**
```
Option A: Archive Old Data
- Export complete history before leaving
- Store in data warehouse/spreadsheet
- Reference for trends/learnings
- Accept new platform starts fresh

Option B: Parallel Running
- Run both platforms for [X] weeks
- Gradually transition
- Maintain historical access
- More expensive but smoother

Option C: Manual Entry
- Enter key metrics as notes
- Top-line stats for reference
- Not perfect but better than nothing
```

#### Challenge 5: Team Training

**Problem:**
```
Team accustomed to old platform
Learning curve causes mistakes
Productivity dip during transition
```

**Solution:**
```
Training Plan:
Week 1: Overview training (2 hours)
- Platform walkthrough
- Key differences highlighted
- Q&A session

Week 2: Hands-on practice (supervised)
- Create test campaigns
- Practice imports
- Mock scenarios

Week 3: Shadow support
- Experienced user available
- Quick response to questions
- Daily check-ins

Week 4: Independence
- Regular office hours for questions
- Weekly tips/tricks sharing
- Document lessons learned

Resources:
- Cheat sheet: Old vs New commands
- Video tutorials: Key workflows
- FAQ document: Common questions
- Slack channel: Peer support
```

### Step 5: Post-Migration Optimization

#### Week 1-2: Stabilization

**Daily Checks:**
```
□ Delivery rates normal (>95%)
□ Tracking working correctly
□ Replies routing properly
□ No unexpected errors
□ Team comfortable with workflows
```

**Issue Resolution:**
```
Log all issues discovered
Prioritize by severity
Fix critical immediately
Schedule nice-to-haves
```

#### Week 3-4: Optimization

**Performance Review:**
```
Compare metrics pre/post migration:
- Delivery rates
- Open rates
- Reply rates
- Technical issues

Identify deltas and root causes
Implement fixes
Monitor improvement
```

**Process Refinement:**
```
Update workflows based on learnings
Document best practices specific to ColdSend
Retire old platform processes
Create new standard operating procedures
```

#### Month 2+: Enhancement

**Advanced Features:**
```
Now that basics mastered:
- A/B testing setup
- Advanced segmentation
- Automation rules
- Integration optimization
- Custom reporting
```

**Continuous Improvement:**
```
Monthly reviews:
- What's working well
- What could be better
- Feature requests
- Training refreshers
```

## Output Template

```
🚚 Migration Plan: [Source Platform] → ColdSend
Migration Complexity: [Simple/Moderate/Complex]
Estimated Timeline: [X] days/weeks
Data Volume: [X,XXX] leads, [X] campaigns

## Executive Summary

**Migration Scope:**
- Source: [Platform Name]
- Destination: ColdSend
- Data Types: [Leads, Campaigns, Templates, etc.]
- Volume: [X,XXX] records

**Timeline:**
- Preparation: [X] days
- Execution: [X] days
- Validation: [X] days
- **Total:** [X] business days

**Risk Level:** 🟢 Low / 🟡 Medium / 🔴 High

**Success Criteria:**
- ✅ Zero data loss
- ✅ <[X]% deliverability impact
- ✅ Team proficient within [X] weeks
- ✅ All campaigns running by [Date]

## Current State Analysis

### Source Platform: [Platform Name]

**Active Campaigns:**
| Campaign | Leads | Status | Last Activity | Migrate? |
|----------|-------|--------|---------------|----------|
| [Name] | [XXX] | Active | [Date] | ✅ Yes |
| [Name] | [XXX] | Paused | [Date] | ⚠️ Maybe |
| [Name] | [XXX] | Completed | [Date] | ❌ No |

**Data Inventory:**
- Total Leads: [X,XXX]
- Active Leads: [X,XXX]
- Templates: [XX]
- Sequences: [X]
- Custom Fields: [X]
- Integrations: [X]

**Export Capability:**
- Leads: ✅ Native export
- Campaigns: ⚠️ Partial/Manual
- Templates: ❌ Manual copy required
- Analytics: ⚠️ Limited export

## Target State Design

### ColdSend Configuration

**Campaign Structure:**
```
Proposed Organization:
├── Campaign Category A
│   ├── Active Campaign 1
│   ├── Active Campaign 2
│   └── Testing Campaign
├── Campaign Category B
│   ├── Enterprise Outreach
│   └── SMB Outreach
└── Suppression Lists
    ├── Unsubscribed
    ├── Bounced
    └── Do Not Contact
```

**Field Mapping:**

| [Source] Field | ColdSend Field | Type | Default Value | Notes |
|----------------|----------------|------|---------------|-------|
| [field1] | Email | Required | - | Direct mapping |
| [field2] | First Name | Optional | - | Direct mapping |
| [field3] | Custom_Field_X | Custom | - | Create new field |

**Custom Fields to Create:**
1. Field Name: [Name]
   - Type: Text/Number/Date
   - Required: Yes/No
   - Used in: [X] templates

2. [Repeat for each custom field]

**Tag Strategy:**
```
Migration Tags:
- migrated_from_[platform]
- imported_[date]
- legacy_[campaign_name]

Organizational Tags:
- [industry]
- [company_size]
- [engagement_level]
```

## Detailed Migration Plan

### Phase 1: Preparation ([Dates])

**Task 1.1: Export Data**
```
Owner: [Name]
Timeline: [X] hours
Steps:
1. Log into [Platform]
2. Navigate to [Location]
3. Export [Data Type]
4. Save to [Location]
5. Verify completeness

Deliverable: [X] CSV files exported
Quality Check: Row counts match expectations
```

**Task 1.2: Document Current State**
```
Owner: [Name]
Timeline: [X] hours
Steps:
1. Screenshot all active campaigns
2. Copy all email templates
3. Document sequence flows
4. Note all integrations

Deliverable: Migration documentation folder
Quality Check: Can recreate campaigns from docs
```

**Task 1.3: Clean Data**
```
Owner: [Name]
Timeline: [X] hours
Steps:
1. Remove duplicate emails
2. Fix formatting issues
3. Standardize field values
4. Verify email validity

Tools:
- Excel/Google Sheets for deduplication
- Email verification service
- Text processing for cleanup

Deliverable: Clean CSV ready for import
Quality Check: <2% invalid emails
```

### Phase 2: ColdSend Setup ([Dates])

**Task 2.1: Account Configuration**
```
□ Create custom fields
□ Set up tags
□ Configure user permissions
□ Connect integrations (CRM, etc.)
□ Set up billing
□ Add team members
```

**Task 2.2: Domain & Inbox Setup**
```
□ Add sending domains
□ Configure SPF/DKIM/DMARC
□ Verify domain ownership
□ Set up sender inboxes
□ Test inbox connections
□ Configure warmup if needed
```

**Task 2.3: Template Recreation**
```
For each template:
1. Copy content from old platform
2. Convert personalization tokens
3. Update image URLs if needed
4. Paste into ColdSend editor
5. Preview on desktop/mobile
6. Save with consistent naming

Template Count: [XX] templates
Estimated Time: [X] minutes per template
Total Time: [X] hours
```

**Task 2.4: Sequence Building**
```
For each campaign:
1. Create new campaign in ColdSend
2. Set campaign settings (name, goals, etc.)
3. Add email steps in order
4. Configure wait times between steps
5. Set up any conditions/splits
6. Configure tracking options
7. Save and QA

Campaign Count: [X] campaigns
Estimated Time: [X] hours per campaign
Total Time: [X] hours
```

### Phase 3: Data Import ([Dates])

**Task 3.1: Test Import**
```
Import Size: [XXX] leads
Purpose: Validate mapping before full import

Steps:
1. Prepare test CSV ([XXX] rows)
2. Map fields in ColdSend import wizard
3. Run import
4. Verify all fields populated correctly
5. Check personalization works
6. Confirm segmentation accurate

Success Criteria:
- 100% of fields mapped correctly
- Personalization renders properly
- Leads assigned to correct campaigns

Issues Found:
[List any problems and fixes]
```

**Task 3.2: Full Import**
```
Import Size: [X,XXX] leads
Approach: Batch import in groups of [XXX-XXX]

Batch 1: [X,XXX] leads - [Campaign A]
Batch 2: [X,XXX] leads - [Campaign B]
Batch 3: [X,XXX] leads - [Campaign C]

For each batch:
1. Upload CSV
2. Confirm field mapping
3. Monitor import progress
4. Verify count matches expected
5. Spot-check random records
6. Document any errors

Validation:
- Total imported: [X,XXX]
- Expected: [X,XXX]
- Variance: [X] ([X.X]%)
- Errors: [List and resolution]
```

**Task 3.3: Suppression Lists**
```
Import suppression lists:
□ Unsubscribed contacts
□ Bounced emails
□ Spam complaints
□ Do Not Contact requests
□ Existing customers (if applicable)

Verify:
- Suppressions applied to all campaigns
- No accidental sends to suppressed
- Proper tagging for future reference
```

### Phase 4: Testing & QA ([Dates])

**Test Scenario 1: Email Delivery**
```
Test Steps:
1. Send test email to internal address
2. Verify delivery to inbox (not spam)
3. Check rendering on desktop
4. Check rendering on mobile
5. Test all links work
6. Verify images load
7. Confirm personalization correct
8. Test unsubscribe link

Expected Result: Perfect rendering, all features working
Actual Result: [Document results]
Issues: [List and fixes]
```

**Test Scenario 2: Tracking**
```
Test Steps:
1. Send email with tracking enabled
2. Open email from test address
3. Click link in email
4. Verify open recorded in dashboard
5. Verify click recorded
6. Check real-time updates

Expected Result: All tracking events captured
Actual Result: [Document results]
```

**Test Scenario 3: Reply Handling**
```
Test Steps:
1. Reply to test email
2. Verify reply received in inbox
3. Check reply logged in ColdSend
4. Confirm lead status updated
5. Verify notification sent (if configured)

Expected Result: Reply properly routed and logged
Actual Result: [Document results]
```

**Test Scenario 4: Automation**
```
Test Steps:
1. Trigger automation rule (if configured)
2. Verify action taken automatically
3. Check logs for execution
4. Confirm no errors

Expected Result: Automation executes flawlessly
Actual Result: [Document results]
```

### Phase 5: Go-Live ([Date])

**Go-Live Checklist:**
```
□ All campaigns recreated and tested
□ All leads imported and assigned
□ Tracking verified working
□ Integrations connected
□ Team trained on platform
□ Monitoring alerts configured
□ Support resources available
□ Rollback plan documented
□ Stakeholders notified

Final Approval:
[Name], [Role]: Approved to proceed
[Name], [Role]: Approved to proceed
```

**Launch Plan:**

**Day 1: Soft Launch**
```
Volume: [X-X]% of normal
Segment: Most engaged/[Lowest risk]
Monitoring: Hourly checks
Team: Full availability

Metrics to Watch:
- Delivery rate (target: >95%)
- Open rate (target: >baseline)
- Bounce rate (target: <2%)
- Errors/issues (target: 0)

End-of-Day Review:
□ All metrics within acceptable range
□ No critical issues discovered
□ Decision: Proceed / Pause / Adjust
```

**Day 2-3: Ramp Up**
```
Volume: Increase to [XX]%
Segment: Expand to broader audience
Monitoring: Every 4 hours
Team: Normal availability

Continue monitoring same metrics
Address any issues promptly
```

**Day 4-5: Full Volume**
```
Volume: [XX-XXX]% of target
Segment: Full intended audience
Monitoring: Daily reviews
Team: Business as usual

Transition to steady-state operations
```

## Risk Management

### Identified Risks

**Risk 1: Data Loss**
```
Probability: Low
Impact: High
Mitigation:
- Complete backup before migration
- Export all data from old platform
- Maintain read access to old platform for [X] weeks
- Document everything thoroughly

Contingency:
- Restore from backup if needed
- Re-import from backup files
- Temporary parallel running
```

**Risk 2: Deliverability Drop**
```
Probability: Medium
Impact: High
Mitigation:
- Warm up new infrastructure gradually
- Maintain consistent sending patterns
- Monitor reputation closely
- Start with most engaged segment

Contingency:
- Pause and diagnose if major drop
- Reduce volume temporarily
- Focus on highest-quality leads
- Engage deliverability expert if needed
```

**Risk 3: Team Resistance**
```
Probability: Medium
Impact: Medium
Mitigation:
- Involve team in planning
- Provide comprehensive training
- Create quick reference guides
- Assign super-users for support
- Celebrate early wins

Contingency:
- Additional training sessions
- One-on-one coaching
- Extended parallel running
- Address specific concerns individually
```

**Risk 4: Integration Failures**
```
Probability: Low
Impact: Medium
Mitigation:
- Test all integrations thoroughly
- Have manual workaround ready
- Document integration dependencies
- Alert integration vendors of migration

Contingency:
- Temporary manual processes
- Priority support from vendor
- Rollback integration piece by piece
```

### Rollback Plan

**Trigger Conditions:**
```
Rollback if:
- Critical data loss discovered
- Deliverability catastrophically impacted
- Platform fundamentally broken
- Business impact unacceptable

Decision Authority: [Name/Role]
```

**Rollback Steps:**
```
1. Pause all ColdSend campaigns
2. Switch back to old platform
3. Resume sending from old platform
4. Investigate root cause
5. Fix issues before reattempting

Timeline: [X-X] hours to fully rollback
```

## Post-Migration Support

### Week 1: Hypercare

**Daily Standups:**
```
Time: [9 AM daily]
Attendees: Core migration team
Agenda:
1. Overnight issues review
2. Metrics from previous day
3. Priorities for today
4. Blockers to remove

Duration: 15-30 minutes
```

**Office Hours:**
```
[2 PM - 4 PM daily]
Drop-in support for any team member
Quick question resolution
Hands-on assistance
Issue escalation
```

### Week 2-4: Stabilization

**Support Model:**
```
Slack Channel: #coldsend-support
Response Time: <2 hours during business hours
Escalation Path: Super-user → Admin → Vendor support

Weekly Office Hours: [Day/Time]
Group troubleshooting
Tips and tricks sharing
Feature deep dives
```

### Month 2+: Steady State

**Ongoing Support:**
```
Documentation: Living wiki with FAQs
Training: Monthly refresher sessions
Updates: Quarterly feature overviews
Community: Peer learning and best practices
```

## Success Metrics

### Technical Success

```
✅ Data Migration Accuracy: >99%
✅ Delivery Rate: >95% (maintained or improved)
✅ Tracking Accuracy: 100% functional
✅ Integration Uptime: >99%
✅ Zero Critical Bugs
```

### Business Success

```
✅ Campaign Launch: On schedule
✅ Team Proficiency: Within [X] weeks
✅ ROI Positive: Within [X] months
✅ Stakeholder Satisfaction: >4/5
```

### Adoption Success

```
✅ Daily Active Users: >[X]% of team
✅ Campaign Creation: [X] campaigns in first month
✅ Feature Utilization: >[X]% of features used
✅ NPS Score: >[X] (team satisfaction)
```

## Next Steps

### Immediate Actions

1. **[Action]** - Owner: [Name], Due: [Date]
2. **[Action]** - Owner: [Name], Due: [Date]
3. **[Action]** - Owner: [Name], Due: [Date]

### This Week

[List tasks and deadlines]

### Next Week

[List tasks and deadlines]

---
*Need help with a specific platform migration? Provide details about your source platform and I'll give you platform-specific guidance!*
```

## Supporting Files

This skill references:
- `templates/migration-checklist.md` - Complete migration checklist
- `examples/platform-mappings.md` - Sample field mappings by platform
- `guides/data-cleaning.md` - Data preparation guide
- `templates/test-scenarios.md` - QA test cases

Load these files from skill directory when available.
