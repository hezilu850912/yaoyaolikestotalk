# Input to FA Report Workflow

## Purpose

This workflow converts raw FA inputs into a concise, customer-readable FA report Markdown file.

It should use:

- `../customer_training_issue_dri_jira_notes.md` as the customer section requirement baseline.
- `../prompts/section_generation_prompt.md` as the report generation prompt.
- `../templates/standard_fa_report.md` as the default Markdown output structure.

The target style is practical factory-engineer English: simple, clear, evidence-based, and easy for customer SQE teams to understand. Do not over-polish into vague consulting language.

## 1. Input Collection

Accepted source materials:

- Original FA reports
- JIRA exports
- PDF reports
- PPT files
- Excel data
- Images
- Test logs
- Manual notes
- Supplier FA reports
- User-corrected final report examples
- External research references when explicitly allowed

Treat user-corrected final reports as high-value style references. They show the preferred wording, logic depth, and section length.

## 2. Evidence Extraction

Extract only source-supported facts:

- Issue title, JIRA ID, DRI, risk color
- Failure symptom and customer complaint
- Date, station, line, test condition, failure quantity, total quantity, DPPM, failure rate
- Customer-visible failure mode
- FA evidence, measurements, pictures, process mapping, teardown results, DOE results, reproduction tests
- Good vs. failed comparison
- Supplier findings and supplier process information
- Occurrence root cause and escape root cause
- Containment, corrective, and preventive actions
- Factory risk and field exposure risk data

If evidence conflicts, flag the conflict and ask for confirmation.

Do not fabricate missing numbers, dates, quantities, DRI names, JIRA IDs, validation sample sizes, or risk conclusions.

## 3. Raw Report to Final Report Conversion

Raw reports often contain long process descriptions, repeated details, weak conclusions, or mixed D5/D7 actions. Convert them into concise report sections.

### Keep

- Key evidence that supports the main FA logic.
- Quantitative data such as DPPM, failure rate, sample size, measurement value, specification, yield impact, and CI.
- Reproduction evidence.
- Process mapping evidence.
- Evidence that excludes a major alternative cause.
- Owner, date, checkpoint, and completion status.

### Remove or Compress

- Repeated wording.
- Long procedural history.
- Side branches that do not support FA -> RC -> CA.
- General statements such as "we checked and found issue" without result.
- Training/monitoring/data collection when presented as the only corrective action.
- Overly complex English when simple wording is clearer.

## 4. Practical English Style

Use simple, direct wording. Prefer words like:

```text
found
checked
confirmed
verified
blocked
remained
caused
not cleaned in time
not fully removed
not fully seated
became trapped
was difficult to detect
```

Avoid unnecessarily fancy wording when factory English is clearer.

Examples:

```text
Rubber residue around the mold gate was not cleaned in time.
The residue blocked material flow and caused short shot.
Fibers remained on the product surface before coating and became trapped after coating.
The PCBA was not fully seated on the positioning columns.
Residual material inside the MIC hole was difficult to detect under reflective lighting conditions.
```

## 5. Defect Term Preference

For printing and appearance defects, use customer-readable terms:

```text
毛丝: ink stringing / stringing defect / ink filament
异色: color variation / color mismatch / color deviation
锯齿: jagged edge / saw-tooth edge
```

Preferred report wording:

```text
Printing defect including color variation, ink stringing, and jagged edge appearance.
Logo printing showed color deviation, ink stringing, and jagged edges.
```

Use `burr` only when the defect is a physical burr from molding, cutting, stamping, or insert mismatch. Use `ink stringing` when it is ink filament during printing.

## 6. FA Sentence Normalization

Failure Analysis should use concise fixed-format evidence statements.

Preferred sentence patterns:

```text
Checked [item/process]; [result] was found.
Performed [action/test]; [result] was observed.
Compared [A] with [B]; [difference] confirmed [conclusion].
Measured [parameter]; [value] was [within/out of] specification.
Reviewed [record/process]; [source process or timing] was identified.
Reproduced [condition]; [failure mode] was confirmed.
Verified [hypothesis]; [result] supported [cause].
Verified [hypothesis]; [result] excluded [alternative cause].
```

Good examples:

```text
Checked the log; MIC_FR failed and the test value was below the lower limit.
Disassembled the device; the rubber was found blocked in the MIC hole.
Process mapping identified the punching process as the most likely source.
Reproduction testing confirmed that insufficient punch stroke resulted in incomplete punching and residual material remaining in the MIC hole.
Inspection simulation confirmed that residual material inside the MIC hole was difficult to detect under reflective lighting conditions.
```

Avoid weak FA wording:

