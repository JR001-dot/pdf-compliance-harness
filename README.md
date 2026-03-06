# Automated PDF Compliance Test Harness

Multi-layer validation framework that programmatically tests PDF documents against structural and content compliance rules - achieving 100% true positive and true negative rates across a controlled ground-truth corpus of 300 documents, with per-file failure diagnosis and colour-coded Excel reporting.

---

## Key Results

- **100% true positive rate** - all 210 compliant documents correctly passed
- **100% true negative rate** - all 90 defective documents correctly failed
- **Zero misclassifications** across 300 documents (0 false positives, 0 false negatives)
- Per-file failure diagnosis with root cause breakdown by failure mode

## The Problem

Automated document generation pipelines produce outputs at scale, but without systematic validation, defects accumulate silently. A PDF generator producing thousands of letters or regulated notices may drift from specification without triggering any visible error.

Manual spot-checking at volume is statistically insufficient. Automated harnesses with quantified false-positive and false-negative rates are the only defensible approach for regulated environments (financial services, insurance, legal).

## Approach

1. **Ground-Truth Corpus** - 300 synthetic PDF letters: 210 known-good, 90 known-defective with deliberate, categorised violations
2. **Layer 1: Structural Validation (Y-Gap)** - PyMuPDF-based paragraph spacing analysis asserting inter-paragraph gaps conform to layout specification
3. **Layer 2: Content Integrity** - Sequential regex assertions validating required fields in strict order: salutation, date, property address, order reference, phone, website, bold markers, weather-line phrases
4. **Reporting** - Per-file PASS/FAIL verdicts, specific failure reasons, colour-coded Excel workbook (green/red), and aggregate failure mode breakdown

## Failure Mode Analysis

| Failure Mode | Count |
|---|---|
| Weather line 1 - missing required phrase | 74 |
| Weather line 2 - missing required phrase | 74 |
| Salutation - incorrect format or missing | 58 |
| Order number - absent or malformed | 36 |
| Date - absent or malformed | 36 |
| Property line - absent or malformed | 36 |
| Phone - absent or incorrect | 20 |
| Website - absent or incorrect | 20 |
| Bold formatting - expected markers missing | 16 |

## Technology Stack

| Category | Tools |
|---|---|
| PDF Parsing | PyMuPDF (fitz) |
| Validation | Regex, custom assertion engine |
| Reporting | openpyxl (Excel), pandas |
| Infrastructure | pathlib, logging |

## Repository Structure

```
pdf-compliance-harness/
├── README.md
├── requirements.txt
├── src/
│   ├── structural_validator.py    # Layer 1: Y-gap analysis
│   ├── content_validator.py       # Layer 2: Regex assertions
│   ├── report_generator.py        # Excel report output
│   └── run_harness.py             # Main entry point
├── test_corpus/
│   ├── known_good/                # 210 compliant PDFs
│   ├── known_defective/           # 90 defective PDFs
│   └── README.md                  # Corpus design notes
├── output/
│   └── (generated Excel reports)
└── images/
    └── (sample report screenshots)
```

## Relevance to Production

The architecture - parse, assert, report - scales to any document type where compliance rules can be formalised: regulated financial notices, insurance certificates, legal contracts, or automated correspondence. Only the assertion rules change.

For organisations running AI-assisted document generation, this kind of post-generation compliance testing is the QA layer that makes the pipeline auditable.

## Case Study

Full write-up: [rjdatavoyage.co.uk/projects/pdf-test-harness](https://rjdatavoyage.co.uk/projects/pdf-test-harness/)

## Author

**Raquel J.** - [RJ Data Voyage](https://rjdatavoyage.co.uk) | [LinkedIn](https://www.linkedin.com/in/raquel-j-664113153/)
