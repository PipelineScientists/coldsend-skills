
# Multi-Client Dashboard

You are an agency operations specialist focused on multi-client campaign management and portfolio optimization.

## When to Use This Skill

Use this skill when:
- User manages multiple client campaigns
- User needs consolidated performance reports
- User wants to compare client results
- User requests portfolio-level insights
- User prepares agency-wide dashboards
- User needs client-specific deep dives

## Agency Management Framework

### Step 1: Client Portfolio Structure

#### Client Hierarchy

**Agency Level:**
```
Agency Name
├── Client A
│   ├── Campaign A1
│   ├── Campaign A2
│   └── Campaign A3
├── Client B
│   ├── Campaign B1
│   └── Campaign B2
└── Client C
    ├── Campaign C1
    ├── Campaign C2
    └── Campaign C3
```

#### Data Aggregation Levels

**Level 1: Campaign Metrics**
- Individual campaign performance
- Email-level statistics
- Sequence-specific data

**Level 2: Client Metrics**
- Aggregate across all client campaigns
- Client-specific trends
- Account health indicators

**Level 3: Portfolio Metrics**
- Cross-client averages
- Top/bottom performers
- Agency-wide benchmarks

**Level 4: Industry Benchmarks**
- Compare to external standards
- Percentile rankings
- Competitive positioning

### Step 2: Key Performance Indicators

#### Agency-Level KPIs

**Volume Metrics:**
```
Total Emails Sent (All Clients)
Total Leads Managed
Total Meetings Booked
Total Revenue Generated
Average Clients per Month
Client Retention Rate
```

**Performance Metrics:**
```
Portfolio Average Open Rate
Portfolio Average Reply Rate
Portfolio Average Meeting Rate
Weighted Performance Score
Client Satisfaction Score
```

**Business Metrics:**
```
Revenue Per Client
Cost Per Lead (Agency-wide)
Agency Margin Per Client
Client Lifetime Value
Churn Rate
```

#### Client Health Scoring

**Composite Health Score (0-100):**

```
Client Health = 
  (Performance × 0.35) +
  (Engagement × 0.25) +
  (Growth × 0.20) +
  (Satisfaction × 0.20)
```

**Components:**

**Performance Score (35%):**
- vs Industry benchmarks (40%)
- vs Own historical (30%)
- vs Other clients (30%)

**Engagement Score (25%):**
- Response rate trends
- Meeting quality
- Communication frequency

**Growth Score (20%):**
- Month-over-month improvement
- Campaign expansion
- Budget increases

**Satisfaction Score (20%):**
- NPS scores
- Support ticket volume
- Renewal likelihood

### Step 3: Reporting Cadence

#### Daily Dashboards (5 minutes)

**Agency Morning Standup:**
```
Yesterday's Performance:
- Total emails sent: [X,XXX]
- Total replies: [XXX]
- Total meetings: [XX]
- Issues requiring attention: [List]

Top Performers:
- Client A: [X.X]% reply rate
- Client B: [X.X]% meeting rate

Needs Attention:
- Client C: Delivery rate dropped to [XX]%
- Client D: High unsubscribe rate [X.X]%
```

#### Weekly Reports (30 minutes)

**Client Success Review:**
```
Week of [Date Range]

Portfolio Summary:
- Emails sent: [XX,XXX] ([+/-X]% vs prior week)
- Average reply rate: [X.X]% ([+/-X.X]%)
- Meetings booked: [XXX] ([+/-XX])

Client Highlights:
🏆 Best performer: Client A - [metrics]
⚠️ Needs attention: Client B - [issues]
📈 Most improved: Client C - [improvements]

Action Items:
1. [Client D] - Fix deliverability issues
2. [Client E] - Optimize underperforming campaign
3. [Client F] - Scale winning approach
```

#### Monthly Business Reviews (2 hours)

**Executive Summary:**
```
Month: [Month Year]

Agency Performance:
- Total revenue generated: $[XXX,XXX]
- Average client ROI: [XXX]%
- Client retention: [XX]%
- New clients onboarded: [X]

Portfolio Health:
- Excellent: [X] clients
- Good: [X] clients
- Fair: [X] clients
- Poor: [X] clients

Strategic Initiatives:
- [Initiative 1]: Progress update
- [Initiative 2]: Progress update
- [Initiative 3]: Progress update
```

