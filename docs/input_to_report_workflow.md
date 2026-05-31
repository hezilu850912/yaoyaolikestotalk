# Input to FA Report Workflow

## 1. Input Collection

Accepted source materials:

- PDF reports
- JIRA exports
- PPT files
- Excel data
- Images
- Test logs
- Manual notes
- Supplier FA reports
- External research references when explicitly allowed

## 2. Evidence Extraction

Extract only source-supported facts:

- Failure symptom
- Customer complaint
- Test station and condition
- Failure rate and calculation base
- Good vs. failed comparison
- Measurements and statistical data
- Images and annotations
- JIRA IDs and ownership
- Containment, corrective, and preventive actions
- Factory and field risk data

If evidence conflicts, flag the conflict and ask for confirmation.

## 3. FA Sentence Normalization

Failure Analysis should use concise fixed-format statements.

Preferred sentence patterns:

```text
Performed [action/test]; [result] was observed.
Compared [A] with [B]; [difference] confirmed [conclusion].
Measured [parameter]; [value/trend] indicated [finding].
Verified [condition/hypothesis]; [result] supported [cause].
Verified [condition/hypothesis]; [result] excluded [alternative cause].
```

Avoid:

- Long procedural narratives
- Unnecessary test history
- Unsupported opinions
- Side branches that do not support the final logic

## 4. Logic Chain Construction

Build a main logic chain:

```text
Failure symptom -> FA evidence -> mechanism -> root cause -> corrective action
```

Example:

```text
Split mold design
-> insert joint exists
-> insert alignment mismatch creates overflow path
-> burr forms at joint area
-> root cause: split mold insert alignment instability
```

## 5. Branch Filtering

Keep a side branch only if it does one of the following:

- Supports a key link in the main logic chain.
- Provides required evidence for a conclusion.
- Excludes a major alternative cause.
- Explains why existing controls failed.
- Is required for risk, containment, CA, PA, or next steps.

Do not include side branches in the final customer report if they are only procedural background.

## 6. External Research

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

## 7. Report Generation

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

## 8. Review Gate

Before finalizing:

- Confirm every claim is supported by source material.
- Confirm each FA sentence is concise and evidence-based.
- Confirm root cause connects to FA evidence.
- Confirm corrective action addresses root cause.
- Confirm containment prevents customer escape.
- Confirm risk assessment is data-based.
- Confirm missing data is clearly listed.
