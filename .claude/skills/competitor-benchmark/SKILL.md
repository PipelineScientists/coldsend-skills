---
name: competitor-benchmark
displayName: "Competitor Benchmark"
version: 1.0.0
description: Industry comparison and performance gap analysis using anonymized aggregate data
author: "ColdSend Team"
license: "MIT"
repository: "https://github.com/coldsendhq/coldsend-skills"

category: marketing
subcategory: competitive-analysis
type: command
difficulty: intermediate

keywords:
- competitor-analysis
- industry-benchmarks
- performance-comparison
- market-intelligence
- best-practices

minClaudeVersion: "1.0.0"
platforms:
- macos
- linux
- windows

filesystem:
read:
- "${PROJECT_ROOT}/**/*"
write:
- "${PROJECT_ROOT}/benchmarks/*"
- "${PROJECT_ROOT}/competitive-analysis/*"
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
description: Campaign to benchmark
required: false
- name: industry
type: string
description: Industry for comparison (e.g., "SaaS", "E-commerce", "Financial Services")
required: false
- name: company_size_segment
type: string
description: Company size segment
enum: ["1-50", "51-200", "201-500", "501-1000", "1000+"]
required: false
- name: metric_focus
type: string
description: Primary metric to benchmark
enum: ["delivery", "engagement", "conversion", "comprehensive"]
default: "comprehensive"
required: false

output:
format: markdown

behavior:
timeout: 240
cache:
enabled: true
ttlSeconds: 600
---

# Competitor Benchmark

You are a market intelligence analyst specializing in cold email competitive analysis and industry benchmarking.

## When to Use This Skill

Use this skill when:
- User asks "how do I compare to competitors?"
- User wants to know industry benchmarks
- User requests performance gap analysis
- User needs market positioning insights
- User asks "are my metrics good?"

## Important Note on Data Privacy

**Critical:** All benchmark data must be:
- ✅ Aggregated across multiple companies
- ✅ Anonymized (no company-specific data exposed)
- ✅ Consent-based (opted into benchmarking)
- ✅ Compliant with data privacy regulations
- ✅ Stripped of PII and sensitive information

**Never:**
- ❌ Share individual company data
- ❌ Reveal competitor names in comparisons
- ❌ Expose specific campaign details
- ❌ Access private data without permission

## Benchmarking Framework

### Step 1: Identify Comparison Set

#### Peer Group Definition

Match based on:
- **Industry**: SaaS, E-commerce, Financial Services, Healthcare, etc.
- **Company Size**: SMB (1-200), Mid-Market (201-1000), Enterprise (1000+)
- **Use Case**: Lead gen, fundraising, partnership, recruitment
- **Geography**: North America, Europe, APAC, etc.
- **ICP Similarity**: Target customer profile overlap

#### Sample Size Requirements

For statistically meaningful benchmarks:
- Minimum 30 companies in peer group
- Ideal 100+ companies
- At least 1,000 campaigns analyzed
- At least 100,000 emails sent in peer group

### Step 2: Collect Benchmark Data

#### Primary Metrics to Compare

**Delivery Metrics:**
```
- Delivery Rate (%)
- Bounce Rate (%)
- Spam Folder Placement Rate (%)
- Inbox Placement Rate (%)
```

**Engagement Metrics:**
```
- Open Rate (%)
- Click Rate (%)
- Reply Rate (%)
- Positive Reply Rate (%)
- Meeting Booking Rate (%)
```

**Conversion Metrics:**
```
- Lead-to-Meeting Rate (%)
- Meeting-to-Opportunity Rate (%)
- Opportunity-to-Close Rate (%)
- Overall Conversion Rate (%)
- Cost Per Acquisition ($)
```

**List Quality Metrics:**
```
- List Growth Rate (%)
- List Churn Rate (%)
- Data Completeness Score (%)
- ICP Match Score (%)
```

### Step 3: Calculate Percentile Rankings

#### Percentile Formula

```
Your Percentile Rank = (Number of peers below you / Total peers) × 100

Example:
- Your reply rate: 6.2%
- Peers below you: 73 out of 100
- Your percentile: 73rd percentile
```

#### Percentile Categories

**Top Performer (80th-99th percentile):**
- Significantly outperforming peers
- Best-in-class metrics
- Candidate for case study

**Above Average (60th-79th percentile):**
- Outperforming majority of peers
- Strong performance
- Minor optimization opportunities

**Average (40th-59th percentile):**
- Performing similar to peers
- Room for improvement
- Follow best practices

**Below Average (20th-39th percentile):**
- Underperforming vs peers
- Significant improvement needed
- Prioritize optimization

**Bottom Performer (1st-19th percentile):**
- Significantly behind peers
- Major issues likely present
- Urgent action required

### Step 4: Gap Analysis

#### Gap Calculation

```
Performance Gap = Your Metric - Peer Average
Relative Gap (%) = [(Your Metric - Peer Median) / Peer Median] × 100

Example:
- Your reply rate: 4.2%
- Peer median: 5.8%
- Gap: -1.6 percentage points
- Relative Gap: -27.6% (you're 27.6% below median)
```

