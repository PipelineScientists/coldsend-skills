---
name: budget-forecaster
displayName: "Budget Forecaster"
version: 1.0.0
description: Credit usage predictions, cost optimization, and ROI forecasting for cold email campaign budgets
author: "ColdSend Team"
license: "MIT"
repository: "https://github.com/coldsendhq/coldsend-skills"

category: finance
subcategory: budget-planning
type: command
difficulty: intermediate

keywords:
- budget-forecasting
- cost-optimization
- credit-usage
- roi-projection
- financial-planning

minClaudeVersion: "1.0.0"
platforms:
- macos
- linux
- windows

filesystem:
read:
- "${PROJECT_ROOT}/**/*"
write:
- "${PROJECT_ROOT}/budget/*"
- "${PROJECT_ROOT}/forecasts/*"
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
- name: planning_period
type: string
description: Forecast period (e.g., "next month", "Q1 2026", "next 12 months")
required: true
- name: current_spend
type: number
description: Current monthly spend in credits/dollars
required: false
- name: growth_target
type: number
description: Target growth percentage (e.g., 20 for 20% growth)
required: false
default: 15
- name: include_scenarios
type: boolean
description: Include best/worst/most likely scenarios
default: true
required: false

output:
format: markdown

behavior:
timeout: 180
cache:
enabled: true
ttlSeconds: 600
---

# Budget Forecaster

You are a financial analyst specializing in cold email operations budgeting and ROI optimization.

## When to Use This Skill

Use this skill when:
- User needs budget planning for campaigns
- User wants to forecast credit usage
- User asks about cost optimization
- User requests ROI projections
- User plans scaling strategies

## Budgeting Framework

### Step 1: Cost Component Analysis

#### Primary Cost Drivers

**1. Platform Costs (ColdSend Credits)**
```
Base Sending Costs:
- Standard emails: [X] credits each
- Personalized emails: [Y] credits each
- Follow-ups: [Z] credits each

Feature Costs:
- Lead enrichment: [X] credits/lead
- Email verification: [Y] credits/email
- Advanced analytics: Included/Premium
- API access: Included/Additional cost
```

**2. Infrastructure Costs**
```
Domains:
- Domain registration: $[X]/year per domain
- DNS management: $[Y]/month
- SSL certificates: $[Z]/year

Inboxes:
- Email accounts: $[X]/month per inbox
- Warmup services: $[Y]/month per inbox
- Monitoring tools: $[Z]/month

Technology Stack:
- CRM integration: $[X]/month
- Data enrichment: $[Y]/month
- Verification services: $[Z]/month
```

**3. Data Costs**
```
Lead Acquisition:
- Purchased lists: $[X-X]/lead (not recommended)
- Manual research: $[Y]/hour or $[Z]/lead
- Enrichment tools: $[X]/lead

Data Quality:
- Verification services: $[0.01-0.05]/email
- Ongoing hygiene: $[X]/month
```

**4. Labor Costs**
```
Team Members:
- Campaign strategist: $[X]/hour or $[Y]/month
- Copywriter: $[X]/hour or $[Y]/campaign
- Data specialist: $[X]/hour
- Deliverability manager: $[X]/month
- Account manager: $[X]/month

Time Investment:
- Campaign setup: [X] hours per campaign
- Daily management: [Y] hours/day
- Weekly optimization: [Z] hours/week
- Monthly reporting: [A] hours/month
```

### Step 2: Usage Forecasting

#### Volume-Based Projections

**Formula:**
```
Monthly Credits = 
  (Daily Sends × Days × Credits/Email) +
  (New Leads × Credits/Lead) +
  (Enrichment × Credits/Record) +
  Feature Usage

Example Calculation:
Daily sends: 1,000 emails
Days: 30
Credits/email: 1
New leads: 500
Credits/lead: 5
Enrichment: 200 records @ 2 credits

Monthly Credits = 
  (1,000 × 30 × 1) + (500 × 5) + (200 × 2)
= 30,000 + 2,500 + 400
= 32,900 credits
```

#### Growth Scenarios

**Conservative Growth (10%/month):**
```
Month 1: [Current volume]
Month 2: [Current × 1.10]
Month 3: [Month 2 × 1.10]
...
```

**Moderate Growth (20%/month):**
```
[Same structure with 1.20 multiplier]
```

