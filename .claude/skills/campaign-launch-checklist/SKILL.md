---
name: campaign-launch-checklist
displayName: "Campaign Launch Checklist"
version: 1.0.0
description: Pre-launch verification checklist to ensure successful cold email campaign deployment
author: "ColdSend Team"
license: "MIT"
repository: "https://github.com/coldsendhq/coldsend-skills"

category: marketing
subcategory: campaign-management
type: command
difficulty: beginner

keywords:
- campaign-launch
- pre-flight-checklist
- deliverability
- quality-assurance
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
- "${PROJECT_ROOT}/checklists/*"
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
- name: campaign_name
type: string
description: Campaign to verify before launch
required: true
- name: checklist_type
type: string
description: Depth of verification
enum: ["quick", "standard", "comprehensive"]
default: "standard"
required: false

output:
format: markdown

behavior:
timeout: 180
cache:
enabled: true
ttlSeconds: 600
---

# Campaign Launch Checklist

You are a deliverability expert ensuring campaigns are set up for success before launch.

## When to Use This Skill

Use this skill when:
- User is about to launch a new campaign
- User asks "is my campaign ready?"
- User wants pre-launch verification
- User needs deliverability best practices
- User requests quality assurance review

## Pre-Launch Verification Framework

### Level 1: Quick Checklist (5 minutes)
Essential checks before any send:

#### ✅ Domain & Authentication
- [ ] Domain added to ColdSend
- [ ] DNS records configured (SPF, DKIM, DMARC)
- [ ] Domain verification completed
- [ ] Custom tracking domain setup (optional but recommended)

#### ✅ Sender Inboxes
- [ ] At least 1 sender inbox configured
- [ ] Inbox connection tested successfully
- [ ] Daily sending limits set appropriately
- [ ] Warmup status checked (if new inbox)

#### ✅ Campaign Content
- [ ] Subject line written (<60 characters ideal)
- [ ] Email body under 100 words
- [ ] Clear CTA included
- [ ] Unsubscribe link enabled (automatic in ColdSend)
- [ ] No spam trigger words ("free", "guaranteed", etc.)

#### ✅ Lead List
- [ ] CSV uploaded with valid emails
- [ ] Minimum 50 leads for meaningful test
- [ ] Duplicates removed
- [ ] Role-based emails excluded (info@, support@)

### Level 2: Standard Checklist (15 minutes)
Recommended for all campaigns:

#### ✅ Technical Setup
**Domain Health:**
- [ ] SPF record includes ColdSend/Azure
- [ ] DKIM selector configured
- [ ] DMARC policy set to p=none or p=quarantine
- [ ] No DNS errors in ColdSend dashboard
- [ ] Domain age >30 days (or warmed up properly)

**Inbox Configuration:**
- [ ] Sending from professional domain (not gmail.com)
- [ ] Inbox has profile photo and signature
- [ ] Reply-to address monitored daily
- [ ] Bounce handling configured
- [ ] Unsubscribe processing enabled

**Tracking & Analytics:**
- [ ] Open tracking enabled
- [ ] Click tracking enabled
- [ ] Goal conversion tracking setup (if applicable)
- [ ] UTM parameters added to links (recommended)

#### ✅ Content Quality
**Subject Line:**
- [ ] Under 60 characters (mobile-friendly)
- [ ] Personalization token used ({first_name}, {company})
- [ ] Creates curiosity or states value
- [ ] No spam triggers
- [ ] Tested on spam checker tool

**Email Body:**
- [ ] Starts with recipient-focused hook
- [ ] Conversational tone (reads like human wrote it)
- [ ] Short paragraphs (2-3 sentences max)
- [ ] One clear CTA
- [ ] Mobile preview looks good
- [ ] Links work and go to correct URLs
- [ ] No attachments (spam trigger)

**Personalization:**
- [ ] Merge tags match CSV column names
- [ ] Fallback values set for optional fields
- [ ] Company/industry research done for top segments
- [ ] Variable testing configured (if using A/B tests)

#### ✅ Audience & Timing
**Lead Quality:**
- [ ] All leads fit ICP (Ideal Customer Profile)
- [ ] Leads scored A/B tier minimum
- [ ] Enriched with first name + company
- [ ] Segmented by relevant criteria

**Sending Schedule:**
- [ ] Start date set (avoid Mondays/Fridays for B2B)
- [ ] Send time optimized for timezone (9-11 AM ideal)
- [ ] Daily limits respect inbox reputation
- [ ] Follow-up sequence spaced appropriately (3-5 days)

**Compliance:**
- [ ] CAN-SPAM compliance (physical address in footer)
- [ ] GDPR considerations reviewed (EU prospects)
- [ ] No purchased lists (only opted-in or researched leads)
- [ ] Suppression list applied (existing customers, competitors)

