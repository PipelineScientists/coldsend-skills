---
name: campaign-audit
displayName: "Campaign Performance Audit"
version: 1.0.0
description: Comprehensive campaign performance analysis with health scoring, benchmarking, and optimization recommendations
author: "ColdSend Team"
license: "MIT"
repository: "https://github.com/coldsendhq/coldsend-skills"

category: marketing
subcategory: email-campaigns
type: command
difficulty: intermediate

keywords:
- campaign-analysis
- performance
- analytics
- optimization
- email-marketing

minClaudeVersion: "1.0.0"
platforms:
- macos
- linux
- windows

filesystem:
read:
- "${PROJECT_ROOT}/**/*"
write:
- "${PROJECT_ROOT}/reports/*"
deny:
- "**/.env*"
- "**/*.key"
- "**/*.pem"

tools:
allowed:
- Read
- Write
- Bash
denied: []

input:
arguments:
- name: campaign_name_or_id
type: string
description: Campaign to audit (optional, will ask if not provided)
required: false
- name: depth
type: string
description: Analysis depth
enum: ["quick", "standard", "deep"]
default: "standard"
required: false

output:
format: markdown

behavior:
timeout: 300
cache:
enabled: true
ttlSeconds: 600
---

# Campaign Performance Audit

You are now performing a comprehensive campaign audit for ColdSend email campaigns.

## When to Use This Skill

Use this skill when:
- User asks to analyze campaign performance
- User wants optimization recommendations
- User requests campaign health check
- User needs performance reports
- User asks "how is my campaign doing?"

## Required Tools

This skill works with:
- **ColdSend MCP Server** (for API calls: get_campaign_analytics, get_inbox_performance, list_leads)
- **Write tool** (for generating reports)
- **Read tool** (for reviewing templates)

## Step-by-Step Process

### Phase 1: Data Collection

#### Step 1.1: Get Campaign Overview
If user hasn't specified a campaign, ask them which campaign they want to audit.

Call `get_campaign_analytics` with the campaign ID to retrieve:
- Delivery metrics (sent, delivered, bounced)
- Engagement metrics (opens, clicks, replies)
- Conversion metrics (meetings booked, deals closed)
- Timeline data (daily performance trends)

#### Step 1.2: Analyze Inbox Performance
Call `get_inbox_performance` for each sender account used in the campaign:
- Sender reputation scores
- Deliverability rates per inbox
- Bounce reasons and patterns
- ESP blocking indicators

#### Step 1.3: Review Lead Quality
Call `list_leads` with statistics to understand:
- Lead source distribution
- Industry/company size breakdown
- Geographic distribution
- Engagement by segment

### Phase 2: Analysis Framework

#### Deliverability Assessment (Weight: 40%)
✅ Excellent: >95% delivery rate
⚠️ Good: 90-95% delivery rate  
❌ Poor: <90% delivery rate

**Red Flags:**
- Bounce rate >5% indicates list quality issues
- Spam complaints >0.1% requires immediate attention
- ESP-specific blocks (Google, Microsoft) need warmup adjustment

#### Engagement Assessment (Weight: 35%)
**Industry Benchmarks:**
- Open Rate: 20-25% average, >30% excellent
- Click Rate: 2-4% average, >5% excellent
- Reply Rate: 3-5% average, >8% excellent

**Analysis Steps:**
1. Compare against industry benchmarks
2. Identify top/bottom performing segments
3. Analyze subject line patterns in high-open campaigns
4. Review email copy in high-reply campaigns

#### ROI Assessment (Weight: 25%)
Calculate:
- Cost per lead (total spend / leads generated)
- Meeting rate (replies → meetings conversion)
- Pipeline generated (meetings → opportunities)

### Phase 3: Generate Recommendations

Structure recommendations using this format:

### 🔴 Critical Issues (Fix Immediately)
[List any deliverability crises or compliance risks]

### 🟡 Optimization Opportunities (This Week)
[A/B tests to run, segments to adjust]

### 🟢 Strategic Improvements (This Month)
[Long-term plays, infrastructure changes]

### Phase 4: Create Action Plan

For each recommendation, provide:
1. **Specific Action**: What to do exactly
2. **Expected Impact**: Quantified improvement
3. **Effort Level**: Low/Medium/High
4. **Timeline**: When to implement

## Output Template

Present findings in this structure:

```
📊 Campaign Audit: [Campaign Name]
Period: [Date Range]
Overall Health Score: [X/100]

## Executive Summary
[2-3 paragraph overview of key findings and recommendations]

## Key Metrics
| Metric | Value | Benchmark | Status |
|--------|-------|-----------|--------|
| Delivery Rate | 97.2% | 95% | ✅ |
| Open Rate | 28.4% | 22% | ✅ |
| Reply Rate | 6.1% | 4% | ✅ |
| Meeting Rate | 1.2% | 1% | ✅ |

## Deep Dive Analysis

### Deliverability
[Detailed deliverability breakdown by inbox and ESP]

### Engagement
[Performance by segment, subject line analysis]

### ROI
[Cost analysis and pipeline generation]

## Recommendations

### 🔴 Critical Issues
1. [Issue] - [Action required]

### 🟡 Optimization Opportunities
1. [Opportunity] - [Expected impact]

### 🟢 Strategic Improvements
1. [Improvement] - [Timeline]

## Next Steps
1. [Specific task 1] - Due: [Date]
2. [Specific task 2] - Due: [Date]
3. [Specific task 3] - Due: [Date]
```

## Important Notes

- Always ask clarifying questions if data is unclear
- Provide context-aware advice (B2B vs B2C differ significantly)
- Flag compliance concerns immediately (CAN-SPAM, GDPR)
- Suggest follow-up audits in 2-4 weeks to track improvements
- If depth="quick", focus only on top-level metrics and 1-2 key recommendations
- If depth="deep", include segment analysis, A/B test recommendations, and detailed competitive benchmarking

## Supporting Files

This skill can reference:
- `templates/audit-report.md` - Detailed report template
- `checklists/deliverability.md` - Deliverability checklist
- `examples/sample-audit.md` - Example audit output

Load these files from the skill directory when generating comprehensive reports.
