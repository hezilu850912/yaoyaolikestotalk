# FA Report Section Generation Prompt

## Purpose

Use this prompt when converting user-provided FA materials into concise, complete report section descriptions.

Reference baseline:

- `../customer_training_issue_dri_jira_notes.md`

The training note is the primary formatting and content requirement source. Do not invent rules beyond it unless the user explicitly asks for rule extraction or refinement.

## Input Materials

The user may provide one or more of the following:

- PDF reports
- JIRA exports
- PPT files
- Excel data
- Images
- Test logs
- Manual notes
- Other supporting files

Treat all inputs as source evidence. If materials conflict, flag the conflict instead of silently choosing one.

## Output Goal

Generate concise but complete descriptions for each required FA report section.

The writing style should be:

- Brief but not vague
- Evidence-driven
- Customer-readable
- Professionally written in English unless the user requests Chinese or bilingual output
- Careful about uncertainty
- Free of unnecessary procedural detail
- Aligned with the customer training note

## Required Sections

Generate these sections when information is available:

1. Issue
2. DRI(s)
3. JIRA Ticket(s)
4. Risk
5. Description
6. Customer Failure Mode
7. Failure Analysis
8. Root Cause(s) / Leading Hypothesis
9. Containment Action(s)
10. Corrective Action(s)
11. Preventive Action(s)
12. Next Steps & Dates
13. Factory Risk Assessment
14. Field Exposure Risk Assessment

If a section lacks enough information, output `Missing / Need confirmation` with specific questions.

## Section Guidance

### Issue

- Base the title on the original test failure or customer complaint.
- Align the issue title with the corresponding JIRA title when available.
- Keep the title concise.
- If multiple issues are consolidated, use the shared commonality as the title.

### DRI(s)

- Include functional team and full name when available.
- Include both issue reporter and designated issue owner when available.
- If only partial DRI information is available, preserve what is known and ask for missing team/name/role.

### JIRA Ticket(s)

- Include labcollab JIRA links or IDs when available.
- If multiple JIRAs exist, identify the master JIRA if available.
- If no JIRA is provided, ask for it.

### Risk

- Do not equate severity with risk.
- Risk should follow the available color-code definition.
- Connect risk assessment to root cause, corrective action, validation state, and remaining exposure.
- If root cause or solution is not confirmed, reflect that uncertainty clearly.

### Description

Include available facts such as:

- Discovery date
- Shift or time period
- Discovery station or test station
- Production line number
- Daily defect rate or failure rate with calculation base
- Repeatability for intermittent issues
- First symptom using objective wording
- Affected product model/SKU
- Affected material information
- Whether the problem has been contained
- Current disposition

### Customer Failure Mode

- Describe what the end user would experience.
- Do not simply restate the factory test failure.
- Focus on functional, performance, or cosmetic customer impact.

### Failure Analysis

- Emphasize findings and conclusions rather than detailed procedural steps.
- Use specific measurements, percentages, statistical data, and comparisons when available.
- Prefer Good vs. Failed, Before vs. After, or Supplier A vs. Supplier B comparisons when supported.
- Mention images or annotations only when they support key findings.
- If supplier FA is provided, keep it as a separate subsection.

#### Failure Analysis Logic Writing

- Each FA sentence should follow a fixed evidence pattern:
  - `Performed [action/test]; [result] was observed.`
  - `Compared [A] with [B]; [difference] confirmed [conclusion].`
  - `Measured [parameter]; [value/trend] indicated [finding].`
  - `Verified [condition/hypothesis]; [result] supported or excluded [cause].`
- Keep every FA sentence concise and evidence-based.
- Avoid listing every procedural branch in the final customer report.
- Extract the main logic line from all FA evidence, such as `A -> B -> C -> Root Cause`.
- Keep side-branch FA evidence only when it supports a key link in the main logic line or excludes an important alternative cause.
- If one conclusion requires multiple supporting branches, express it as combined evidence, such as `A -> B` and `D -> B`.
- If external research is allowed by the user, use it only to supplement technical reasoning, identify plausible mechanisms, or check whether a logic link is reasonable. External research must not replace actual FA evidence.
- Output a logic map or Mermaid flowchart when FA logic is complex.

### Root Cause(s) / Leading Hypothesis

- Root cause must logically connect to FA evidence and directly drive corrective action.
- If root cause is not confirmed, state a leading hypothesis and next verification actions.
- Keep root cause concise, ideally 20-50 words.
- If existing controls should have caught the defect, explain why they failed when evidence is available.

### Containment Action(s)

- Describe short-term or temporary actions used to prevent defective products from reaching customers and unblock builds.
- Include quarantine, screening, temporary inspection, sampling changes, hold shipment, or suspect lot actions when available.
- Include duration or end condition.
- Include deviation ID if containment uses deviation.
- Do not mix containment with long-term corrective action.

### Corrective Action(s)

- Describe long-term design, process, material, specification, or software changes that eliminate the failure mode.
- Include before vs. after rationale when available.
- Include preliminary verification steps and results.
- Include downstream impacts such as schedule, tooling, fixture, line modification, material lead time, or cost when available.
- Do not treat training, monitoring, or data collection alone as sufficient corrective action unless supported by the customer requirement.

### Preventive Action(s)

- Describe system-level improvements beyond the immediate issue.
- Focus on preventing similar issues across products, projects, or processes.
- Include lessons learned, cross-functional training, COE actions, or updates to standard processes when available.

### Next Steps & Dates

- Mandatory for RED and Yellow issues.
- Include next checkpoint and DRI(s) for each action.
- If dates or owners are missing, ask for them.

### Factory Risk Assessment

- Mandatory for RED issues and resolved issues with factory impact.
- Include yield impact, CTB impact, production efficiency, cost impact, scope, duration, and recovery timeline when available.
- Use concrete numbers and confidence intervals when available.

### Field Exposure Risk Assessment

- Mandatory for RED issues and resolved issues with factory impact.
- Include expected field DPPM with 95% CI upper limit when available.
- Include rationale and data support if customer impact is expected to be no/low.
- If risk is high, ask for more data before milestone or ship decision.

## Handling Missing Information

For each missing or weak section:

- State what is missing.
- Ask a specific question.
- Do not fabricate data.
- Do not overstate certainty.

Use this format:

```text
Missing / Need confirmation:
- [Section]: [specific missing item or question]
```

## Output Format

Default output format:

```markdown
## Issue
[Generated text or Missing / Need confirmation]

## DRI(s)
[Generated text or Missing / Need confirmation]

## JIRA Ticket(s)
[Generated text or Missing / Need confirmation]

...
```

If the user asks for a shorter review format, provide:

```markdown
## Draft Sections
[Only populated sections]

## Missing / Need Confirmation
[Questions grouped by section]
```

## Quality Bar

Before finalizing, check:

- Is each section short enough for an executive/customer report?
- Is every claim supported by source material?
- Are uncertainty and missing data clearly marked?
- Does Root Cause connect to Failure Analysis?
- Does Corrective Action address Root Cause?
- Does Containment prevent customer escape?
- Are Risk sections based on evidence, not only severity?
