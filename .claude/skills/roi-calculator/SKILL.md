---
name: roi-calculator
displayName: "ROI Calculator & Revenue Attribution"
version: 1.0.0
description: Calculate campaign ROI, cost per lead, meeting conversion rates, and pipeline revenue attribution
author: "ColdSend Team"
license: "MIT"
repository: "https://github.com/coldsendhq/coldsend-skills"

category: marketing
subcategory: analytics
type: command
difficulty: intermediate

keywords:
- roi-calculation
- revenue-attribution
- cost-per-lead
- pipeline-tracking
- conversion-metrics

minClaudeVersion: "1.0.0"
platforms:
- macos
- linux
- windows

filesystem:
read:
- "${PROJECT_ROOT}/**/*"
write:
- "${PROJECT_ROOT}/analytics/*"
- "${PROJECT_ROOT}/revenue/*"
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
- name: campaign_name_or_id
type: string
description: Campaign to analyze (optional, defaults to all active campaigns)
required: false
- name: date_range
type: string
description: Analysis period (e.g., "last 30 days", "Q4 2025")
required: false
default: "last 30 days"
- name: include_pipeline
type: boolean
description: Include pipeline/revenue metrics if available
required: false
default: true
- name: currency
type: string
description: Currency for financial calculations
default: "USD"
required: false

output:
format: markdown

behavior:
timeout: 180
cache:
enabled: true
ttlSeconds: 600
---

# ROI Calculator & Revenue Attribution

You are a marketing analyst specializing in cold email campaign profitability and revenue attribution.

## When to Use This Skill

Use this skill when:
- User asks to calculate campaign ROI
- User wants to know cost per lead/meeting
- User requests revenue attribution analysis
- User needs to justify cold email investment
- User asks "is this campaign profitable?"

## Calculation Framework

### Step 1: Gather Required Data

#### Call `get_campaign_analytics`
Retrieve:
- Emails sent
- Delivery rate
- Open rate, click rate, reply rate
- Meetings booked
- Unsubscribes

#### Call `get_account_metrics`
Retrieve:
- Credit usage
- Cost breakdown
- Account-level aggregations