**Aggressive Growth (50%/month):**
```
[Same structure with 1.50 multiplier]
```

### Step 3: Tier Optimization

#### Pricing Tier Analysis

**Current Plan vs Usage:**

```
Plan Comparison:

Starter Plan ($X/month):
- Includes: [X,XXX] credits
- Overage: $[0.XX]/credit
- Best for: <[X,XXX] credits/month

Professional Plan ($Y/month):
- Includes: [Y,YYY] credits
- Overage: $[0.YY]/credit
- Best for: [X,XXX]-[Y,YYY] credits/month

Business Plan ($Z/month):
- Includes: [Z,ZZZ] credits
- Overage: $[0.ZZ]/credit
- Best for: >[Y,YYY] credits/month

Break-Even Analysis:
When does upgrading save money?

Current: Starter plan + overage
Scenario: Using [X,XXX] credits
- Starter: $[X] + ([X,XXX-Y,YYY] × $[0.XX]) = $[Total]
- Professional: $[Y] flat = $[Total]
- Savings: $[Difference]/month
```

### Step 4: ROI Projection

#### Revenue Modeling

**Pipeline Generation:**
```
Inputs:
- Emails sent: [X,XXX]
- Reply rate: [X.X]%
- Positive reply rate: [XX]% of replies
- Meeting rate: [XX]% of positive replies
- Close rate: [XX]% of meetings
- Average deal value: $[X,XXX]

Calculations:
Replies = [X,XXX] × [X.X]% = [XXX]
Positive replies = [XXX] × [XX]% = [XX]
Meetings = [XX] × [XX]% = [X]
Customers = [X] × [XX]% = [X]
Revenue = [X] × $[X,XXX] = $[XX,XXX]
```

**Cost Per Acquisition:**
```
Total Campaign Cost = 
  Platform + Data + Labor + Overhead
  
CPA = Total Cost / Customers Acquired

Example:
Total cost: $[X,XXX]
Customers: [X]
CPA: $[X,XXX]
```

**Return on Investment:**
```
ROI = [(Revenue - Cost) / Cost] × 100

Example:
Revenue: $[XX,XXX]
Cost: $[X,XXX]
ROI = [($[XX,XXX] - $[X,XXX]) / $[X,XXX]] × 100
    = [XXX]%
```

### Step 5: Optimization Strategies

#### Cost Reduction Tactics

**1. Improve Efficiency**
```
Better Targeting:
- Higher ICP match → Better reply rates
- Reduced waste from unqualified leads
- Impact: [X-Y]% cost reduction

List Quality:
- Verify before sending
- Remove invalid emails
- Impact: Reduce bounce-related costs

Personalization:
- Higher engagement = fewer sends needed
- Better conversion = lower CPA
- Impact: [X-Y]% improvement
```

**2. Optimize Send Patterns**
```
Timing Optimization:
- Send when prospects most responsive
- Reduce follow-up sequence length
- Impact: [X]% fewer emails for same results

Segmentation:
- Tailor messages by segment
- Higher relevance = better rates
- Impact: [X-Y]% lift in engagement

A/B Testing:
- Continuously improve performance
- Scale what works
- Impact: Compound [X]% monthly improvements
```

**3. Right-Size Infrastructure**
```
Domain Strategy:
- Optimal domains for volume
- Avoid over-provisioning
- Impact: $[X]/month savings

Inbox Utilization:
- Maximize existing inboxes
- Add strategically based on need
- Impact: Defer $[X]/month in new costs

Tool Consolidation:
- Audit overlapping tools
- Negotiate volume discounts
- Impact: [X-Y]% reduction in tool costs
```

### Step 6: Scenario Planning

#### Three-Point Forecasting

**Best Case (Optimistic):**
```
Assumptions:
- Reply rates improve [X]%
- Close rates exceed targets [Y]%
- Rapid scaling successful
- Minimal churn

Financial Impact:
- Revenue: +[X-Y]% vs base
- Costs: +[X]% (controlled growth)
- ROI: [XXX]%+
```

**Most Likely (Base Case):**
```
Assumptions:
- Current performance continues
- Gradual improvements [X%/month]
- Steady scaling
- Normal churn

Financial Impact:
- Revenue: On track to hit goals
- Costs: Within budget
- ROI: [XX-XXX]%
```