### Level 3: Comprehensive Checklist (30 minutes)
For high-stakes campaigns:

#### ✅ Advanced Deliverability
**Domain Reputation:**
- [ ] Google Postmaster Tools monitoring setup
- [ ] Microsoft SNDS monitoring setup
- [ ] No blacklist appearances checked
- [ ] Previous sending history clean

**Inbox Warmup:**
- [ ] New inboxes warmed up 7-14 days
- [ ] Gradual volume increase planned
- [ ] Engagement rate >40% during warmup
- [ ] No spam complaints during warmup

**ESP-Specific Optimization:**
- [ ] Gmail: Low promotional tab placement tactics
- [ ] Outlook: Avoid image-heavy content
- [ ] Yahoo: Strict authentication requirements met
- [ ] Corporate domains: Identified major ESPs in list

#### ✅ Content Optimization
**A/B Testing Plan:**
- [ ] Test hypothesis documented
- [ ] Sample size calculated for significance
- [ ] Primary metric defined (opens/replies/meetings)
- [ ] Test duration planned (5-7 days minimum)
- [ ] Variant differences substantial enough to matter

**Copy Review:**
- [ ] Value proposition clear in first 2 sentences
- [ ] Social proof included (logos, stats, testimonials)
- [ ] Objection handling addressed
- [ ] Urgency/scarcity authentic (not fake)
- [ ] Tone matches brand voice
- [ ] Grammar/spelling perfect
- [ ] Read aloud test passed (sounds natural)

**Link & Landing Page Audit:**
- [ ] All links use HTTPS
- [ ] No URL shorteners (bit.ly, tinyurl)
- [ ] Landing page mobile-optimized
- [ ] Landing page load time <3 seconds
- [ ] Clear next step on landing page
- [ ] Conversion tracking pixel installed

#### ✅ Risk Mitigation
**Contingency Planning:**
- [ ] Spam complaint monitoring alerts set
- [ ] Bounce rate threshold alerts (>5%)
- [ ] Unsubscribe spike detection (>2% per send)
- [ ] Backup sending domains ready
- [ ] Pause plan if metrics tank

**Monitoring Cadence:**
- [ ] First 24 hours: Check every 4 hours
- [ ] Days 2-7: Daily check-ins
- [ ] Week 2+: Weekly performance reviews
- [ ] Monthly: Comprehensive audit

## Risk Assessment Matrix

Rate each category 🟢 Good / 🟡 Caution / 🔴 Stop

| Category | Status | Notes |
|----------|--------|-------|
| Domain Health | 🟢 | All DNS records configured |
| Inbox Reputation | 🟡 | New inbox, needs warmup |
| Content Quality | 🟢 | Reviewed and optimized |
| Lead Quality | 🟢 | A/B tier leads only |
| Compliance | 🟢 | CAN-SPAM compliant |
| **Overall** | 🟡 | **Proceed with caution** |

## Output Template

```
✅ Campaign Launch Checklist
Campaign: [Campaign Name]
Review Date: [Date]
Checklist Level: [Quick/Standard/Comprehensive]

## Summary

**Overall Readiness:** 🟢 Ready / 🟡 Proceed with Caution / 🔴 Not Ready

**Passed:** [X]/[Y] checks
**Warnings:** [X] items
**Critical Issues:** [X] blockers

## ✅ What's Good

[List what's already working well]

## ⚠️ Warnings (Fix Before Launch)

1. **[Issue Title]**
   - Problem: [Description]
   - Impact: [What could go wrong]
   - Fix: [Specific action required]
   - Priority: High/Medium/Low

2. **[Issue Title]**
   [Repeat structure]

## 🔴 Critical Blockers (MUST FIX)

1. **[Blocker Title]**
   - Problem: [Description]
   - Why it blocks launch: [Explanation]
   - Fix: [Required action]
   - Time to fix: [Estimate]

## Recommended Timeline

### If addressing warnings:
- Fix critical blockers: [X] hours
- Implement warnings fixes: [Y] hours
- Re-run checklist: [Z] hours
- **Ready to launch:** [Date/Time]

### If all green:
- **Launch immediately**
- Monitor closely for first 24 hours

## Monitoring Plan

### First 24 Hours:
- Check delivery rate every 4 hours
- Monitor spam complaints
- Track open rate trajectory

### First Week:
- Daily performance reviews
- A/B test analysis (if running)
- Adjust sending based on engagement

## Final Go/No-Go Decision

**Recommendation:** GO / NO-GO

**Reasoning:** [Brief explanation]

**Next Review:** [Date/time for follow-up]
```

## Supporting Files

This skill references:
- `validation/dns-records.md` - DNS configuration guide
- `templates/spam-checker.md` - Content review checklist
- `examples/warmup-schedule.md` - Inbox warmup timeline

Load these files from the skill directory when available.
