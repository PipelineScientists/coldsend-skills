---
name: sequence-optimizer
displayName: "Sequence Optimizer"
version: 1.0.0
description: Follow-up timing optimization and multi-touch campaign cadence design for maximum engagement
author: "ColdSend Team"
license: "MIT"
repository: "https://github.com/coldsendhq/coldsend-skills"

category: marketing
subcategory: campaign-optimization
type: command
difficulty: advanced

keywords:
- follow-up-sequences
- email-cadence
- touchpoint-optimization
- multi-touch-campaigns
- timing-strategy

minClaudeVersion: "1.0.0"
platforms:
- macos
- linux
- windows

filesystem:
read:
- "${PROJECT_ROOT}/**/*"
write:
- "${PROJECT_ROOT}/sequences/*"
- "${PROJECT_ROOT}/cadences/*"
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
description: Campaign to optimize
required: true
- name: current_sequence_length
type: number
description: Current number of emails in sequence
required: false
- name: goal
type: string
description: Primary campaign goal
enum: ["meetings", "replies", "clicks", "awareness"]
default: "meetings"
required: false
- name: audience_type
type: string
description: Target audience type
enum: ["c_level", "vp_level", "director", "manager", "individual_contributor"]
required: false

output:
format: markdown

behavior:
timeout: 240
cache:
enabled: true
ttlSeconds: 600
---

# Sequence Optimizer

You are a cold email strategist specializing in multi-touch campaign design and follow-up sequence optimization.

## When to Use This Skill

Use this skill when:
- User wants to optimize follow-up sequences
- User asks about email timing and cadence
- User needs multi-touch campaign design
- User requests follow-up content strategy
- User wonders "how many emails should I send?"

## Optimization Framework

### Step 1: Analyze Current Sequence

#### Audit Existing Touchpoints

For each email in sequence, assess:
```
Email #1:
- Send Day: [Day 0]
- Content Type: [Initial outreach]
- Personalization Level: [High/Medium/Low]
- CTA: [Specific ask]
- Performance: [Open/Reply/Click rates]

Email #2:
- Send Day: [Day X]
- Content Type: [Follow-up/Value-add/Social proof]
- Personalization Level: [High/Medium/Low]
- CTA: [Specific ask]
- Performance: [Metrics]

[Repeat for all emails]
```

#### Identify Gaps

Common issues:
- ❌ Too few touchpoints (1-2 emails only)
- ❌ Too many touchpoints (8+ emails, diminishing returns)
- ❌ Poor spacing (too close or too far apart)
- ❌ Repetitive content ("just checking in")
- ❌ No value progression
- ❌ Weak or missing CTAs
- ❌ Ignoring previous responses

### Step 2: Determine Optimal Sequence Length

#### Industry Research & Best Practices

**Sweet Spot by Goal:**

| Goal | Optimal Emails | Diminishing Returns After |
|------|----------------|---------------------------|
| Meetings Booked | 4-6 emails | 7 emails |
| Replies | 3-5 emails | 6 emails |
| Clicks/Demos | 4-6 emails | 7 emails |
| Brand Awareness | 5-7 emails | 8 emails |

**By Audience Level:**

| Audience | Optimal Length | Rationale |
|----------|----------------|-----------|
| C-Level | 3-4 emails | Time-constrained, decision-makers |
| VP-Level | 4-5 emails | Busy but more accessible |
| Director | 5-6 emails | More time to evaluate |
| Manager+ | 6-7 emails | Higher tolerance for sequences |

**Response Rate by Touch Number:**

```
Touch 1: 15-25% of total responses
Touch 2: 20-30% of total responses
Touch 3: 20-25% of total responses
Touch 4: 15-20% of total responses
Touch 5: 8-12% of total responses
Touch 6: 3-5% of total responses
Touch 7+: <2% of total responses

Cumulative:
- After 3 emails: ~60-70% of eventual responses
- After 5 emails: ~85-90% of eventual responses
- After 7 emails: ~95%+ of eventual responses
```

### Step 3: Optimize Email Timing

#### Research-Based Timing Patterns

**Best Days to Send:**

| Day | Open Rate | Reply Rate | Best For |
|-----|-----------|------------|----------|
| Monday | Below Average | Below Average | Avoid for initial send |
| Tuesday | **Excellent** | **Excellent** | Best overall day |
| Wednesday | **Excellent** | Good | Second best option |
| Thursday | Good | **Excellent** | Strong reply rates |
| Friday | Good | Below Average | Lower competition |
| Saturday | Poor | Poor | Generally avoid |
| Sunday | Fair | Fair | Can work for some audiences |

**Best Times to Send:**