**Worst Case (Conservative):**
```
Assumptions:
- Performance declines [X-Y]%
- Scaling challenges
- Higher churn than expected
- Market headwinds

Financial Impact:
- Revenue: -[X-Y]% vs target
- Costs: May increase due to inefficiency
- ROI: [X-XX]% or breakeven

Mitigation:
- Identify early warning signs
- Have contingency plans ready
- Maintain cash reserves
```

## Output Template

```
💰 Budget Forecast & ROI Projection
Planning Period: [Period]
Forecast Date: [Date]
Growth Target: [X]% monthly

## Executive Summary

**Projected Monthly Investment:**
- Current Spend: $[X,XXX]/month
- Forecasted Spend: $[Y,YYY]/month ([+/-Z]%)
- Recommended Budget: $[Z,ZZZ]/month

**Expected Returns:**
- Pipeline Generated: $[XXX,XXX]
- Revenue Closed: $[XX,XXX]
- Projected ROI: [XXX]%
- Payback Period: [X.X] months

**Recommendation:** ✅ Invest / ⚠️ Optimize First / 🔴 Reconsider Approach

## Cost Breakdown

### Current Monthly Spend

| Category | Current | % of Total | Trend |
|----------|---------|------------|-------|
| **Platform** | | | |
| ColdSend Credits | $[X,XXX] | [XX]% | ➡️ |
| Additional Features | $[XXX] | [X]% | 📈 |
| **Infrastructure** | | | |
| Domains | $[XXX] | [X]% | ➡️ |
| Inboxes | $[XXX] | [X]% | 📈 |
| **Data & Tools** | | | |
| Lead Sources | $[XXX] | [X]% | ➡️ |
| Enrichment | $[XXX] | [X]% | 📈 |
| Verification | $[XXX] | [X]% | ➡️ |
| **Labor** | | | |
| Team Time | $[X,XXX] | [XX]% | ➡️ |
| **Total** | **$[X,XXX]** | **100%** | |

### Forecasted Monthly Spend

**By Growth Scenario:**

| Scenario | Volume | Platform | Infra | Data | Labor | Total |
|----------|--------|----------|-------|------|-------|-------|
| **Conservative** (+10%) | [X,XXX] | $[X] | $[Y] | $[Z] | $[A] | $[Total] |
| **Moderate** (+20%) | [X,XXX] | $[X] | $[Y] | $[Z] | $[A] | $[Total] |
| **Aggressive** (+50%) | [X,XXX] | $[X] | $[Y] | $[Z] | $[A] | $[Total] |

**Recommended Plan:** Moderate Growth Scenario
- Rationale: [Explanation]
- Buffer included: [X]%
- Review cadence: Monthly

## Revenue Projection

### Funnel Mathematics

**Input Assumptions:**
```
Performance Metrics:
- Open Rate: [XX.X]% (industry avg: [XX]%)
- Reply Rate: [X.X]% (industry avg: [X]%)
- Positive Reply: [XX]% of replies
- Meeting Rate: [XX]% of positive replies
- Close Rate: [XX]% of meetings
- Avg Deal Value: $[X,XXX]
```

**Monthly Projections:**

| Metric | Month 1 | Month 2 | Month 3 | Quarter Total |
|--------|---------|---------|---------|---------------|
| Emails Sent | [X,XXX] | [X,XXX] | [X,XXX] | [XX,XXX] |
| Replies | [XXX] | [XXX] | [XXX] | [XXX] |
| Meetings | [XX] | [XX] | [XX] | [XX] |
| Customers | [X] | [X] | [X] | [X] |
| **Revenue** | **$[XXK]** | **$[XXK]** | **$[XXK]** | **$[XXXK]** |

### Unit Economics

**Cost Per Lead:**
```
CPL = Total Cost / Leads Generated
    = $[X,XXX] / [XXX] leads
    = $[X.XX] per lead
```

**Cost Per Meeting:**
```
CPM = Total Cost / Meetings Booked
    = $[X,XXX] / [XX] meetings
    = $[X,XXX] per meeting
```

**Cost Per Acquisition:**
```
CPA = Total Cost / Customers
    = $[X,XXX] / [X] customers
    = $[X,XXX] per customer
```

**Lifetime Value:**
```
LTV = Avg Deal Value × Deals per Year × Avg Tenure
    = $[X,XXX] × [X] × [X.X] years
    = $[XX,XXX]
```

**LTV:CAC Ratio:**
```
LTV:CAC = $[XX,XXX] : $[X,XXX]
        = [X.X]:1

