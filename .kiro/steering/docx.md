# DOCX Steering

## Metadata

- **Name**: docx
- **Description**: Use this skill for Microsoft Word document (.docx) creation, editing, analysis, and manipulation. This includes creating new Word documents, editing content, working with tracked changes, adding comments, formatting, and find-and-replace operations. Trigger when user asks for a "report", "memo", "letter", "template", or similar deliverable as a Word or .docx file. Do NOT use for PDFs, spreadsheets, Google Docs, or general coding tasks.

## Triggers

Use this steering when:
- User mentions ".docx", "Word document", "report", "memo", "letter", or "template"
- User wants to create, edit, or analyze a Word document
- User needs to work with tracked changes or comments
- User asks to convert content into a polished Word document
- User needs to manipulate document formatting or structure

## Instructions

### Overview

A .docx file is a ZIP archive containing XML files.

### Quick Reference

| Task | Approach |
|------|----------|
| Read/analyze content | `pandoc` or unpack for raw XML |
| Create new document | Use `docx-js` - see Creating New Documents below |
| Edit existing document | Unpack → edit XML → repack |

### Converting .doc to .docx

Legacy `.doc` files must be converted before editing:

```bash
python scripts/office/soffice.py --headless --convert-to docx document.doc
```

### Reading Content

```bash
# Text extraction with tracked changes
pandoc --track-changes=all document.docx -o output.md

# Raw XML access
python scripts/office/unpack.py document.docx unpacked/
```

### Converting to Images

```bash
python scripts/office/soffice.py --headless --convert-to pdf document.docx
pdftoppm -jpeg -r 150 document.pdf page
```

### Creating New Documents

Generate .docx files with JavaScript, then validate. Install: `npm install -g docx`

#### Setup

```javascript
const { Document, Packer, Paragraph, TextRun, Table, TableRow, TableCell, ImageRun,
        Header, Footer, AlignmentType, PageOrientation, LevelFormat, ExternalHyperlink,
        TableOfContents, HeadingLevel, BorderStyle, WidthType, ShadingType,
        VerticalAlign, PageNumber, PageBreak } = require('docx');

const doc = new Document({ sections: [{ children: [/* content */] }] });
Packer.toBuffer(doc).then(buffer => fs.writeFileSync("doc.docx", buffer));
```

#### Validation

After creating the file, validate it:
```bash
python scripts/office/validate.py doc.docx
```

#### Critical Rules for docx-js

- **Set page size explicitly** - docx-js defaults to A4; use US Letter (12240 x 15840 DXA) for US documents
- **Never use `\n`** - use separate Paragraph elements
- **Never use unicode bullets** - use `LevelFormat.BULLET` with numbering config
- **PageBreak must be in Paragraph** - standalone creates invalid XML
- **ImageRun requires `type`** - always specify png/jpg/etc
- **Always set table `width` with DXA** - never use `WidthType.PERCENTAGE`
- **Use `ShadingType.CLEAR`** - never SOLID for table shading
- **TOC requires HeadingLevel only** - no custom styles on heading paragraphs

### Editing Existing Documents

**Follow all 3 steps in order.**

#### Step 1: Unpack
```bash
python scripts/office/unpack.py document.docx unpacked/
```

#### Step 2: Edit XML

Edit files in `unpacked/word/`. Use "Claude" as the author for tracked changes and comments.

**Use the Edit tool directly for string replacement. Do not write Python scripts.**

**CRITICAL: Use smart quotes for new content:**
```xml
<w:t>Here&#x2019;s a quote: &#x201C;Hello&#x201D;</w:t>
```

#### Step 3: Pack
```bash
python scripts/office/pack.py unpacked/ output.docx --original document.docx
```

### XML Reference

#### Tracked Changes

**Insertion:**
```xml
<w:ins w:id="1" w:author="Claude" w:date="2025-01-01T00:00:00Z">
  <w:r><w:t>inserted text</w:t></w:r>
</w:ins>
```

**Deletion:**
```xml
<w:del w:id="2" w:author="Claude" w:date="2025-01-01T00:00:00Z">
  <w:r><w:delText>deleted text</w:delText></w:r>
</w:del>
```

### Dependencies

- **pandoc**: Text extraction
- **docx**: `npm install -g docx` (new documents)
- **LibreOffice**: PDF conversion

## Resources

- `skills/docx/scripts/` - Helper scripts for unpacking, packing, comments, etc.
- `skills/docx/scripts/templates/` - Document templates