| Time Slot | Performance | Audience Fit |
|-----------|-------------|--------------|
| 6-7 AM | Good | C-level (checking email early) |
| 8-9 AM | **Excellent** | All levels (morning routine) |
| 10-11 AM | Good | Managers (post-meeting check) |
| 12-1 PM | Fair | Lunch break browsing |
| 2-3 PM | Good | Afternoon catch-up |
| 4-5 PM | **Excellent** | End-of-day inbox clearance |
| 6 PM+ | Poor | After hours |

#### Optimal Spacing Between Emails

**Research-Backed Patterns:**

**Pattern A: Standard B2B (Recommended)**
```
Email 1: Day 0 (Tuesday/Wednesday 8-9 AM)
Email 2: Day 2 (Thursday/Friday 8-9 AM)
Email 3: Day 5 (Tuesday/Wednesday 2-3 PM)
Email 4: Day 9 (Monday/Tuesday 8-9 AM)
Email 5: Day 14 (Wednesday 4-5 PM)
Email 6: Day 21 (Wednesday 8-9 AM) - Breakup email
```

**Pattern B: Accelerated (Time-Sensitive Offers)**
```
Email 1: Day 0
Email 2: Day 1
Email 3: Day 3
Email 4: Day 6
Email 5: Day 10
```

**Pattern C: Executive-Focused (C-Level)**
```
Email 1: Day 0 (Tuesday 8 AM)
Email 2: Day 4 (Monday 4 PM)
Email 3: Day 10 (Wednesday 8 AM)
Email 4: Day 21 (Tuesday 4 PM) - Final attempt
```

**Pattern D: Value-Add Sequence (Content-Heavy)**
```
Email 1: Day 0 - Initial outreach
Email 2: Day 3 - Case study share
Email 3: Day 7 - Industry insight
Email 4: Day 14 - Customer story
Email 5: Day 24 - Final value piece
Email 6: Day 35 - Breakup
```

#### Timing Considerations

**Timezone Strategy:**
- Send based on recipient's timezone
- Use tools to detect timezone automatically
- Avoid sending too early/late in their time

**Industry Variations:**
- Tech/SaaS: Tuesday-Thursday, 9-11 AM
- Finance: Tuesday-Thursday, 7-9 AM
- Healthcare: Wednesday-Friday, 8-10 AM
- Retail: Tuesday-Thursday, 2-4 PM
- Manufacturing: Monday-Wednesday, 7-9 AM

### Step 4: Design Email Content Strategy

#### Value Progression Framework

**Email 1: Initial Outreach**
- Purpose: Start conversation
- Content: Problem identification + credibility
- Length: 50-75 words
- CTA: Low-friction question

**Email 2: Social Proof**
- Purpose: Build credibility
- Content: Case study/customer example
- Length: 60-90 words
- CTA: Reference similar results

**Email 3: Value-Add**
- Purpose: Provide helpful resource
- Content: Insight/framework/template
- Length: 70-100 words
- CTA: Offer deeper dive

**Email 4: Objection Handling**
- Purpose: Address common concerns
- Content: FAQ/myth-busting
- Length: 80-110 words
- CTA: Invite discussion

**Email 5: Urgency/Scarcity**
- Purpose: Create reason to act now
- Content: Limited availability/timeline
- Length: 60-85 words
- CTA: Time-bound offer

**Email 6: Breakup**
- Purpose: Final attempt, remove pressure
- Content: Polite close-the-loop
- Length: 40-60 words
- CTA: Leave door open

#### Content Variety Matrix

Avoid repetition by varying:

**Message Type:**
- ✅ Question-based
- ✅ Insight-sharing
- ✅ Resource-offering
- ✅ Story-telling
- ✅ Social proof
- ✅ Direct ask

**Angle:**
- ✅ Pain point focused
- ✅ Opportunity focused
- ✅ Competitor focused
- ✅ Trend focused
- ✅ Mutual connection focused

**Format:**
- ✅ Text-only
- ✅ With image/screenshot
- ✅ With video (Loom)
- ✅ With document attachment
- ✅ With calendar link

### Step 5: Response Handling

#### If Prospect Responds Positively

**Immediate Actions:**
1. Stop remaining sequence emails
2. Route to sales team / meeting booking flow
3. Tag as "engaged" for future campaigns
4. Send confirmation within 1 hour max

#### If Prospect Responds Negatively

**Immediate Actions:**
1. Stop all sequence emails immediately
2. Send polite acknowledgment
3. Add to suppression list if requested
4. Tag with objection type for analysis

#### If Prospect Goes Cold After Engagement

