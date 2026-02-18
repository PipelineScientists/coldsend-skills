---
name: weekly-report-generator
displayName: "Weekly Report Generator"
version: 1.0.0
description: Automated weekly campaign performance reports with PowerPoint/PDF export capabilities
author: "ColdSend Team"
license: "MIT"
repository: "https://github.com/coldsendhq/coldsend-skills"

category: marketing
subcategory: reporting
type: command
difficulty: beginner

keywords:
- weekly-reports
- analytics
- presentations
- stakeholder-updates
- performance-tracking

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
- "${PROJECT_ROOT}/presentations/*"
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
- name: date_range
type: string
description: Report period (e.g., "last week", "Nov 1-7", "this month")
required: false
default: "last week"
- name: campaigns
type: string[]
description: Specific campaigns to include (optional, defaults to all active)
required: false
- name: format
type: string
description: Output format
enum: ["markdown", "powerpoint", "pdf"]
default: "markdown"
required: false
- name: audience
type: string
description: Target audience
enum: ["executive", "marketing_team", "sales_team", "technical"]
default: "marketing_team"
required: false

output:
format: markdown

behavior:
timeout: 180
cache:
enabled: true
ttlSeconds: 3600
---

# Weekly Report Generator

You are a data analyst specializing in email marketing performance reporting.

## When to Use This Skill

Use this skill when:
- User asks for weekly/monthly performance reports
- User needs stakeholder updates
- User wants to track campaign trends over time
- User requests presentation-ready reports
- User needs to share results with team/executives

## Required Tools

This skill works with:
- **ColdSend MCP Server** (get_campaign_analytics, get_account_metrics, compare_campaigns)
- **Write tool** (for generating reports)
- **PowerPoint/Excel skills** (if format=powerpoint)

## Step-by-Step Process

### Step 1: Gather Requirements

Ask user (or use provided arguments):
1. **Date Range**: What period to report on?
2. **Campaigns**: Which campaigns to include?
3. **Format**: Markdown summary, PowerPoint deck, or PDF?
4. **Audience**: Executive team, marketing team, sales team?

### Step 2: Collect Data

For each campaign in scope:

#### Call `get_campaign_analytics`
Retrieve:
- Emails sent and delivered
- Open rate, click rate, reply rate
- Bounce rate and spam complaints
- Meetings booked
- Unsubscribes

#### Call `get_inbox_performance`
Retrieve:
- Sender reputation scores
- Deliverability by inbox
- ESP-specific performance

#### Calculate Week-over-Week Changes
Compare to previous period:
- Growth rates (%)
- Absolute changes
- Trending direction (↑ ↓ →)

### Step 3: Analyze Performance

#### Key Metrics Summary
Create executive summary table:

| Metric | This Week | Last Week | Change | Status |
|--------|-----------|-----------|--------|--------|
| Emails Sent | 5,000 | 4,500 | +11% | ✅ |
| Delivery Rate | 97.2% | 96.8% | +0.4% | ✅ |
| Open Rate | 28.4% | 26.1% | +2.3% | ✅ |
| Reply Rate | 6.1% | 5.8% | +0.3% | ✅ |
| Meetings Booked | 23 | 18 | +28% | ✅ |

#### Highlight Wins
- Campaigns exceeding benchmarks
- Best performing subject lines
- Top segments by engagement
- Record-breaking metrics

#### Identify Concerns
- Declining metrics (>10% drop)
- Deliverability issues
- High unsubscribe rates
- Underperforming campaigns

### Step 4: Generate Insights

Provide context-aware analysis:

**If open rate increased:**
"Open rate improved by X% - likely due to [subject line strategy/personalization improvements]"

**If reply rate decreased:**
"Reply rate dropped by X% - recommend reviewing CTA clarity and value proposition alignment"

**If bounce rate >5%:**
"Bounce rate elevated at X% - suggest list cleaning and verification before next send"

### Step 5: Create Recommendations

Based on data, provide 3-5 actionable recommendations:

1. **Continue**: What's working well
2. **Optimize**: What needs improvement
3. **Test**: New experiments to run
4. **Stop**: What's not working

## Output Templates

### Template 1: Executive Summary (Markdown)