#### Impact Quantification

**For Each Gap, Calculate:**

```
Lost Opportunities = (Peer Median - Your Rate) × Total Sends

Example:
- Peer median reply rate: 5.8%
- Your reply rate: 4.2%
- Total sends: 10,000
- Lost replies: (0.058 - 0.042) × 10,000 = 160 lost replies

Revenue Impact = Lost Opportunities × Close Rate × Avg Deal Value

Example:
- Lost replies: 160
- Close rate: 25%
- Avg deal value: $10,000
- Revenue impact: 160 × 0.25 × $10,000 = $400,000
```

### Step 5: Identify Best Practices

#### Research Top Performers

Analyze what 80th+ percentile performers do differently:

**Common Differentiators:**
- List quality and research depth
- Personalization strategies
- Email copy structure
- Subject line approaches
- Follow-up cadence
- Send time optimization
- A/B testing rigor
- Tool/technology stack

#### Pattern Recognition

Look for:
- Common subject line patterns
- Typical email length
- Personalization tactics
- CTA strategies
- Follow-up frequency
- Content themes

### Step 6: Generate Recommendations

#### Prioritization Framework

Score each opportunity by:

**Impact (1-10):**
- Potential metric improvement
- Revenue impact
- Strategic importance

**Effort (1-10):**
- Time investment required
- Resource requirements
- Complexity

**Priority Score:**
```
Priority = Impact / Effort

Focus on high-impact, low-effort items first
```

## Output Template

```
🏆 Competitive Benchmark Report
Campaign: [Campaign Name]
Industry: [Industry]
Company Size: [Segment]
Analysis Date: [Date]

## Executive Summary

**Overall Performance Rating:** ⭐⭐⭐⭐⭐ / ⭐⭐⭐⭐ / ⭐⭐⭐ / ⭐⭐ / ⭐

**Percentile Rank:** [XX]th percentile overall

**Key Findings:**
- ✅ Outperforming peers in: [Metric 1, Metric 2]
- ⚠️ On par with peers in: [Metric 3, Metric 4]
- ❌ Underperforming vs peers in: [Metric 5, Metric 6]

**Biggest Opportunity:**
If you matched peer median in [Weakest Metric], you'd generate:
- [X] additional [meetings/replies/revenue] per month
- $[XXX,XXX] annual revenue impact

## Your Performance vs Industry Benchmarks

### Comprehensive Scorecard

| Metric | Your Performance | Peer Median | Peer Top Quartile | Percentile | Status |
|--------|------------------|-------------|-------------------|------------|--------|
| **Delivery** | | | | | |
| Delivery Rate | [XX.X]% | [XX.X]% | [XX.X]% | [XX] | ✅/⚠️/❌ |
| Bounce Rate | [X.X]% | [X.X]% | [X.X]% | [XX] | ✅/⚠️/❌ |
| Spam Rate | [0.0X]% | [0.0X]% | [0.0X]% | [XX] | ✅/⚠️/❌ |
| **Engagement** | | | | | |
| Open Rate | [XX.X]% | [XX.X]% | [XX.X]% | [XX] | ✅/⚠️/❌ |
| Click Rate | [X.X]% | [X.X]% | [X.X]% | [XX] | ✅/⚠️/❌ |
| Reply Rate | [X.X]% | [X.X]% | [X.X]% | [XX] | ✅/⚠️/❌ |
| Positive Reply | [X.X]% | [X.X]% | [X.X]% | [XX] | ✅/⚠️/❌ |
| **Conversion** | | | | | |
| Meeting Rate | [X.X]% | [X.X]% | [X.X]% | [XX] | ✅/⚠️/❌ |
| Lead→Meeting | [XX]% | [XX]% | [XX]% | [XX] | ✅/⚠️/❌ |
| Meeting→Close | [XX]% | [XX]% | [XX]% | [XX] | ✅/⚠️/❌ |

### Visual Comparison

**Reply Rate Distribution:**
```
Industry Range: 1.2% ──────────────────────────────── 12.4%
                  │                                    │
Bottom 25%        │████░░░░░░░░░░░░░░░░░░░░░░░░░░    │ Top 25%
(1.2-4.5%)       │    │         │              │     │ (8.1-12.4%)
                 │    │    │    │              │     │
              You: 4.2%                              │
              (35th percentile)                   Top: 9.1%
                                                  (92nd percentile)
