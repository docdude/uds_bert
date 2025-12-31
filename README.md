# CRC UDS Prototype 2025

A Python notebook system for extracting and auditing Colorectal Cancer (CRC) screening data from scanned PDFs and structured CSV files for UDS (Uniform Data System) reporting.

## Features

- **OCR-based PDF extraction** using Tesseract and Poppler
- **Intelligent date parsing** with DOB filtering
- **Event type classification** (Colonoscopy, FIT, FOBT, etc.)
- **UDS 2025 CRC rules engine** (lookback periods for different screening types)
- **Confidence scoring** and review flagging
- **Audit-ready evidence strings** for compliance documentation

## Requirements

### Python Packages
```bash
pip install pandas pytesseract pdf2image pdfplumber python-dateutil
```

### System Dependencies

#### Poppler (PDF to image conversion)
- **Windows**: Download from https://github.com/oschwartz10612/poppler-windows/releases
- Extract to `C:\poppler` and add `C:\poppler\Library\bin` to PATH
- Or set `POPPLER_PATH` in the notebook

#### Tesseract OCR
- **Windows**: Download from https://github.com/UB-Mannheim/tesseract/wiki
- Install to `C:\Program Files\Tesseract-OCR`
- Add to PATH or set `pytesseract.pytesseract.tesseract_cmd` in notebook

## Project Structure

```
uds_bert/
├── crc_uds_2025_updated.ipynb    # Main notebook
├── pdf_data/                      # Scanned CRC reports (PDFs)
├── csv_data/                      # Structured FOBT extracts
├── audit_data/                    # Output audit tables
└── .gitignore
```

## Usage

1. Place PDF reports in `pdf_data/`
2. Place CSV extracts in `csv_data/`
3. Configure `POPPLER_PATH` and Tesseract path in notebook
4. Run all cells in `crc_uds_2025_updated.ipynb`
5. Review output in `audit_data/crc_2025_audit_table_updated.csv`

## CRC Screening Types & Lookback Periods

| Test Type | Lookback Period |
|-----------|----------------|
| FOBT/FIT | Within reporting year |
| FIT-DNA (Cologuard) | 3 years |
| Flexible Sigmoidoscopy | 5 years |
| CT Colonography | 5 years |
| Colonoscopy | 10 years |

## Output

The notebook generates an audit table with:
- Patient ID
- Numerator status (met/not met)
- Best qualifying event type and date
- Data source (PDF vs CSV)
- Confidence score
- Review flag
- Evidence summary with snippets

## Notes

- **PHI Warning**: PDFs and CSVs may contain protected health information. Do NOT commit to public repositories without de-identification.
- The `.gitignore` excludes data files by default for safety.
- OCR accuracy depends on scan quality; review low-confidence results.

## License

Internal use only - Healthcare data processing system.