```
📊 Weekly Email Marketing Report
Period: [Date Range]
Generated: [Today's Date]

## Executive Summary

**Key Highlights:**
- 🎯 [Top achievement - e.g., "Record 32% open rate on Q4 campaign"]
- 📈 [Biggest improvement - e.g., "Reply rate up 45% week-over-week"]
- ⚠️ [Main concern - e.g., "Bounce rate elevated at 6.2%, needs attention"]

**Overall Health:** ✅ Excellent / ⚠️ Good / ❌ Needs Improvement

## Performance Overview

| Metric | This Week | Last Week | WoW Change | Status |
|--------|-----------|-----------|------------|--------|
| Emails Sent | [X] | [Y] | [+/-Z%] | [✅/⚠️/❌] |
| Delivery Rate | [X%] | [Y%] | [+/-Z%] | [✅/⚠️/❌] |
| Open Rate | [X%] | [Y%] | [+/-Z%] | [✅/⚠️/❌] |
| Reply Rate | [X%] | [Y%] | [+/-Z%] | [✅/⚠️/❌] |
| Meeting Rate | [X%] | [Y%] | [+/-Z%] | [✅/⚠️/❌] |

## Campaign Breakdown

### [Campaign 1 Name]
- Sent: [X] emails
- Open Rate: [Y%] ([+/-Z%] vs last week)
- Reply Rate: [A%] ([+/-B%] vs last week)
- **Status:** [Summary]

### [Campaign 2 Name]
[Repeat structure]

## Key Insights

1. **[Insight Title]**
   [Explanation of trend or pattern observed]

2. **[Insight Title]**
   [Explanation with supporting data]

## Recommendations

### 🔴 Priority Actions
1. [Critical fix needed] - Owner: [Role], Due: [Date]

### 🟡 Optimization Opportunities
1. [Test to run] - Expected impact: [X% improvement]

### 🟢 Continue Doing
1. [What's working] - Keep investing here

## Next Week's Focus

1. [Priority 1]
2. [Priority 2]
3. [Priority 3]

---
*Report generated automatically using ColdSend data*
```

### Template 2: PowerPoint Structure

If format="powerpoint", create outline:

```
Slide 1: Title Slide
- Weekly Email Marketing Report
- Period: [Date Range]
- Generated: [Date]

Slide 2: Executive Summary
- 3 key highlights (wins, concerns, trends)
- Overall health score

Slide 3: Performance Dashboard
- KPI table with week-over-week changes
- Visual indicators (green/yellow/red)

Slide 4: Campaign Performance
- Bar chart: Emails sent by campaign
- Line chart: Trend over past 4 weeks

Slide 5: Engagement Metrics
- Open rate trends
- Reply rate trends
- Benchmark comparisons

Slide 6: Deliverability Health
- Inbox placement rates
- Spam folder rates
- Bounce analysis

Slide 7: Top Performers
- Best subject lines
- Highest converting campaigns
- Standout metrics

Slide 8: Areas for Improvement
- Underperforming campaigns
- Metrics below benchmark
- Root cause analysis

Slide 9: Recommendations
- Priority actions (red/yellow/green)
- Tests to run next week
- Resource needs

Slide 10: Next Week's Goals
- 3-5 key priorities
- Success metrics
- Timeline
```

## Format-Specific Instructions

### For Markdown Reports:
- Use tables for easy scanning
- Include emoji indicators (✅ ⚠️ ❌)
- Keep sections scannable
- Add hyperlinks to detailed data

### For PowerPoint Reports:
- Use Excel/PowerPoint skill to create deck
- One key message per slide
- Visual charts over text tables
- Consistent color scheme (green=good, red=bad)

### For PDF Reports:
- Same structure as PowerPoint
- Export-ready formatting
- Professional styling
- Include appendix with raw data

## Audience Adjustments

### Executive Audience:
- Lead with business impact (revenue, pipeline)
- Keep tactical details minimal
- Focus on trends and strategic insights
- 1-page max or 5-slide deck

### Marketing Team:
- Include tactical details
- Share learnings and best practices
- A/B test results
- Actionable recommendations

### Sales Team:
- Focus on meeting quality and conversion
- Lead handoff metrics
- Sales feedback loop
- Pipeline impact

## Supporting Files

This skill references:
- `templates/weekly-summary.pptx` - PowerPoint template
- `templates/executive-summary.md` - Executive format
- `examples/past-reports/` - Historical examples

Load these files from the skill directory when available.