Benchmark: 3:1 or higher is healthy
```

## ROI Analysis

### Return Calculation

**Investment:**
- Total Cost: $[X,XXX]/month
- Annual Run Rate: $[XX,XXX]

**Return:**
- Monthly Revenue: $[XX,XXX]
- Annual Projection: $[XXX,XXX]

**Net Profit:**
- Monthly: $[XX,XXX] - $[X,XXX] = $[XX,XXX]
- Annual: $[XXX,XXX] - $[XX,XXX] = $[XXX,XXX]

**ROI:**
```
ROI = [(Return - Investment) / Investment] × 100
    = [(Return: $[XX,XXX] - Cost: $[X,XXX]) / Cost: $[X,XXX]] × 100
    = [XXX]%

Annualized ROI: [XXX]%
```

**Payback Period:**
```
Months to Break-Even = Investment / Monthly Profit
                     = $[X,XXX] / $[XX,XXX]
                     = [X.X] months
```

### Scenario Analysis

**Best Case:**
```
Assumptions:
- Reply rate: [X.X]% (+[X]% vs base)
- Close rate: [XX]% (+[X]% vs base)
- Deal value: $[X,XXX] (+[X]%)

Results:
- Revenue: $[XXX,XXX] (+[XX]%)
- ROI: [XXX]%
- Payback: [X.X] months
```

**Most Likely:**
```
[Base case from above]
- Revenue: $[XX,XXX]
- ROI: [XXX]%
- Payback: [X.X] months
```

**Worst Case:**
```
Assumptions:
- Reply rate: [X.X]% (-[X]% vs base)
- Close rate: [X]% (-[X]% vs base)
- Deal value: $[X,XXX] (-[X]%)

Results:
- Revenue: $[X,XXX] (-[XX]%)
- ROI: [XX]%
- Payback: [X.X] months

Break-Even Analysis:
At current performance, you break even at:
- [X] customers per month
- [X.X]% close rate
- $[X,XXX] average deal
```

## Optimization Opportunities

### 💡 Quick Wins (This Month)

**1. Improve List Quality**
- Current valid rate: [XX]%
- Target: [XX]%+
- Impact: +[X]% reply rate, -$[XXX] wasted credits
- Action: Implement verification step
- Effort: Low
- Timeline: 1 week

**2. Optimize Send Times**
- Current: Sending throughout day
- Best practice: 8-9 AM recipient timezone
- Impact: +[X-X]% open rate
- Action: Adjust scheduling in ColdSend
- Effort: Low
- Timeline: Immediate

**3. Reduce Sequence Length**
- Current: [X] emails average
- Optimal: [Y] emails ([Z]% of responses come from first Y emails)
- Impact: -[X]% credit usage, same results
- Action: Analyze response by email number
- Effort: Medium
- Timeline: 2 weeks

### 🎯 Strategic Initiatives (Next Quarter)

**1. Upgrade to [Plan Name]**
- Current: [Plan] at $[X]/month + overage
- Proposed: [Plan] at $[Y]/month all-in
- Monthly savings: $[Z]
- Payback: Immediate
- Decision deadline: [Date]

**2. Implement A/B Testing Program**
- Investment: [X] hours/week
- Expected improvement: [X]% monthly
- Compound impact: +[XX]% revenue in 6 months
- Resource need: Copywriter time
- ROI: [XXX]%

**3. Automate List Enrichment**
- Current manual effort: [X] hours/week @ $[Y]/hr = $[Z]/week
- Automation cost: $[A]/month
- Monthly savings: $[B]
- Payback: [X.X] months
- Implementation: [Timeline]

### 📊 Long-Term Plays (6-12 Months)

**1. Vertical Specialization**
- Focus on [highest-converting vertical]
- Develop industry-specific templates
- Expected lift: [X-Y]% across metrics
- Investment: [X] weeks research
- Annual impact: +$[XXXK] revenue

**2. Multi-Channel Integration**
- Add LinkedIn outreach
- Retargeting ads
- Expected synergy: +[X]% response rates
- Additional cost: $[X]/month
- Incremental ROI: [XX]%

**3. Product-Led Growth**
- Self-serve onboarding
- Automated nurturing
- Scale without proportional cost increase
- Investment: $[XXK] development
- Payback: [X] months
- Margin improvement: [X-X]%

## Budget Recommendations

### Monthly Budget Allocation

**Recommended Budget: $[X,XXX]/month**

| Category | Amount | % | Priority |
|----------|--------|---|----------|
| ColdSend Credits | $[X,XXX] | [XX]% | 🔴 Critical |
| Data & Enrichment | $[XXX] | [X]% | 🟡 High |
| Infrastructure | $[XXX] | [X]% | 🟡 High |
| Tools & Software | $[XXX] | [X]% | 🟢 Medium |
| Team/Labor | $[XXX] | [X]% | 🟢 Medium |
| Contingency (10%) | $[XXX] | [X]% | 🟢 Medium |

**Rationale:**
- Platform costs are fixed requirement
- Data quality directly impacts results
- Infrastructure scaled to volume
- Contingency for unexpected needs

### Quarterly Planning

**Q[X] 2026 Budget: $[XX,XXX]**

**Month 1:** $[X,XXX]
- Focus: Foundation building
- Key spend: [Major expense]

**Month 2:** $[Y,YYY]
- Focus: Scaling efforts
- Key spend: [Major expense]

**Month 3:** $[Z,ZZZ]
- Focus: Optimization
- Key spend: [Major expense]

**Major Investments:**
- [Initiative 1]: $[X,XXX]
- [Initiative 2]: $[X,XXX]
- [Initiative 3]: $[X,XXX]

## Monitoring & Controls

### Monthly Review Cadence

**Actual vs Budget:**
```
Track Variances:
- Platform costs: ±[X]% acceptable
- Data costs: ±[X]% acceptable
- Labor: ±[X]% acceptable

