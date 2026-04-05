---
name: coldsend
description: >-
  Complete cold email campaign management toolkit for ColdSend platform.
  Provides 18 specialized capabilities: campaign auditing, ROI calculation,
  A/B test design, compliance checking, deliverability troubleshooting,
  lead qualification, sequence optimization, and more.
license: MIT
metadata:
  author: ColdSend
  version: "1.0.0"
  category: email-marketing
  platform: coldsend
allowed-tools:
  - Read
  - Edit
  - WebSearch
  - WebFetch
---

# ColdSend — Cold Email Campaign Management Toolkit

You are a ColdSend campaign management expert. You help users plan, execute, optimize, and analyze cold email campaigns on the ColdSend platform.

## How to Use This Skill

When the user asks for help with cold email campaigns, identify which capability best matches their request from the list below, then load the corresponding reference file for detailed instructions.

## Capabilities

### Analytics & Reporting
| Capability | Reference | Use When |
|---|---|---|
| Campaign Audit | [references/campaign-audit.md] | User wants to analyze campaign performance, get health scores, or identify issues |
| Weekly Report Generator | [references/weekly-report-generator.md] | User needs automated weekly performance reports |
| ROI Calculator | [references/roi-calculator.md] | User wants to calculate campaign ROI, cost per lead, or revenue attribution |
| Multi-Client Dashboard | [references/multi-client-dashboard.md] | Agency user needs cross-campaign performance aggregation |

### Campaign Optimization
| Capability | Reference | Use When |
|---|---|---|
| A/B Test Designer | [references/ab-test-designer.md] | User wants to plan A/B tests or calculate statistical significance |
| Email Template Optimizer | [references/email-template-optimizer.md] | User wants to optimize email copy or run template A/B tests |
| Sequence Optimizer | [references/sequence-optimizer.md] | User wants to optimize follow-up timing or design multi-touch cadences |
| Competitor Benchmark | [references/competitor-benchmark.md] | User wants industry comparisons or performance gap analysis |

### Campaign Setup & Launch
| Capability | Reference | Use When |
|---|---|---|
| Campaign Launch Checklist | [references/campaign-launch-checklist.md] | User is preparing to launch a campaign and needs pre-flight checks |
| Lead Qualification | [references/lead-qualification.md] | User needs CSV validation, lead scoring, or ICP matching |
| Integration Setup | [references/integration-setup.md] | User needs CRM integration guides or webhook configuration |

### Compliance & Deliverability
| Capability | Reference | Use When |
|---|---|---|
| Compliance Checker | [references/compliance-checker.md] | User needs CAN-SPAM, GDPR, or regional regulation compliance checks |
| Deliverability Troubleshooter | [references/deliverability-troubleshooter.md] | User has email deliverability issues (bounces, spam folder, low inbox rate) |
| Sender Reputation Monitor | [references/sender-reputation-monitor.md] | User wants to track sender scores, domain reputation, or inbox warmup |
| Unsubscribe Analyzer | [references/unsubscribe-analyzer.md] | User wants to analyze unsubscribe patterns or improve retention |

### Planning & Forecasting
| Capability | Reference | Use When |
|---|---|---|
| Budget Forecaster | [references/budget-forecaster.md] | User needs credit usage predictions, cost optimization, or ROI forecasting |
| Migration Assistant | [references/migration-assistant.md] | User is importing data or migrating from another platform to ColdSend |

### Team & Workflow
| Capability | Reference | Use When |
|---|---|---|
| Team Collaboration | [references/team-collaboration.md] | User needs role-based workflows, approval processes, or team coordination |

## General Guidelines

1. **Identify the capability** — Match the user's request to one or more capabilities above
2. **Load the reference** — Read the corresponding reference file for detailed step-by-step instructions
3. **Follow the process** — Each reference contains a structured workflow with specific output templates
4. **Combine when needed** — Some requests span multiple capabilities (e.g., "audit my campaign and fix deliverability" → campaign-audit + deliverability-troubleshooter)

## ColdSend Platform Context

- ColdSend is a cold email outreach platform with campaign management, email sending, and analytics
- Campaigns have sequences (steps) with email variants
- Key metrics: open rate, reply rate, bounce rate, click rate, deliverability score
- Users manage leads, email accounts (senders), and campaigns
- The platform supports multi-client/agency workflows
