# Customer Training PPT Text Extraction

Source: Photos taken from PPT slides on 2026-05-31.

Status: Raw text extraction only. No rule summary has been added yet.

Note: The source images are slightly blurry. Text marked with `[unclear]` should be verified against the original PPT later.

## Contents

1. Issue, DRI(s), and JIRA Ticket(s)
2. Risk
3. Description
4. Customer Failure Mode
5. Failure Analysis
6. Root Cause(s) / Leading Hypothesis
7. Containment Action(s)
8. Corrective Action(s)
9. Preventive Action(s)
10. Next Steps & Dates
11. Factory Risk Assessment
12. Field Exposure Risk Assessment

## 1. Issue, DRI(s), and JIRA Ticket(s)

### Slide Title

```text
Issue & DRI(s) & JIRA Ticket(s):
```

### Guidances & Tips

#### Issue

- Base the title on the original test failure or customer complaint.
- Ensure alignment between the issue title and corresponding JIRA title.
- When consolidating multiple issues, use a shared commonality as the title.
- Keep titles concise - avoid excessive detail.

#### DRI(s)

- Identify all DRIs: include functional team and full name for each.
- DRIs must include the issue reporter and the designated issue owner.
- DRIs are responsible for:
  - Driving issue to closure.
  - Providing inputs for executive reporting decks.
  - Presenting issue explanations to external stakeholders in meetings.

#### JIRA Ticket(s)

- JIRA created in "labcollab".
- If multiple JIRAs exist, provide the master JIRA link.
- Ensure the latest FA report is updated.

### Examples & Appendix

```text
Issue examples:

1. [SMT] Flash_erase_sfw fail cause by solder bridge
2. [FATF][RIT] SoC failure *19 - kernel panic
3. [OBA] Unable to output sound streams from Amazon Music to external BT speaker

DRI examples:

1. [SMT] Flash_erase_sfw fail cause by solder bridge
   DRI(s): SQM: XXX, SME: XXX

2. [FATF] Touching of "+" button is weak
   DRI(s): PMQE: XXX, STR: XXX

3. [OBA] Unable to launch "Live TV sources" screen when press "Guide" button on remote
   DRI(s): LTPM: XXX, DQM: XXX
```

## 2. Risk

### Guidances & Tips

- Severity is not equal to Risk.
- Risk should strictly follow color code definition.
  - Risk is highly correlated with root cause and corrective action.
- Red Issue Classification (Non-Blocker Scenarios)
  - Issue without root cause MUST offline aligned in leadership White Paper review.
  - Issue with root cause but no POR solution. A temporary solution is only to unblock current build for other verification. Issue still be a blocker for next RR review. (Not applied for PVT RR/OK2Ship)

### Examples & Appendix

```text
Green - NO ISSUES/LOW RISK
Solutions identified and fully validated (for Hardware: validation must be on a large sample size)

Yellow - MEDIUM RISK
Open items and/or potential issues
Solution and implementation plan identified, but validation not yet complete or complete only on small sample size

Red - HIGH RISK
Root cause not yet identified, OR
Solution cannot be implemented within POR boundaries (schedule, cost, budget, or specifications)
Red does not necessarily indicate program blocker (management must assess the risk)
PVT Readiness through OK2Ship: Solution for P0 issues not fully validated (for Hardware: validation must be on a large sample size)
Core team must provide a single recommendation, backed up with data, on whether builds should start

Example:
1. OBA SW issue that target to fix by future build should be classified as Yellow
```

## 3. Description

### Guidances & Tips

- Discovery date (specific date)
- Time period (shift: Day/Night)
- Discovery station/test station
- Production line number
- Daily defect rate/failure rate (specific value and calculation base)
- Problem repeatability (for intermittent issues)
- Specific manifestation of first symptom (objective description, avoid subjective judgement)
- Affected product model/SKU (if applicable)
- Affected material information (if applicable)
- Whether problem has been contained
- Current disposition (Line stop, Material switch, tighten sampling rate...)

## 4. Customer Failure Mode

### Guidances & Tips

- Describe how the issue manifests to end-users (not factory test failures)
- Focus on customer experience impact (functional/performance/cosmetic)

### Examples & Appendix

