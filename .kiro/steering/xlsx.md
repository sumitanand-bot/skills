# XLSX Steering

## Metadata

- **Name**: xlsx
- **Description**: Use this skill any time a spreadsheet file is the primary input or output. This includes opening, reading, editing, or fixing .xlsx, .xlsm, .csv, or .tsv files; creating new spreadsheets from scratch or other data sources; converting between tabular file formats; and cleaning or restructuring messy tabular data files. Trigger when user references a spreadsheet file by name or path, or wants tabular data cleaned into proper spreadsheets. Do NOT trigger when primary deliverable is Word, HTML, standalone Python script, database pipeline, or Google Sheets API integration.

## Triggers

Use this steering when:
- User mentions ".xlsx", ".xlsm", ".csv", ".tsv", "spreadsheet", or "Excel"
- User wants to create, read, edit, or analyze spreadsheet data
- User needs to add columns, compute formulas, or format cells
- User wants to convert between tabular file formats
- User needs to clean or restructure messy tabular data

## Instructions

### Requirements for Outputs

#### All Excel files

**Professional Font**: Use a consistent, professional font (e.g., Arial, Times New Roman) for all deliverables unless otherwise instructed.

**Zero Formula Errors**: Every Excel model MUST be delivered with ZERO formula errors (#REF!, #DIV/0!, #VALUE!, #N/A, #NAME?).

**Preserve Existing Templates**: Study and EXACTLY match existing format, style, and conventions when modifying files.

#### Financial models

**Color Coding Standards**:
- **Blue text (RGB: 0,0,255)**: Hardcoded inputs
- **Black text (RGB: 0,0,0)**: ALL formulas and calculations
- **Green text (RGB: 0,128,0)**: Links from other worksheets
- **Red text (RGB: 255,0,0)**: External links to other files
- **Yellow background (RGB: 255,255,0)**: Key assumptions needing attention

**Number Formatting**:
- **Years**: Format as text strings (e.g., "2024" not "2,024")
- **Currency**: Use $#,##0 format; ALWAYS specify units in headers
- **Zeros**: Use number formatting to make all zeros "-"
- **Percentages**: Default to 0.0% format (one decimal)
- **Multiples**: Format as 0.0x for valuation multiples
- **Negative numbers**: Use parentheses (123) not minus -123

### CRITICAL: Use Formulas, Not Hardcoded Values

**Always use Excel formulas instead of calculating values in Python and hardcoding them.**

❌ WRONG:
```python
total = df['Sales'].sum()
sheet['B10'] = total  # Hardcodes 5000
```

✅ CORRECT:
```python
sheet['B10'] = '=SUM(B2:B9)'
```

### Common Workflow

1. **Choose tool**: pandas for data, openpyxl for formulas/formatting
2. **Create/Load**: Create new workbook or load existing file
3. **Modify**: Add/edit data, formulas, and formatting
4. **Save**: Write to file
5. **Recalculate formulas (MANDATORY IF USING FORMULAS)**:
   ```bash
   python scripts/recalc.py output.xlsx
   ```
6. **Verify and fix any errors**

### Creating new Excel files

```python
from openpyxl import Workbook
from openpyxl.styles import Font, PatternFill, Alignment

wb = Workbook()
sheet = wb.active

# Add data
sheet['A1'] = 'Hello'
sheet.append(['Row', 'of', 'data'])

# Add formula
sheet['B2'] = '=SUM(A1:A10)'

# Formatting
sheet['A1'].font = Font(bold=True, color='FF0000')
sheet['A1'].fill = PatternFill('solid', start_color='FFFF00')

wb.save('output.xlsx')
```

### Editing existing Excel files

```python
from openpyxl import load_workbook

wb = load_workbook('existing.xlsx')
sheet = wb.active

# Modify cells
sheet['A1'] = 'New Value'
sheet.insert_rows(2)

wb.save('modified.xlsx')
```

### Best Practices

- **pandas**: Best for data analysis, bulk operations, and simple data export
- **openpyxl**: Best for complex formatting, formulas, and Excel-specific features
- Cell indices are 1-based (row=1, column=1 refers to cell A1)
- **Warning**: If opened with `data_only=True` and saved, formulas are replaced with values and permanently lost

## Resources

- `skills/xlsx/scripts/recalc.py` - Formula recalculation script
- `skills/xlsx/scripts/office/` - Office helper utilities
