# PDF Compliance Test Harness

Automated validation of generated PDF letters against layout and content rules, with per-file diagnosis and a colour-coded Excel report.

**Origin:** personal project. **Data:** fully synthetic - the notebook generates its own test corpus. Outputs cleared.

## What was done
- Generates 300 synthetic letters with ReportLab: 210 valid and 90 with one seeded defect each (missing salutation, wrong weather lines, missing bold line, missing company line or missing date).
- **Layout check (PyMuPDF):** expects ten text lines at the specified spacing (10.8 pt).
- **Content check:** ordered regex rules for company, address, phone, website, date, order number, property line, salutation, two weather lines and bold formatting.
- Outputs: Excel report (green PASS / red FAIL), per-file text reports, executive summary, accuracy report and a Graphviz flowchart.

## Results
- Overall PASS/FAIL agreed with the known ground truth for all 300 letters, reproduced in three independent runs.
- Every letter failed by the layout check was also failed by the content check; the layout check only fires when a defect removes a line.

## Limitations
- The corpus and the rules come from the same specification, and only five defect types are seeded, so perfect agreement is expected by construction. It shows the harness works as designed, not how it would perform on real generator drift.
- Original version: one missing field made every later field report as missing (cascade). Fixed here, so per-file reasons now point to the actual defect. A fixed random seed makes runs reproducible.

## Tech stack
Python, ReportLab, PyMuPDF (fitz), regex, pandas, openpyxl, Matplotlib, Graphviz

## Repository
- `pdf_compliance_harness.ipynb`
- `requirements.txt`

---

**Author:** Raquel J. | [rjdatavoyage.co.uk](https://rjdatavoyage.co.uk)