```text
Example:
PVT is running with an Echo Multi-modal product. At the AUT station, 3 devices fail in one shift for PRB resulting in a line down situation on 1/29. The PRB failures are a discovery or observations of non-conforming material. Since the reason for the increase in PRB failure rate is not known, a containment action is taken and all finished goods are quarantined.

Additional examples:

1. For these RIT failure modes, the end user will see one of two failing conditions:
   1) unexpected reboot during boot (a longer booting time),
   2) unexpected reboot during normal usage
   (SoC failure *19 - Kernal panic)

2. Device has no audio output for a certain period (>15s) after boot up.
   (spc_speaker_1000_hz fail at BFT station)

3. Customer will hear minor noise in 900/950Hz audio frequency.
   Impacting audio performance.
   (SPK_ALL.loopback_mic1_MiAD_Buzz_900/950 at AUT station)
```

## 5. Failure Analysis

### Guidances & Tips

- Emphasize FA findings and conclusions rather than detailed procedural steps.
- Use specific measurements and percentages wherever possible.
- Provide statistical data to support conclusions.
- Add annotations directly on images to highlight key findings. Use arrows, circles, and text labels to mark critical areas.
- Use tables for comparative data (Good vs. Failed units, Before vs. After, Supplier A vs. Supplier B).
- If supplier provides their own FA report, present it in a separate subsection.

### Examples & Appendix

```text
Example:

1. We performed cross-section analysis on the failed samples and examined them under microscope. The solder joints showed some issues. We also did X-ray inspection and found problems with the joints. (Bad example)

1. Cross-section analysis of 20 failed units reveals solder coverage of 65% compared to 95% in good units, representing a 30% reduction. IMC layer thickness measures 1.2um in failed samples versus 3.5um in good samples (66% reduction). Void rate in failed units is 15% compared to less than 2% in good units. (Good example)
```

## 6. Root Cause(s) / Leading Hypothesis

### Guidances & Tips

- Root cause must have strong logical connection to Failure Analysis and directly drive the Corrective Action.
- If root cause is not confirmed, DRI need provide leading hypothesis with next verification actions.
- State the most basic reason that, if eliminated, would have prevented the failure entirely.
- If the defect should have been caught earlier, identify why existing controls failed to detect it.
- State root cause in 20-50 words maximum. Avoid lengthy explanations.

### Examples & Appendix

```text
Example:

1. A foreign material from supplier that causing a solder bridge during SMT process & failed @ BFT

   - A solder bridge occurred between SoC pins when foreign materials fell during reflow.
   - The contaminants escaped detection due to supplier AOI limitations, including poor contrast settings and loose size specifications.
   - The paper scraps originated from improper tray storage with carton boxes.

2. A SoC issue due to cache corruption, FA only reveal symptom but root cause not yet confirmed.

   - This issue has been isolated to SoC CPU core1. The hypothesis is the failure within CPU1 core due to instruction or data cache corruption may be causing random kernel panics during Linux boot-up. Testing is ongoing to further isolate the issue.
```

## 7. Containment Action(s)

### Guidances & Tips

- Containment actions are short term/temporary measures on the specific issue to unblock the build moving forward. Not part of the corrective actions.
- Describe immediate actions to prevent defective products from reaching customers.
  - Quarantine/isolate finished goods inventory.
  - Add temporary inspection personnel/station.
  - Increase sampling rate (e.g., from 2% to 100% inspection).
  - Hold shipments.
  - Screen suspect material lots.
- Specify duration or end condition for each containment action.
- If containment is with deviation, document the deviation ID.

### Examples & Appendix

```text
Example:

1. SMT is using 40x time microscope to do material sorting before SMT input till arrival of improved lot

2. FATP to establish additional incoming inspection station for top housing components inspection before production loading till 5/19.
```

## 8. Corrective Action(s)

### Guidances & Tips

- Corrective actions are long term fixes from design/process on the specific issue to resolve the failure mode.
- Describe design and/or process changes to eliminate the failure mode from happening again
  - Design optimizations on specific features.
  - Tightened specifications and tolerance analysis.
  - Material changes (before vs. after with rationale).
  - Process changes (before vs. after with rationale).
  - SW changes on specific patch/versions.
- Include preliminary verification steps and results to prove the action effectiveness.
- Specify if any downstream impacts (schedule due to tooling/fixture/line modification, material LT, cost etc.) are projected with the proposed correction action.