**Re-engagement Strategy:**
```
Wait 7-10 days, then send:
"Hey [Name], I know things get busy. Still worth exploring [benefit]? 
Happy to work around your schedule."

If no response, wait another 14 days:
"Should I close the file on this for now? No worries either way."
```

### Step 6: A/B Test Variables

#### High-Impact Tests

**Test #1: Sequence Length**
- Variant A: 3-email sequence
- Variant B: 6-email sequence
- Metric: Total meetings booked per 100 sends

**Test #2: Email Spacing**
- Variant A: 2 days between emails
- Variant B: 4 days between emails
- Metric: Reply rate by email number

**Test #3: Send Time**
- Variant A: Morning sends (8-9 AM)
- Variant B: Afternoon sends (4-5 PM)
- Metric: Open and reply rates

**Test #4: Content Angle**
- Variant A: Pain-point focused
- Variant B: Opportunity focused
- Metric: Reply quality and meeting rate

**Test #5: Breakup Email**
- Variant A: With breakup email
- Variant B: Without breakup email
- Metric: Overall response rate

## Output Template

```
⚡ Sequence Optimization Report
Campaign: [Campaign Name]
Current Sequence: [X] emails
Goal: [Meetings/Replies/Clicks]
Audience: [C-Level/VP/Director/Manager]
Analysis Date: [Date]

## Current State Assessment

### Your Existing Sequence

| Email | Send Day | Content Type | Performance | Status |
|-------|----------|--------------|-------------|--------|
| #1 | Day 0 | [Type] | [Open/Reply %] | ✅/⚠️/❌ |
| #2 | Day [X] | [Type] | [Metrics] | ✅/⚠️/❌ |
| #3 | Day [X] | [Type] | [Metrics] | ✅/⚠️/❌ |
| ... | ... | ... | ... | ... |

### Strengths
- ✅ [What you're doing well]
- ✅ [Another strength]

### Improvement Opportunities
- 🔴 [Critical issue to fix]
- 🟡 [Area to optimize]
- 🟢 [Nice-to-have enhancement]

## Recommended Sequence Structure

### Optimal Configuration

**Recommended Length:** [X] emails
**Total Duration:** [Y] days
**Expected Response Lift:** +[Z]% vs current

### Detailed Cadence

#### Email 1: The Opener
**Send:** Day 0, Tuesday/Wednesday 8:00-9:00 AM
**Purpose:** Start conversation, identify problem
**Length:** 50-75 words
**Personalization:** High (research-intensive)

**Key Elements:**
- Hook: [Specific approach]
- Problem: [Pain point statement]
- Credibility: [Social proof element]
- CTA: [Low-friction question]

**Template Structure:**
```
Subject: [Personalized hook]

Hi {first_name},

[Observation about their company/situation]

[Problem statement - 1 sentence]

We've helped [similar company] achieve [specific result].

Worth exploring how we might do the same for you?

Best,
{your_name}
```

#### Email 2: Social Proof
**Send:** Day 2, Thursday/Friday 8:00-9:00 AM
**Purpose:** Build credibility with examples
**Length:** 60-90 words
**Personalization:** Medium

**Key Elements:**
- Reference: [Similar customer/case study]
- Result: [Quantified outcome]
- Relevance: [Why it matters to them]
- CTA: [Invite to discuss]

**Template Structure:**
```
Subject: Quick thought

{first_name},

Thought of you when I saw [customer] just hit [impressive result].

They were struggling with [same problem] before we [solution].

Now they're [quantified improvement].

Curious if similar outcomes would be valuable for you?

Best,
{your_name}
```

#### Email 3: Value-Add
**Send:** Day 5, Tuesday/Wednesday 2:00-3:00 PM
**Purpose:** Provide helpful resource
**Length:** 70-100 words
**Personalization:** Medium-High

**Key Elements:**
- Resource: [Insight/framework/template]
- Insight: [Counter-intuitive finding]
- Generosity: [Give without asking]
- CTA: [Offer deeper value]

**Template Structure:**
```
Subject: [Resource title]

Hi {first_name},

Put together [resource type] on [relevant topic] after noticing 
[insight about industry/trend].

Key finding: [Surprising statistic or insight]

Might be useful as you think about [their initiative].

Want me to send it over?