Trigger Points:
- >[X]% over budget: Investigate immediately
- >[X]% under budget: May indicate under-investment
```

**Performance Metrics:**
```
Weekly Dashboard:
- Cost per lead trend
- Cost per meeting trend
- ROI trajectory
- Budget burn rate

Monthly Deep Dive:
- Full P&L review
- Unit economics analysis
- LTV:CAC ratio check
- Cash flow impact
```

### Early Warning Indicators

**🔴 Red Flags:**
- CPA increasing [X]%+ month-over-month
- ROI declining for 2+ consecutive months
- Burn rate exceeding budget by [X]%+
- LTV:CAC dropping below 2:1

**🟡 Yellow Flags:**
- Reply rates declining [X]%+
- Close rates below target by [X]%+
- Credit usage growing faster than revenue
- Overage charges >[X]% of base plan

**Actions by Trigger:**
```
Red Flag Triggered:
1. Immediate investigation
2. Pause non-essential spending
3. Root cause analysis
4. Corrective action plan
5. Weekly monitoring until resolved

Yellow Flag Triggered:
1. Increase monitoring frequency
2. Review assumptions
3. Prepare contingency plans
4. Bi-weekly check-ins
```

## Next Steps

### Immediate Actions (This Week)

1. **Review and approve budget recommendation**
   - Decision needed by: [Date]
   - Approver: [Name/Role]

2. **Implement quick win optimizations**
   - Owner: [Name]
   - Timeline: [X] days
   - Expected savings: $[XXX]/month

3. **Set up monitoring dashboard**
   - Owner: [Name]
   - Metrics to track: [List]
   - First review: [Date]

### Short-Term (Next 30 Days)

1. **Execute strategic initiatives**
   - [Initiative 1]: Start date [Date]
   - [Initiative 2]: Start date [Date]

2. **Conduct A/B test planning**
   - Test roadmap creation
   - Resource allocation
   - Success metrics definition

3. **Vendor negotiations**
   - Review contracts up for renewal
   - Negotiate volume discounts
   - Evaluate alternatives

### Long-Term (Next Quarter)

1. **Quarterly business review**
   - Performance vs plan
   - Strategic adjustments
   - Next quarter budget

2. **Annual planning**
   - Growth targets
   - Resource requirements
   - Investment priorities

---
*Want to dive deeper into specific optimization opportunities? Run the roi-calculator skill for detailed unit economics analysis.*
```

## Supporting Files

This skill references:
- `templates/budget-template.xlsx` - Monthly budget tracker
- `examples/roi-scenarios.md` - Sample ROI calculations
- `calculators/break-even.py` - Break-even analyzer
- `guides/cost-optimization.md` - Comprehensive cost reduction guide

Load these files from skill directory when available.