### Examples & Appendix

```text
Example:

1. Issue Target to fix in R64 image and deploy by OTA.

2. TI add a new test pattern to screen this kind of defect in supplier's ATE station.

3. Adjust the auto AOI's bottom light parameters, from "Red1 / fine setting 15%" to "Red Coax & Green Coax & Blue Coax / fine setting 23%"; this could make foreign material color in AOI from Green to Black.

4. OP training with current SOP / Monitoring / Data collection should NOT consider as a sole valid corrective action.
```

## 9. Preventive Action(s)

### Guidances & Tips

- Preventive actions are system-level improvements beyond fixing the immediate issue.
- Focus on preventing similar issues across other products/projects/processes and recorded in below system is preferred.
  - Document and share lessons learned.
  - Conduct cross-functional training sessions.
  - Take COE.

### Examples & Appendix

```text
Example:

1. Gift box lid gap over Spec -> conflicting grain directions in the multi-layer lid structure -> Lid design change and new designed test -> Add new designed test into regular package Rel test process

2. Tactility of "+" button is weak -> Burrs formed at insert joint area due to inserts misalignment in molder -> Replace two-joint molder with one-joint -> Avoid two-joint molder for small pieces
```

## 10. Next Steps & Dates

### Guidances & Tips

```text
This section is a mandatory section for all RED & Yellow issues. Below information should be included for each action.

- Next checkpoint
- DRI(s)
```

### Examples & Appendix

```text
Example:

1. Verify effectiveness of 40k sorted and following improved material and close this issue. DRI: Mike, Checkpoint: 12/8

2. Supplier prepared 20 boxes, 1920pcs fabric damage improved products for CR1001542 DRI: John, Checkpoint: 5/3
```

## 11. Factory Risk Assessment

### Guidances & Tips

```text
Factory Risk Assessment is a mandatory section for all RED issues and issue resolved but with factory impact.
```

- Yield Impact: Current yield vs. baseline with 95% CI upper limit (e.g., Current: 93.0%, Baseline: 98.5% (n=500), 95% CI: 94.8%).
- CTB Impact: Additional cycle time per unit/batch due to containment, rework, or testing (e.g., "+2.5 hours per 100-unit batch").
- Production Efficiency: Throughput reduction percentage and labor impact (e.g., "650 vs. 1,000 units/day (-35%), 3 additional QA deployed").
- Cost Impact: Breakdown of scrap, rework, labor, expedite costs with total (e.g., "Scrap: $45K, Labor: $30K, Expedite: $50K, Total: $125K").
- Scope & Duration: Affected quantity, production dates, recovery timeline (e.g., "2,500 units (Jan 10-15), 3-week recovery to baseline").

### Examples & Appendix

```text
Example:

1. The test results from PVT is in a nominal observed failure rate of 0.03% (7F/23,826T) with a projected upper limit of 0.05% (95% CI). SMT MLB Yield is ~99.92% versus target 99.5%.

2. FATP has CTB risk before supplier A new material (build with one-insert molder) qualified on 8/4, only supported by supplier B and sorted parts from supplier A.
```

## 12. Field Exposure Risk Assessment

### Guidances & Tips

```text
Field Exposure Risk Assessment is a mandatory section for all RED issues and issue resolved but with factory impact.
```

- Overall risk level calculation results based on GFRPB. If risk level is high, need more data to assess the risk before go to next milestone / Ship.
  - A expected field DPPM with 95% CI upper limit.
  - If team expected no/low customer impact, need the reason and data support the reason.

### Examples & Appendix

```text
Example:

1. In the absence of root cause, the field failure risk is estimated based on in-line RIT failure rates observed during PVT. The projected failure rate is 903 DPPM, with a 95% confidence upper limit of 1,324 DPPM, indicating a Critical/High Risk to customer (Severity 5; Occurrence x Detection = 4x5 = 20).

   - A secondary screening of 1,300 units that passed RIT showed 0 failures, providing 95% confidence that false negatives (escapes) from RIT are minimal.
   - Of those, 65 units also passed OBA testing with 0 failures.
   - Additional post-RIT testing across 7,349 units (including 6,792 from OBA, 180 from DRDT, and 377 from LTOS and Corner Test) showed 0 failures, supporting the screening effectiveness of RIT and downstream tests.
```