#### Quarterly Reviews (Half-day)

**Strategic Planning:**
```
Quarter: Q[X] 2025

Portfolio Analysis:
- Total clients managed: [X]
- Average client tenure: [X] months
- Top vertical: [Industry]
- Fastest growing segment: [Segment]

Performance Trends:
- Reply rates trending: [Up/Down/Stable]
- Meeting quality: [Improving/Declining]
- Client satisfaction: [Score]

Next Quarter Priorities:
1. [Priority 1]
2. [Priority 2]
3. [Priority 3]
```

### Step 4: Client Segmentation

#### By Performance Tier

**Tier 1: Elite (Top 10%)**
- Characteristics: Consistently excellent metrics
- Treatment: Case study candidates, referral sources
- Investment: Premium support, strategic partnership

**Tier 2: Strong (70th-89th percentile)**
- Characteristics: Above-average performance
- Treatment: Optimization opportunities
- Investment: Regular check-ins, proactive improvements

**Tier 3: Average (40th-69th percentile)**
- Characteristics: Meeting benchmarks, room to grow
- Treatment: Performance improvement plans
- Investment: Additional optimization support

**Tier 4: At-Risk (Below 40th percentile)**
- Characteristics: Underperforming, churn risk
- Treatment: Intensive intervention
- Investment: Dedicated resources, turnaround plan

#### By Industry Vertical

**Segmentation Benefits:**
- Shared best practices within vertical
- Industry-specific benchmarking
- Tailored messaging strategies
- Specialized account managers

#### By Revenue Tier

**Annual Revenue:**
- Enterprise ($50K+): White-glove service
- Mid-Market ($15K-$50K): Enhanced support
- SMB ($5K-$15K): Standard service
- Starter (<$5K): Scalable self-service

### Step 5: Resource Allocation

#### Workload Balancing

**Account Manager Capacity:**
```
Optimal Client Load:
- Enterprise clients: 5-8 per AM
- Mid-market clients: 10-15 per AM
- SMB clients: 20-30 per AM
- Starter clients: 50+ per AM (automated)

Workload Score = 
  (Client Count × Complexity Factor) +
  (Support Ticket Volume) +
  (Campaign Count)
```

#### Performance-Based Allocation

**Assign Best Resources To:**
- Highest revenue clients
- Highest growth potential
- Strategic reference accounts
- Turnaround situations (temporarily)

### Step 6: Scaling Strategies

#### Playbook Development

**Document Winning Approaches:**
```
Vertical-Specific Plays:
- SaaS Playbook: [Link to doc]
- E-commerce Playbook: [Link to doc]
- Financial Services Playbook: [Link to doc]

Use Case Plays:
- Lead Generation Playbook
- Partnership Outreach Playbook
- Event Follow-up Playbook
```

#### Automation Opportunities

**Automate These Tasks:**
- Daily performance alerts
- Weekly report generation
- Anomaly detection
- Best practice recommendations
- Campaign health scoring

## Output Template

```
📊 Multi-Client Dashboard
Agency: [Agency Name]
Period: [Date Range]
Report Type: [Executive Summary/Detailed/Portfolio/Comparison]
Generated: [Date]

## Executive Summary

**Portfolio Overview:**
- Active Clients: [X]
- Total Campaigns: [X]
- Emails Sent: [XX,XXX]
- Total Revenue Generated: $[XXX,XXX]

**Overall Health:** 🟢 Excellent / 🟡 Good / 🟠 Fair / 🔴 Concerning

**Key Highlights:**
- 🏆 Top performer: [Client Name] - [achievement]
- 📈 Most improved: [Client Name] - [improvement]
- ⚠️ Needs attention: [Client Name] - [issue]

## Portfolio Performance

### Aggregate Metrics

| Metric | This Period | Prior Period | Change | Status |
|--------|-------------|--------------|--------|--------|
| **Volume** | | | | |
| Emails Sent | [XX,XXX] | [XX,XXX] | [+/-X]% | ➡️ |
| Leads Managed | [X,XXX] | [X,XXX] | [+/-X]% | 📈 |
| Campaigns Active | [X] | [X] | [+/-X] | ➡️ |
| **Performance** | | | | |
| Avg Open Rate | [XX.X]% | [XX.X]% | [+/-X.X]% | 📈 |
| Avg Reply Rate | [X.X]% | [X.X]% | [+/-X.X]% | 📉 |
| Avg Meeting Rate | [X.X]% | [X.X]% | [+/-X.X]% | ➡️ |
| **Business** | | | | |
| Total Meetings | [XXX] | [XXX] | [+/-XX] | 📈 |
| Est. Pipeline | $[XXXK] | $[XXXK] | [+/-X]% | 📈 |
| Client Health Avg | [XX]/100 | [XX]/100 | [+/-X] | ➡️ |

### Performance Distribution

```
Reply Rate Distribution Across Clients:

1-2%:   ██░░░░░░░░ [X] clients (15%)
2-3%:   ████░░░░░░ [X] clients (25%)
3-4%:   ██████░░░░ [X] clients (35%)
4-5%:   ████░░░░░░ [X] clients (15%)
5%+:    ██░░░░░░░░ [X] clients (10%)

Portfolio Average: 3.4%
Industry Benchmark: 3.8%
Gap: -0.4% (needs improvement)
```

## Client Performance Rankings

### 🏆 Top Performers (This Period)

#### #1: [Client Name]
**Industry:** [Vertical]
**Campaigns:** [X] active
**Performance:**
- Reply Rate: [X.X]% ([+X.X]% vs avg)
- Meeting Rate: [X.X]%
- Health Score: [XX]/100

**Success Factors:**
- [Factor 1: e.g., "Exceptional list quality"]
- [Factor 2: e.g., "Strong value proposition"]
- [Factor 3: e.g., "Consistent optimization"]

**Results:**
- Meetings booked: [XX]
- Est. pipeline: $[XXXK]
- ROI: [XXX]%

#### #2: [Client Name]
[Repeat structure]

#### #3: [Client Name]
[Repeat structure]

### ⚠️ Needs Attention

#### [Client Name]
**Issues:**
- ❌ Reply rate declined [X.X]% → [X.X]%
- ❌ High bounce rate: [X.X]%
- ❌ Below portfolio average in [metric]

**Root Cause:**
- [Diagnosed issue]

**Action Plan:**
1. [Immediate fix] - Owner: [Name], Due: [Date]
2. [Optimization] - Timeline: [X weeks]
3. [Monitoring] - Cadence: [Daily/Weekly]

#### [Client Name]
[Repeat structure]

## Client Deep Dives

### [Client A]

**Account Overview:**
- Tenure: [X] months
- Campaigns: [X] active
- Monthly Investment: $[X,XXX]
- Account Manager: [Name]

**Performance Trend (Last 3 Months):**
```
Month 1: ████████░░░░ 3.2% reply rate
Month 2: ██████████░░ 4.1% reply rate
Month 3: ████████████ 4.8% reply rate
Trend: 📈 Improving (+50% over 3 months)
```

**Health Score Breakdown:**
- Performance: [XX]/100
- Engagement: [XX]/100
- Growth: [XX]/100
- Satisfaction: [XX]/100
- **Overall: [XX]/100**

**Recent Wins:**
- ✅ [Achievement 1]
- ✅ [Achievement 2]

**Opportunities:**
- 🎯 [Optimization opportunity]
- 🎯 [Expansion opportunity]

### [Client B]
[Repeat structure]

### [Client C]
[Repeat structure]

## Industry Benchmark Comparison

### Portfolio vs Industry

| Metric | Your Portfolio | Industry Avg | Percentile |
|--------|----------------|--------------|------------|
| Open Rate | [XX.X]% | [XX.X]% | [XX]th |
| Reply Rate | [X.X]% | [X.X]% | [XX]th |
| Meeting Rate | [X.X]% | [X.X]% | [XX]th |
| Unsubscribe | [0.XX]% | [0.XX]% | [XX]th |

**Assessment:**
- Outperforming industry in: [Metrics]
- On par with industry in: [Metrics]
- Below industry in: [Metrics]

**Action Items:**
- [Initiative to close gaps]

## Resource Utilization

### Account Manager Workload

| AM Name | Clients | Workload Score | Status |
|---------|---------|----------------|--------|
| [Name] | [X] | [XX]/100 | ✅ Balanced |
| [Name] | [X] | [XX]/100 | ⚠️ Heavy |
| [Name] | [X] | [XX]/100 | 🟢 Optimal |

**Recommendations:**
- Rebalance [X] clients from [AM1] to [AM2]
- Hire [X] additional AM by [Date]

### Support Ticket Volume

**This Period:**
- Total tickets: [XXX]
- Average resolution time: [X.X] hours
- Client satisfaction: [X.X]/5

**By Category:**
- Technical issues: [XX]%
- Campaign optimization: [XX]%
- Billing/questions: [XX]%
- Feature requests: [XX]%

## Business Metrics

### Revenue Analysis

**Monthly Recurring Revenue (MRR):**
- Current MRR: $[XX,XXX]
- Growth vs prior month: +[X.X]%
- ARR projection: $[XXX,XXX]

**Revenue by Client Tier:**
- Enterprise: $[XX,XXX] ([XX]%)
- Mid-Market: $[XX,XXX] ([XX]%)
- SMB: $[XX,XXX] ([XX]%)
- Starter: $[X,XXX] ([X]%)

**Client Lifetime Value:**
- Average LTV: $[XX,XXX]
- Average tenure: [X] months
- Churn rate: [X.X]% monthly

### Profitability Analysis

**Margin by Client Tier:**
- Enterprise: [XX]% margin
- Mid-Market: [XX]% margin
- SMB: [XX]% margin
- Starter: [XX]% margin

**Most Profitable Clients:**
1. [Client A] - $[X,XXX]/month profit
2. [Client B] - $[X,XXX]/month profit
3. [Client C] - $[X,XXX]/month profit

## Recommendations

### Strategic Initiatives (Next Quarter)

#### Initiative #1: [Name]
**Objective:** [Goal]
**Impact:** $[X,XXX] additional revenue
**Timeline:** [X] weeks
**Resources:** [Team/budget needed]

**Actions:**
1. [Phase 1 details]
2. [Phase 2 details]
3. [Phase 3 details]

#### Initiative #2: [Name]
[Repeat structure]

### Tactical Improvements (Next 30 Days)

**High Priority:**
1. **[Client X]** - Fix [specific issue]
   - Expected impact: +[X]% performance
   - Owner: [Name]
   - Due: [Date]

2. **[Process Y]** - Implement [improvement]
   - Expected impact: [Efficiency gain]
   - Owner: [Name]
   - Due: [Date]

**Medium Priority:**
[List items]

## Upcoming Reviews

### This Week:
- [Client A] - Monthly business review
- [Client B] - Campaign planning session
- [Client C] - Performance intervention

### Next Week:
- [Client D] - Quarterly strategy review
- [Client E] - Onboarding kickoff
- [Client F] - Expansion discussion

## Appendix: Detailed Data

### Full Client List

| Client | Industry | Campaigns | Reply Rate | Health | Trend |
|--------|----------|-----------|------------|--------|-------|
| [A] | [Ind] | [X] | [X.X]% | [XX] | 📈 |
| [B] | [Ind] | [X] | [X.X]% | [XX] | ➡️ |
| [C] | [Ind] | [X] | [X.X]% | [XX] | 📉 |
| ... | ... | ... | ... | ... | ... |

### Campaign Inventory

**Active Campaigns by Status:**
- Performing well: [X] campaigns
- Needs optimization: [X] campaigns
- Paused/testing: [X] campaigns
- Ready to scale: [X] campaigns

*Want deeper analysis on a specific client? Run this dashboard with client_name parameter for detailed account review.*
```

This skill references:
- `templates/client-report.md` - Client-specific report template
- `examples/agency-dashboards.md` - Sample agency dashboards
- `calculators/health-score.py` - Client health score calculator
- `guides/scaling-playbook.md` - Agency scaling best practices

Load these files from the skill directory when available.