```text
FA did process mapping and reproduced this issue.
We checked the product and found some problems.
The issue may be caused by production.
```

Rewrite weak wording:

```text
Process mapping identified the front housing + PCBA assembly process as the source.
Reproduction testing confirmed that when the PCBA was not fully seated on the positioning columns, the battery spring became deformed during mid-frame assembly.
```

## 7. Logic Chain Construction

Build a main logic chain:

```text
Failure symptom -> FA evidence -> process/mechanism -> root cause -> corrective action
```

The root cause should not simply restate the symptom. It should explain why the failure happened.

Weak root cause:

```text
UPH increase caused unstable PCBA assembly.
```

Better root cause:

```text
After the assembly UPH was increased, robot placement speed was accelerated. The PCBA was placed directly onto the positioning columns without sufficient stabilization time, allowing positional shift during placement and resulting in battery spring deformation during subsequent assembly.
```

Logic chain:

```text
UPH increased
-> robot placement speed increased
-> PCBA was placed without sufficient stabilization time
-> PCBA shifted away from positioning columns
-> battery spring deformed during mid-frame assembly
-> Battery Terminal Fail
```

If one conclusion requires multiple evidence paths, keep both:

```text
A -> B
D -> B
B -> C -> Root Cause
```

## 8. Branch Filtering

Keep a side branch only if it does one of the following:

- Supports a key link in the main logic chain.
- Provides required evidence for a conclusion.
- Excludes a major alternative cause.
- Explains why existing controls failed.
- Is required for risk, containment, CA, PA, or next steps.

Do not include side branches in the final customer report if they are only procedural background.

Example:

```text
Main branch:
Ink condition changed during production -> ink spread more easily -> color variation and jagged edges occurred.

Supporting branch:
Fibers and dust were found around the printing area -> contaminants remained on the product surface -> ink stringing occurred after printing.

Exclude branch:
Ink and fixture were checked and no issue was found.
```

## 9. Root Cause Writing

Split root cause when needed:

- Occurrence Cause: why the defect happened.
- Escape Cause: why it was not detected before escape.
- Systemic Root Cause: why the process system allowed the risk.

Use Occurrence Cause and Escape Cause when the original report or issue type supports it.

Examples:

```text
Occurrence Cause:
Rubber residue around the mold gate was not cleaned in time, causing material flow blockage and resulting in short shot.

Escape Cause:
Visual inspection depended on manual checking, and some defect locations were missed.

Systemic Root Cause:
The impact of UPH increase on robot placement stability was not evaluated during process change validation.
```

If root cause is not confirmed, write a leading hypothesis and list next verification actions.

## 10. Action Classification

Separate D5, D7, and next steps clearly.

### Containment Action

Short-term action to prevent customer escape or unblock build.

Examples:

```text
BQ 100% screened all WIP inventory; screening was completed on 2026-05-17.
Supplier sorted all old material in FATP, GTK VMI, and warehouse; no failure was found.
```

### Corrective Action

Long-term fix for the specific failure mode.

Examples:

```text
Modified robot placement motion from direct placement to a two-step placement sequence. A 0.02-second dwell time was added at the midpoint of the placement path to allow PCBA stabilization before final seating onto the positioning columns.

The stroke parameter was standardized at 10.8 mm and locked into machine settings.

Adjusted the ink dilution ratio to keep the ink condition stable during production.
```

### Preventive Action

System-level standardization to prevent recurrence or similar issues.

Keep it short. D7 should not repeat D5 details.

Examples:

```text
Update molding SOP and define mold cleaning frequency.
Update coating SOP and define lint-free cloth replacement frequency.
Update visual inspection WI and define inspection sequence and defect criteria.
Update PFMEA and Control Plan to include short shot and fiber contamination risks.
Conduct operator and inspector training.
```

Rule of thumb:

```text
D5 = what was fixed for this issue.
D7 = what was standardized to prevent recurrence.
```

## 11. Section-Level Lessons from Good Examples

### Material Short and Fiber Issue

Good structure:

```text
Failure Analysis:
1. Short shot and fiber contamination were found on the button surface.
2. Process review confirmed short shot occurred during molding, while fiber contamination was introduced before spray coating.
3. Mold inspection found resin residue remaining on the mold surface. The residue blocked material flow and caused incomplete filling in some areas.
4. Production area inspection found increased fibers and dust due to nearby fixture maintenance activities and strong airflow from the curing line.
5. Before spray coating, some fibers remained on the product surface because static electricity attracted airborne fibers. These fibers could not be completely removed and became trapped after coating.

Root Cause:
Short Shot: Resin residue remained on the mold surface and was not cleaned in time. The residue blocked normal material flow and caused incomplete filling.
Fiber: Fibers and dust in the production area were attracted to the product surface by static electricity. Some fibers remained before spray coating and became trapped after coating.
```