#### Ask User for Additional Inputs
If not available via API:
- **Cost per credit** (from ColdSend pricing)
- **Average deal value** (from user's CRM/sales data)
- **Close rate** (meeting → customer conversion)
- **Time investment** (hours spent on campaign management)
- **Additional costs** (data enrichment, tools, freelancers)

### Step 2: Calculate Core Metrics

#### Cost Metrics

**Total Campaign Cost:**
```
Total Cost = (Credits Used × Cost per Credit) + Time Cost + Additional Costs

Where:
- Credits Used = Total emails sent
- Cost per Credit = $X.XX (from pricing plan)
- Time Cost = Hours Spent × Hourly Rate
- Additional Costs = Data, tools, services
```

**Cost Per Lead:**
```
CPL = Total Cost / Number of Qualified Leads

Where:
- Qualified Leads = Leads that responded positively
```

**Cost Per Meeting:**
```
CPM = Total Cost / Meetings Booked
```

**Cost Per Customer:**
```
CPC = Total Cost / Customers Acquired

Where:
- Customers Acquired = Meetings × Close Rate
```

#### Revenue Metrics

**Pipeline Generated:**
```
Pipeline Value = Meetings Booked × Average Deal Value × Close Rate
```

**Revenue Attributed:**
```
Actual Revenue = Customers Acquired × Average Deal Value
```

**ROI Calculation:**
```
ROI (%) = [(Revenue - Cost) / Cost] × 100

Example:
- Revenue: $50,000
- Cost: $5,000
- ROI = [($50,000 - $5,000) / $5,000] × 100 = 900%
```

**ROAS (Return on Ad Spend):**
```
ROAS = Revenue / Cost

Example:
- Revenue: $50,000
- Cost: $5,000
- ROAS = 10x
```

#### Efficiency Metrics

**Lead-to-Meeting Rate:**
```
Meeting Rate = (Meetings Booked / Qualified Replies) × 100
```

**Meeting-to-Customer Rate:**
```
Close Rate = (Customers / Meetings) × 100
```

**Break-Even Point:**
```
Break-Even Customers = Total Cost / Average Deal Value

Example:
- Total Cost: $5,000
- Avg Deal Value: $10,000
- Break-Even: 0.5 customers (need 1 customer to profit)
```

**Payback Period:**
```
Days to Break-Even = (Total Cost / Daily Revenue) 

Where:
- Daily Revenue = (Daily Meetings × Close Rate × Avg Deal Value)
```

### Step 3: Benchmarking

#### Industry Benchmarks (B2B Cold Email)

**Cost Metrics:**
- Cost Per Lead: $50-$500 (varies by industry)
- Cost Per Meeting: $200-$2,000
- Cost Per Customer: $1,000-$10,000

**Performance Metrics:**
- Reply Rate: 3-8%
- Meeting Rate: 1-3% (of total sends)
- Close Rate: 20-40% (of meetings)

**ROI Expectations:**
- Break-even: 1-2 customers
- Good ROI: 300-500%
- Excellent ROI: 500-1000%+

### Step 4: Scenario Analysis

#### Best Case / Worst Case / Most Likely

**Most Likely (Base Case):**
- Uses actual performance metrics
- Conservative close rate estimates
- Realistic timeline

**Best Case:**
- Top quartile performance
- Higher close rates
- Faster sales cycle

**Worst Case:**
- Bottom quartile performance
- Lower close rates
- Extended sales cycle

**Sensitivity Analysis:**
Show how changes impact ROI:
- If close rate drops from 30% to 20%
- If deal value decreases by 25%
- If reply rate improves from 5% to 8%

### Step 5: Recommendations

Based on ROI analysis, provide actionable guidance:

#### If ROI > 500% (Excellent):
✅ **Scale Up**
- Increase sending volume
- Expand to additional segments
- Invest in more inboxes
- Test higher price points

#### If ROI 100-500% (Good):
🟡 **Optimize**
- Improve reply rates with better copy
- Enhance lead qualification
- Refine ICP targeting
- A/B test subject lines and CTAs

#### If ROI < 100% (Needs Improvement):
🔴 **Pivot or Pause**
- Review ICP alignment
- Overhaul email copy
- Reconsider offer/pricing
- Focus on higher-value segments

## Output Template

```
💰 ROI Analysis Report
Campaign: [Campaign Name]
Period: [Date Range]
Generated: [Date]

## Executive Summary

**Total Investment:** $[X,XXX]
**Revenue Attributed:** $[XX,XXX]
**ROI:** [XXX]% ([X]x return)
**Payback Period:** [X] days

**Verdict:** ✅ Highly Profitable / 🟡 Profitable / 🔴 Needs Improvement

## Cost Breakdown

### Direct Costs
| Item | Quantity | Unit Cost | Total |
|------|----------|-----------|-------|
| ColdSend Credits | [X] | $[X.XX] | $[X,XXX] |
| Data/Enrichment | [X] | $[X.XX] | $[XXX] |
| Tools/Software | [X] | $[X.XX] | $[XXX] |
| Services/Freelancers | [X hrs] | $[X/hr] | $[XXX] |
| **Total Direct Costs** | | | **$[X,XXX]** |

### Time Investment
- Campaign Setup: [X] hours
- Ongoing Management: [Y] hours/week
- Total Time Cost: $[Z] (@ $[rate]/hr)

**Total Fully-Loaded Cost:** $[X,XXX]

## Performance Metrics

### Funnel Overview
| Stage | Volume | Rate |
|-------|--------|------|
| Emails Sent | [X,XXX] | 100% |
| Delivered | [X,XXX] | [XX]% |
| Opened | [XXX] | [XX]% |
| Replied | [XXX] | [X]% |
| Meetings Booked | [XX] | [X]% |
| Customers Acquired | [X] | [X]% |

### Unit Economics
| Metric | Value | Benchmark | Status |
|--------|-------|-----------|--------|
| Cost Per Lead | $[XXX] | $50-$500 | ✅/⚠️/❌ |
| Cost Per Meeting | $[X,XXX] | $200-$2,000 | ✅/⚠️/❌ |
| Cost Per Customer | $[X,XXX] | $1k-$10k | ✅/⚠️/❌ |
| Average Deal Value | $[XX,XXX] | - | - |
| Lifetime Value (LTV) | $[XX,XXX] | - | - |

## Revenue Attribution

### Pipeline Generated
- **Total Pipeline:** $[XXX,XXX]
- **Weighted Pipeline:** $[XX,XXX] (probability-adjusted)
- **Pipeline per Email:** $[XX]
- **Pipeline per Dollar Spent:** $[X.XX]

### Actual Revenue (Closed-Won)
- **Attributed Revenue:** $[XX,XXX]
- **Number of Customers:** [X]
- **Average Deal Size:** $[XX,XXX]
- **Sales Cycle:** [X] days (average)

## ROI Analysis

### Return Calculation
```
Investment: $[X,XXX]
Return: $[XX,XXX]
Net Profit: $[X,XXX]

ROI = [(Return - Investment) / Investment] × 100
    = [((XX,XXX - X,XXX) / X,XXX)] × 100
    = [XXX]%
```

**Return Multiple:** [X]x (for every $1 spent, you get $[X] back)

### Break-Even Analysis
- **Break-Even Customers Needed:** [X.X]
- **Actual Customers:** [X]
- **Margin Above Break-Even:** [XX]%
- **Days to Break-Even:** [X] days

### Scenario Analysis

| Scenario | Customers | Revenue | ROI | Probability |
|----------|-----------|---------|-----|-------------|
| Worst Case | [X] | $[X,XXX] | [X]% | 25% |
| Most Likely | [X] | $[XX,XXX] | [XXX]% | 50% |
| Best Case | [X] | $[XX,XXX] | [XXX]% | 25% |

### Sensitivity Analysis

**Impact of Key Variable Changes:**

1. **If Close Rate Drops to [X]%:**
   - New ROI: [XXX]%
   - Additional customers needed: [X]

2. **If Deal Value Increases by [X]%:**
   - New ROI: [XXX]%
   - Revenue increase: $[X,XXX]

3. **If Reply Rate Improves to [X]%:**
   - New meetings: [X]
   - Additional revenue: $[X,XXX]

## Recommendations

### 🟢 Continue/Scale (If ROI >500%)
1. **Increase Volume**: Scale to [X] emails/day
2. **Expand Segments**: Add [new ICP/industry]
3. **More Inboxes**: Onboard [X] additional sender accounts
4. **Higher Price Points**: Test premium positioning

### 🟡 Optimize (If ROI 100-500%)
1. **Improve Copy**: A/B test to lift reply rate from [X]% to [Y]%
2. **Better Targeting**: Tighten ICP to focus on [specific segment]
3. **Follow-Up Optimization**: Add [X] more touchpoints
4. **Reduce Costs**: Negotiate better credit pricing

### 🔴 Pivot (If ROI <100%)
1. **Revisit ICP**: Current audience may not be ideal fit
2. **Overhaul Offer**: Value proposition may not resonate
3. **Price Adjustment**: May need to target higher-value deals
4. **Consider Pause**: Cut losses and redirect budget

## Next Steps

### Immediate Actions (This Week):
1. [Action 1] - Expected impact: +[X]% ROI
2. [Action 2] - Expected impact: +[Y]% ROI
3. [Action 3] - Expected impact: Reduce cost by $[Z]

### Strategic Moves (Next Month):
1. [Initiative 1] - Timeline: [X] weeks
2. [Initiative 2] - Timeline: [Y] weeks

### Monitoring Cadence:
- **Weekly**: Track leading indicators (replies, meetings)
- **Monthly**: Full ROI analysis refresh
- **Quarterly**: Strategic review and planning

---
*Want to improve these numbers? Run the campaign-audit skill for detailed optimization recommendations.*
```

## Supporting Files

This skill references:
- `templates/roi-dashboard.xlsx` - Excel calculator template
- `examples/benchmarks.md` - Industry benchmark data
- `calculators/break-even.md` - Interactive break-even calculator

Load these files from the skill directory when available.
