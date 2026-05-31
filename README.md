# yaoyaolikestotalk

FA report assistant project for converting PDF, JIRA exports, PPT, Excel files, images, and manual notes into concise customer-ready FA report sections.

## Core Idea

The assistant should generate report sections based on source evidence and the customer training notes. It should not simply summarize all inputs. It should:

- Extract useful evidence from input files.
- Generate standard FA report sections in Markdown.
- Write Failure Analysis in concise fixed-format evidence sentences.
- Build a main FA logic chain such as `A -> B -> C -> Root Cause`.
- Keep side-branch FA evidence only when it supports a key logic link or excludes an important alternative cause.
- Generate a Mermaid FA logic flowchart.
- Mark missing information instead of fabricating data.

## Key Files

- `customer_training_issue_dri_jira_notes.md`: raw extracted customer training notes.
- `prompts/section_generation_prompt.md`: main prompt for generating standard report sections.
- `templates/standard_fa_report.md`: Markdown output template for generated reports.
- `docs/input_to_report_workflow.md`: workflow from input materials to report output.
- `examples/fa_logic_demo_arrow_burr.md`: demo showing FA logic chain and flowchart.

## Expected Output

Default output should be a Markdown report containing:

- Standard report sections.
- Missing / need confirmation questions.
- Failure Analysis written in fixed action-result sentences.
- FA main logic line.
- Supporting and excluded branches.
- Mermaid flowchart.

Final customer deliverables may later be exported to Word, PDF, or PPT.