### Battery Terminal Issue

Good structure:

```text
Failure Analysis:
1. Failure mode was stable and reproducible. BAT terminal measurement was 0 mA while specification was 0.9~10 mA.
2. Product teardown confirmed battery terminal spring deformation.
3. SMT AOI records verified the spring was normal before assembly.
4. Process mapping identified the front housing + PCBA assembly process as the source.
5. Reproduction testing confirmed that when the PCBA was not fully seated on the positioning columns, the battery spring became deformed during mid-frame assembly.

Root Cause:
After the assembly UPH was increased, robot placement speed was accelerated. The PCBA was placed directly onto the positioning columns without sufficient stabilization time, allowing positional shift during placement and resulting in battery spring deformation during subsequent assembly.
```

### MIC Hole Punching Issue

Good structure:

```text
Failure Analysis:
1. Checked the log; MIC_FR failed and the test value was below the lower limit.
2. The failure mode was stable and reproducible on all test equipment.
3. Disassembled the device; the rubber was found blocked in the MIC hole.
4. Process mapping identified the punching process as the most likely contributor.
5. Reproduction testing confirmed that insufficient punch stroke resulted in incomplete punching and residual material remaining in the MIC hole.
6. Inspection simulation confirmed that residual material inside the MIC hole was difficult to detect under reflective lighting conditions.

Root Cause:
Occurrence Root Cause: The punch stroke was manually adjusted without a fixed parameter control, resulting in insufficient punch stroke and incomplete MIC hole punching.
Escape Root Cause: The inspection method was not robust enough to detect residual material inside the MIC hole due to reflective background conditions.
```

### Printing Stringing and Jagged Edge Issue

Good structure:

```text
Failure Analysis:
1. Ink and fixture were checked and no issue was found.
2. Process review confirmed that ink condition changed during production due to dilution adjustment.
3. When the ink became thinner, it spread more easily during printing, causing color variation and jagged edges.
4. Fibers and dust were found around the printing area.
5. Fibers remained on the product surface and caused stringing defects after printing.

Root Cause:
Jagged edge: During printing, the ink became thinner over time, which caused the ink to spread and resulted in color variation and jagged edges.
Artwork stringing: Fibers and dust were attached to the product surface before printing. These contaminants were not fully removed and caused stringing defects after printing.
```

## 12. Risk Assessment Writing

Use risk sections to explain impact with data. Do not confuse severity with risk.

Factory risk should include production impact when available:

- Yield impact
- CTB impact
- Production efficiency
- Cost impact
- Scope and duration

Good example:

```text
FATP risk is low because the action has been cut in and verified effective. Before action, the issue may cause yield impact. The projected yield impact is 0.0018% (up to 0.0057% with 95% confidence level).
```

Field exposure risk should explain escape risk with inspection coverage and field exposure data.

Good examples:

```text
Issue will not have field exposure risk.

Issue has multiple inspections in supplier, IQC, and FATP, so the risk to escape to field is low. No similar issue was reported in GTK IQC, FATP, or OBA.
```

If confidence interval, DPPM, or screening quantity is available, include it.

## 13. External Research

Use external research only when the user allows it.

Allowed uses:

- Supplement technical mechanism reasoning.
- Identify common failure mechanisms.
- Check whether a logic link is reasonable.
- Suggest missing verification tests.

Not allowed:

- Replacing actual FA evidence.
- Inventing root cause.
- Overriding source data.
- Citing unsupported claims as confirmed facts.

When using external research, separate it from confirmed FA evidence.

## 14. Report Generation

Generate a Markdown report using:

- `../prompts/section_generation_prompt.md`
- `../templates/standard_fa_report.md`
- `../customer_training_issue_dri_jira_notes.md`

Default output:

- Standard report sections
- Missing / Need confirmation list
- FA logic line
- Supporting branches
- Mermaid logic flowchart

The generated report should be concise enough to paste into a customer FA table.

## 15. Review Gate

Before finalizing:

- Confirm every claim is supported by source material.
- Confirm each FA sentence is concise and evidence-based.
- Confirm root cause explains why the failure happened, not only what happened.
- Confirm root cause connects to FA evidence.
- Confirm corrective action addresses root cause.
- Confirm containment prevents customer escape.
- Confirm preventive action standardizes the lesson learned and does not merely repeat D5.
- Confirm risk assessment is data-based.
- Confirm missing data is clearly listed.
