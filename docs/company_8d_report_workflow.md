# Company 8D Report Workflow

Low-model friendly workflow. Use this with:

- `../prompts/yaoyao_like_to_talk_8d_prompt.md`
- `../templates/company_8d_report_template.md`

## Goal

Convert raw FA/JIRA/PDF/PPT/Excel/image/manual inputs into a company-style 8D Markdown report.

Output all D1-D7 sections. Do not output JSON.

## Step 1: Extract Facts

Extract only source-supported facts:

- Issue / failure symptom
- Date and time
- Station / line / process
- Who found it
- Failure quantity / total quantity / DPPM / failure rate
- JIRA ID
- Pictures / key findings
- Temporary actions
- Investigation evidence
- Root cause
- Corrective action
- Verification result
- Preventive action
- Owner / status / date

Do not invent missing data.

## Step 2: Fill D1-D7

### D1 Team Building

Table:

```text
Function | Name | Department | Responsibility | Mail
```

### D2 Problem Description

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

D2 is facts only. Do not write root cause here.

### D3 Containment Action

Temporary protection:

```text
No. | Containment Action | Status | Owner | Date
```

Examples: stop line, quarantine, 100% screen, add temporary manpower, hold shipment.

### D4 Root Cause Analysis

Use:

```text
Investigation Progress:
1. Checked / reviewed / tested / reproduced ...; result ...

Root Cause Conclusion:
Occurrence Root Cause:
Escape Root Cause:
Systemic Root Cause:
```

Each FA sentence must be action + result.

Root cause must explain why.

### D5 Corrective Action

Permanent fix for this issue:

```text
No. | Corrective Action | Owner | Due Date | Status
```

D5 must match D4.

### D6 Verification / Effectiveness Check

Proof that D5 worked:

```text
No. | Verification Method | Sample Size / Scope | Result | Owner | Date
```

Include sample size and result when available.

### D7 Preventive Action

Standardization to prevent recurrence:

```text
1. Update SOP / WI / PFMEA / Control Plan.
2. Add audit checklist / shift tracking.
3. Conduct training.
```

D7 should not repeat D5 details.

## Step 3: Add FA Logic

Always output:

```text
Problem -> Evidence -> Mechanism -> Root Cause -> Corrective Action
```

If logic is complex, add Mermaid flowchart.

## Step 4: Missing Information

Ask specific questions only:

```text
- D1:
- D2:
- D3:
- D4:
- D5:
- D6:
- D7:
```

## Final Check

- All D1-D7 sections are present.
- Markdown only.
- No JSON.
- No raw_output.
- Short and complete.
- D4 matches D5.
- D6 verifies D5.
- D7 prevents recurrence.