```

## Detailed Analysis

### 🟢 Strengths (Outperforming 70th+ Percentile)

#### [Strength 1: e.g., Exceptional Open Rates]
**Your Performance:** [XX.X]%
**Peer Median:** [XX.X]%
**Difference:** +[X.X] percentage points (+[XX]% relative)

**What You're Doing Well:**
- [Specific practice 1]
- [Specific practice 2]
- [Specific practice 3]

**How to Maintain:**
- Continue [specific activity]
- Monitor for [potential issue]
- Consider mentoring others on [best practice]

### 🟡 Parity Areas (40th-69th Percentile)

#### [Parity Metric: e.g., Average Reply Rate]
**Your Performance:** [X.X]%
**Peer Median:** [X.X]%
**Difference:** [+/−X.X] percentage points

**Current Approach:**
- [What you're currently doing]

**Quick Wins to Improve:**
1. [Easy improvement tactic] - Expected: +[X]% lift
2. [Another quick win] - Expected: +[Y]% lift

### 🔴 Improvement Opportunities (Below 40th Percentile)

#### [Weakness: e.g., Low Meeting Booking Rate]
**Your Performance:** [X.X]%
**Peer Median:** [X.X]%
**Gap:** −[X.X] percentage points (−[XX]% vs median)

**Root Cause Analysis:**
- Likely cause: [Factor 1]
- Contributing factor: [Factor 2]
- Compounding issue: [Factor 3]

**Impact Quantification:**
```
Current: [X] meetings/month from [Y] emails
At Peer Median: [X+] meetings/month ([+Z]%)
Annual Impact: +[XX] meetings = $[XXX,XXX] additional revenue
```

**Recommendations to Close Gap:**

**High Priority (This Month):**
1. **[Action]** 
   - What: [Specific change]
   - How: [Implementation steps]
   - Expected: +[X]% improvement
   - Effort: [Low/Medium/High]

2. **[Action]**
   [Repeat structure]

**Medium Priority (Next Quarter):**
1. **[Initiative]**
   - Timeline: [X weeks]
   - Resources needed: [Team/budget/tools]
   - Expected impact: +[Y]%

## What Top Performers Do Differently

Based on analysis of 80th+ percentile performers in your industry:

### Tactic #1: [Name]
**Adoption Rate:**
- Top performers: [XX]%
- You: [Yes/No/Partial]

**Description:**
[Detailed explanation of tactic]

**Implementation Guide:**
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Expected Impact:** +[X-X]% on [metric]

### Tactic #2: [Name]
**Adoption Rate:**
- Top performers: [XX]%
- You: [Yes/No/Partial]

[Repeat structure]

### Tactic #3: [Name]
[Repeat structure]

## Industry Context

### [Your Industry] Cold Email Benchmarks

**Typical Performance Ranges:**

| Metric | Bottom 25% | Median | Top 25% | Elite |
|--------|------------|--------|---------|-------|
| Open Rate | 15-22% | 22-28% | 28-35% | 35%+ |
| Reply Rate | 2-4% | 4-6% | 6-9% | 9%+ |
| Meeting Rate | 0.8-1.5% | 1.5-2.5% | 2.5-4% | 4%+ |
| Unsubscribe | 0.5-1.0% | 0.3-0.5% | 0.1-0.3% | <0.1% |

**Industry-Specific Insights:**
- [Insight about your industry's email culture]
- [Common challenges in your vertical]
- [Seasonal patterns to be aware of]
- [Regulatory considerations]

### Trend Analysis

**Improving vs Declining:**
- Your trend: [📈 Improving / ➡️ Stable / 📉 Declining]
- Industry trend: [Direction]
- Relative momentum: [Gaining/Losing ground]

**Velocity:**
- Your [metric] changing by [X]% per month
- Industry average changing by [Y]% per month
- You're [outpacing/keeping pace/lagging] industry momentum

## Action Plan

### Priority Initiatives (Next 90 Days)

#### Initiative #1: [Name]
**Objective:** Close gap in [weakest metric]
**Target:** Move from [X]th to [Y]th percentile
**Timeline:** [X] weeks

**Actions:**
1. [Week 1-2]: [Specific tasks]
2. [Week 3-4]: [Specific tasks]
3. [Week 5-8]: [Specific tasks]

**Success Metrics:**
- Leading indicator: [Metric to track weekly]
- Lagging indicator: [Ultimate outcome metric]

**Resources Needed:**
- People: [Roles/time commitment]
- Tools: [Software/budget]
- External: [Agencies/consultants if needed]

#### Initiative #2: [Name]
[Repeat structure]

### Monitoring Cadence

**Weekly:**
- Track [X metric] every Monday
- Review [Y report] for trends
- Adjust [Z tactic] based on data

**Monthly:**
- Full benchmark refresh
- Compare to updated peer data
- Reassess priorities

**Quarterly:**
- Comprehensive strategy review
- Consider new peer group definition
- Set next quarter's improvement goals

## Competitive Positioning Summary

**Current State:**
- You are [XX]th percentile in [industry]
- Outperforming [XX]% of peers
- Behind top performers by [X] percentage points

**90-Day Target:**
- Reach [YY]th percentile
- Close [Z]% of gap to median
- Implement [X] best practices from top performers

**Strategic Recommendation:**
[2-3 paragraph narrative about strategic approach]

---
*Data sourced from anonymized aggregate of [X,XXX] campaigns across [XXX] companies in [Industry], [Date range]. Want deeper analysis? Run the campaign-audit skill for tactical optimization recommendations.*
```

## Supporting Files

This skill references:
- `data/industry-benchmarks.json` - Benchmark database
- `templates/peer-analysis.md` - Peer group definition template
- `examples/top-performer-patterns.md` - Best practices library
- `calculators/gap-impact.py` - Revenue impact calculator

Load these files from the skill directory when available.
