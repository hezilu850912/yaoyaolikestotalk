# Company 8D Report Workflow

## Purpose

Convert raw issue materials into a company-style 8D report using `yaoyao_like_to_talk` practical English.

Use these files:

- `../prompts/yaoyao_like_to_talk_8d_prompt.md`
- `../templates/company_8d_report_template.md`
- `../customer_training_issue_dri_jira_notes.md`
- `../docs/input_to_report_workflow.md`

## Input Materials

Accepted inputs:

- Original FA report
- JIRA export
- Supplier report
- PPT/PDF/Excel/image evidence
- Test logs
- Manual notes
- Existing 8D report draft
- User-corrected examples

Company format examples show:

- D1: Team table
- D2: 5W + How Many + JIRA + Finding
- D3: Containment action table with status/owner/date
- D4: Root cause analysis with investigation progress, conclusion, and optional fishbone logic
- D5: Corrective action list/table with owner/status/date
- D6: Verification or preventive action depending on template version
- D7: Preventive action in the generated Markdown for clearer D1-D7 structure

## Step 1: Extract Basic Fields

Extract:

- Project / issue name
- Date and time
- Station / line / process
- Failure symptom
- Failure quantity and total quantity
- DPPM / failure rate
- JIRA ID
- Owner / DRI
- Affected lot, SKU, material, supplier, WIP, inventory

Do not fabricate missing fields.

## Step 2: Build D2 Problem Description

Use 5W + How Many:

```text
When:
Who:
Where:
What:
How Many:
JIRA:
Finding:
```

Keep D2 factual. Do not explain root cause here.

Good D2 style:

```text
When: 2026/03/11
Who: OP
Where: VI3 station
What: Device temple-R inner and outer gap over spec (spec: 0~0.1 mm, actual >0.15 mm)
How Many: 10% (3F/30T)
JIRA: AMELIA-12434
Finding: Gap was over spec and bonding glue was uncured. The glue was soft and could be peeled off from the housing.
```

## Step 3: Build D3 Containment

D3 should answer:

- What was done immediately?
- What scope was covered?
- Was production stopped or resumed?
- Who owns it?
- Is it done or ongoing?
- When was it completed?

Use table:

```markdown
| No. | Containment Action | Status | Owner | Date |
|---|---|---|---|---|
```

## Step 4: Build D4 Root Cause Analysis

D4 should include:

- Investigation progress
- Key evidence
- Excluded causes
- Root cause conclusion
- Optional fishbone/logic categories

Preferred sentence format:

```text
Checked [item/process]; [result] was found.
Reviewed [record/data]; [result] was confirmed.
Reproduced [condition]; [failure mode] was confirmed.
Verified [hypothesis]; [result] supported/excluded [cause].
```

Root cause can be split:

```text
Occurrence Root Cause:
Escape Root Cause:
Systemic Root Cause:
```

If a fishbone is needed, group by:

```text
Manpower / Method / Machine / Material / Environment
```

## Step 5: Build D5 Corrective Action

D5 is the fix for this specific issue.

Examples:

```text
Standardized the punch stroke parameter at 10.8 mm and locked it into machine settings.
Adjusted the ink dilution ratio to keep the ink condition stable during production.
Modified robot placement from direct placement to a two-step sequence with a 0.02-second dwell time.
```

D5 must match D4. If D4 says the issue is parameter control, D5 must define and lock the parameter. If D4 says inspection cannot detect the defect, D5 must improve inspection method.

## Step 6: Build D6 Verification

D6 proves D5 worked.

Include:

- Method
- Sample size / scope
- Result
- Owner
- Date

Examples:

```text
Verified the updated process on 30 units; no gap-over-spec failure was found.
Supplier sorted 49,920 units in GTK VMI and 26,877 units in warehouse; no MIC_FR failure was found.
```

If the company source template uses D6 as Preventive Action, still generate `D6 Verification` in Markdown when verification data exists, and put prevention under D7.

## Step 7: Build D7 Preventive Action

D7 is standardization.

Good actions:

- Update SOP
- Update WI
- Update PFMEA
- Update Control Plan
- Add audit checklist
- Add training
- Add shift attendance / POR tracking
- Add lesson learned sharing

Keep D7 short.

```text
D5 = fixed this issue.
D7 = standardized to prevent recurrence.
```

## Step 8: Generate FA Logic Line and Flowchart

Always output:

```text
Problem -> Evidence -> Mechanism -> Root Cause -> Corrective Action
```

Generate Mermaid when:

- The cause path is complex.
- Occurrence and escape causes both exist.
- Fishbone logic is used.
- The user asks for a logic diagram.

## Step 9: Missing Information Check

Ask only specific questions.

Examples:

```text
- D1: Please provide team member responsibility and mail.
- D3: Please confirm containment completion date.
- D5: Please confirm owner and cut-in date.
- D6: Please provide verification sample size and result.
- D7: Please confirm whether SOP/WI/PFMEA/Control Plan were updated.
```

## Final Review

Before final output:

- D2 is factual.
- D3 protects customer/build immediately.
- D4 explains why the issue happened.
- D5 directly addresses D4.
- D6 proves D5 effectiveness.
- D7 standardizes prevention.
- Language is short and practical.
- No unsupported data is invented.