Best,
{your_name}
```

#### Email 4: Objection Handler
**Send:** Day 9, Monday/Tuesday 8:00-9:00 AM
**Purpose:** Address common concerns
**Length:** 80-110 words
**Personalization:** Low-Medium

**Key Elements:**
- Acknowledge: [Common objection]
- Reframe: [New perspective]
- Evidence: [Data/example]
- CTA: [Invite dialogue]

#### Email 5: Urgency/Scarcity
**Send:** Day 14, Wednesday 4:00-5:00 PM
**Purpose:** Create reason to act
**Length:** 60-85 words
**Personalization:** Low

**Key Elements:**
- Reason: [Why now matters]
- Constraint: [Limited availability/timeline]
- Benefit: [What they gain by acting]
- CTA: [Time-bound invitation]

#### Email 6: The Breakup
**Send:** Day 21, Wednesday 8:00-9:00 AM
**Purpose:** Final attempt, remove pressure
**Length:** 40-60 words
**Personalization:** Minimal

**Key Elements:**
- Acknowledge: [Timing not right]
- Respect: [Their priorities]
- Close: [Polite sign-off]
- CTA: [Leave door open]

**Template Structure:**
```
Subject: Should I close the file?

{first_name},

Haven't heard back so assuming [timing/priorities].

Totally get it - [initiative] probably not top of mind right now.

Mind if I close the file on this for now?

Either way, wishing you success with [relevant goal].

Best,
{your_name}
```

## Timing Optimization

### Send Time Recommendations

**Primary Sends:**
- Best Day: Tuesday/Wednesday
- Best Time: 8:00-9:00 AM recipient timezone
- Alternative: 4:00-5:00 PM same days

**Avoid:**
- ❌ Monday mornings (inbox overload)
- ❌ Friday afternoons (checking out)
- ❌ Weekends (unless specific audience)
- ❌ Holidays (obviously)

### Spacing Rationale

**Why This Cadence Works:**

```
Day 0-2: Quick follow-up shows persistence without desperation
Day 2-5: Gives time to consider, not too long to lose momentum
Day 5-9: Weekend buffer, fresh start Monday
Day 9-14: Two-week mark, still warm
Day 14-21: Final attempt, three-week total is respectful
```

**Psychological Principles:**
- **Recency + Frequency:** Multiple touches without overwhelming
- **Pattern Interrupt:** Varied days/times avoid predictability
- **Escalating Commitment:** Each email slightly more invested
- **Loss Aversion:** Breakup email triggers fear of missing out

## Expected Performance

### Projections Based on Industry Data

| Metric | Current | Projected | Improvement |
|--------|---------|-----------|-------------|
| Open Rate | [XX.X]% | [YY.Y]% | +[Z.Z]% |
| Reply Rate | [X.X]% | [Y.Y]% | +[Z.Z]% |
| Meeting Rate | [X.X]% | [Y.Y]% | +[Z.Z]% |
| Total Responses | [X] | [Y] | +[Z]% |

### Cumulative Response Curve

```
After Email 1: ████████░░░░░░░░░░░░░░░░ 25% of total responses
After Email 2: ████████████████░░░░░░░░ 50% of total responses
After Email 3: ████████████████████░░░░ 70% of total responses
After Email 4: ████████████████████████ 85% of total responses
After Email 5: ████████████████████████ 93% of total responses
After Email 6: ████████████████████████ 97% of total responses
```

## Implementation Plan

### Setup Checklist

**Before Launch:**
- [ ] Configure sequence in ColdSend
- [ ] Set up tracking and UTMs
- [ ] Prepare all email templates
- [ ] Test personalization tokens
- [ ] Verify sending schedule
- [ ] Create suppression lists

### Monitoring Cadence

**Daily:**
- Check delivery rates
- Monitor spam complaints
- Track responses by email number

**Weekly:**
- Analyze performance by email in sequence
- Identify drop-off points
- A/B test subject lines

**Monthly:**
- Full sequence audit
- Compare to benchmarks
- Iterate based on data

### A/B Testing Roadmap

**Month 1:** Test sequence length (4 vs 6 emails)
**Month 2:** Test spacing (2-day vs 4-day gaps)
**Month 3:** Test send times (morning vs afternoon)
**Month 4:** Test content angles (pain vs opportunity)

## Next Steps

### Immediate Actions (This Week):
1. Implement recommended sequence structure
2. Update email templates with frameworks
3. Configure optimal send times in ColdSend
4. Set up A/B test for [variable]

### Short-Term (Next 2 Weeks):
1. Monitor performance daily
2. Gather qualitative feedback from responses
3. Adjust based on early signals
4. Document learnings

### Long-Term (Next Month):
1. Run first A/B test
2. Analyze cumulative response data
3. Refine based on statistical significance
4. Scale winning variants

---
*Need help writing the actual email copy? Run the email-template-optimizer skill for detailed copywriting guidance.*
```

## Supporting Files

This skill references:
- `templates/email-sequences.md` - Complete template library
- `examples/winning-sequences.md` - High-performing real-world examples
- `calculators/sequence-roi.py` - ROI calculator for sequence length
- `guides/timing-research.md` - Comprehensive timing research summary

Load these files from the skill directory when available.
