# PDF Steering

## Metadata

- **Name**: pdf
- **Description**: Use this skill whenever the user wants to do anything with PDF files. This includes reading or extracting text/tables from PDFs, combining or merging multiple PDFs into one, splitting PDFs apart, rotating pages, adding watermarks, creating new PDFs, filling PDF forms, encrypting/decrypting PDFs, extracting images, and OCR on scanned PDFs. If the user mentions a .pdf file or asks to produce one, use this skill.

## Triggers

Use this steering when:
- User mentions ".pdf" or "PDF"
- User wants to read, extract, merge, split, or rotate PDFs
- User asks to fill PDF forms
- User needs to create new PDFs
- User wants OCR on scanned documents
- User mentions watermarks, encryption, or image extraction from PDFs

## Instructions

### Overview

This guide covers essential PDF processing operations using Python libraries and command-line tools. For advanced features, see `skills/pdf/reference.md`. For PDF form filling, read `skills/pdf/forms.md`.

### Quick Start

```python
from pypdf import PdfReader, PdfWriter

# Read a PDF
reader = PdfReader("document.pdf")
print(f"Pages: {len(reader.pages)}")

# Extract text
text = ""
for page in reader.pages:
    text += page.extract_text()
```

### Python Libraries

#### pypdf - Basic Operations

**Merge PDFs:**
```python
from pypdf import PdfWriter, PdfReader

writer = PdfWriter()
for pdf_file in ["doc1.pdf", "doc2.pdf"]:
    reader = PdfReader(pdf_file)
    for page in reader.pages:
        writer.add_page(page)

with open("merged.pdf", "wb") as output:
    writer.write(output)
```

**Split PDF:**
```python
reader = PdfReader("input.pdf")
for i, page in enumerate(reader.pages):
    writer = PdfWriter()
    writer.add_page(page)
    with open(f"page_{i+1}.pdf", "wb") as output:
        writer.write(output)
```

**Rotate Pages:**
```python
page = reader.pages[0]
page.rotate(90)  # Rotate 90 degrees clockwise
```

#### pdfplumber - Text and Table Extraction

```python
import pdfplumber

with pdfplumber.open("document.pdf") as pdf:
    for page in pdf.pages:
        text = page.extract_text()
        tables = page.extract_tables()
```

#### reportlab - Create PDFs

```python
from reportlab.lib.pagesizes import letter
from reportlab.pdfgen import canvas

c = canvas.Canvas("hello.pdf", pagesize=letter)
c.drawString(100, 700, "Hello World!")
c.save()
```

**IMPORTANT**: Never use Unicode subscript/superscript characters in ReportLab PDFs. Use `<sub>` and `<super>` tags instead.

### Command-Line Tools

```bash
# Extract text (pdftotext)
pdftotext input.pdf output.txt

# Merge PDFs (qpdf)
qpdf --empty --pages file1.pdf file2.pdf -- merged.pdf

# Rotate pages (qpdf)
qpdf input.pdf output.pdf --rotate=+90:1
```

### Common Tasks

**OCR Scanned PDFs:**
```python
import pytesseract
from pdf2image import convert_from_path

images = convert_from_path('scanned.pdf')
for image in images:
    text = pytesseract.image_to_string(image)
```

**Add Watermark:**
```python
watermark = PdfReader("watermark.pdf").pages[0]
for page in reader.pages:
    page.merge_page(watermark)
```

**Password Protection:**
```python
writer.encrypt("userpassword", "ownerpassword")
```

### Quick Reference

| Task | Best Tool |
|------|-----------|
| Merge PDFs | pypdf |
| Extract text | pdfplumber |
| Extract tables | pdfplumber |
| Create PDFs | reportlab |
| OCR scanned | pytesseract |
| Fill forms | pdf-lib or pypdf |

## Resources

- `skills/pdf/reference.md` - Advanced features and detailed examples
- `skills/pdf/forms.md` - PDF form filling instructions
- `skills/pdf/scripts/` - Helper scripts for form extraction, validation, etc.
