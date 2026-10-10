# Power BI Model Audit

Finds what is actually used in a Power BI semantic model — and what isn't.

The notebook builds a lineage graph from the SQL layer to the report:

**SQL (CTAS) → semantic model (TMDL) → report visuals (PBIR)**

and flags every column, table and measure that no visual depends on.

## What it detects

- Dead SQL columns, model columns and DAX measures
- Columns only kept alive by dead measures
- Broken visual references (a visual pointing at a field that no longer exists)
- Where each field is used (page, visual, filter)

## Inputs

Place these next to the notebook:

- `build.sql` — the CTAS pipeline
- `<model>.tmdl` — the semantic model (Power BI Desktop → TMDL view)
- `<model>.pbix` — the report, saved in PBIR format

Then set the file names in the `MODELS` dictionary (Cell 1).

## Output

`audit_report.xlsx` with the sheets `dead_objects`, `alive_objects`, `visual_usage`, `broken_refs` and `dead_by_cascade`.

## Stack

Python · sqlglot · networkx · pandas
