---
name: xlsx-creation
description: Use when creating or editing Microsoft Excel spreadsheets programmatically. For generating reports, data exports, formatted tables with formulas.
---

# XLSX Spreadsheet Creation

## Overview

Create and edit Microsoft Excel spreadsheets programmatically using Python.

**Core principle:** Use openpyxl for reliable, cross-platform spreadsheet generation.

## When to Use

**Use when:**
- Generating reports from data
- Creating formatted spreadsheets
- Batch data exports
- Adding formulas and charts

## Setup

```bash
pip install openpyxl
```

## Basic Usage

### Create Workbook

```python
from openpyxl import Workbook
from openpyxl.styles import Font, Alignment, Border, Side, PatternFill
from openpyxl.utils import get_column_letter

# Create new workbook
wb = Workbook()
ws = wb.active
ws.title = "Data"

# Write data
ws['A1'] = 'Header 1'
ws['B1'] = 'Header 2'

# Save
wb.save('output.xlsx')
```

### Write Data

```python
# Cell by cell
ws['A1'] = 'Value'
ws.cell(row=2, column=1, value='Another value')

# Row at a time
ws.append(['Col1', 'Col2', 'Col3'])
ws.append([1, 2, 3])
ws.append([4, 5, 6])
```

### Cell Formatting

```python
from openpyxl.styles import Font, Alignment, PatternFill

# Font
ws['A1'].font = Font(
    name='Arial',
    size=14,
    bold=True,
    color='FFFFFF'
)

# Alignment
ws['A1'].alignment = Alignment(
    horizontal='center',
    vertical='center'
)

# Fill (background color)
ws['A1'].fill = PatternFill(
    start_color='0066CC',
    end_color='0066CC',
    fill_type='solid'
)
```

### Borders

```python
from openpyxl.styles import Border, Side

thin_border = Border(
    left=Side(style='thin'),
    right=Side(style='thin'),
    top=Side(style='thin'),
    bottom=Side(style='thin')
)

ws['A1'].border = thin_border
```

### Column Width and Row Height

```python
# Column width
ws.column_dimensions['A'].width = 20
ws.column_dimensions['B'].width = 15

# Row height
ws.row_dimensions[1].height = 30
```

### Formulas

```python
# Simple formulas
ws['C1'] = '=A1+B1'
ws['D10'] = '=SUM(D1:D9)'
ws['E1'] = '=AVERAGE(A1:A100)'

# Named ranges
from openpyxl.workbook.defined_name import DefinedName
wb.defined_names['total'] = DefinedName('total', attr_text='Sheet!$A$1:$A$10')
```

### Multiple Sheets

```python
# Create new sheet
ws2 = wb.create_sheet(title="Summary")

# Access sheets
sheets = wb.sheetnames  # ['Data', 'Summary']
ws = wb['Summary']

# Copy sheet
wb.copy_worksheet(wb['Data'])
```

### Freeze Panes

```python
# Freeze first row
ws.freeze_panes = 'A2'

# Freeze first column
ws.freeze_panes = 'B1'

# Freeze both
ws.freeze_panes = 'B2'
```

### Filters

```python
# Add autofilter
ws.auto_filter.ref = 'A1:D100'
```

## Common Patterns

### Data Export with Headers

```python
def export_data(data, headers, output_path):
    wb = Workbook()
    ws = wb.active
    
    # Header row with styling
    header_font = Font(bold=True, color='FFFFFF')
    header_fill = PatternFill('solid', fgColor='0066CC')
    
    for col, header in enumerate(headers, 1):
        cell = ws.cell(row=1, column=col, value=header)
        cell.font = header_font
        cell.fill = header_fill
        cell.alignment = Alignment(horizontal='center')
    
    # Data rows
    for row_idx, row_data in enumerate(data, 2):
        for col_idx, value in enumerate(row_data, 1):
            ws.cell(row=row_idx, column=col_idx, value=value)
    
    # Freeze header
    ws.freeze_panes = 'A2'
    
    # Auto-filter
    ws.auto_filter.ref = ws.dimensions
    
    wb.save(output_path)
```

### Styled Report Table

```python
def create_report_table(ws, data, start_row=1):
    from openpyxl.styles import Border, Side
    
    thin = Side(style='thin', color='000000')
    border = Border(left=thin, right=thin, top=thin, bottom=thin)
    
    for row_idx, row_data in enumerate(data, start_row):
        for col_idx, value in enumerate(row_data, 1):
            cell = ws.cell(row=row_idx, column=col_idx, value=value)
            cell.border = border
            
            # Header row styling
            if row_idx == start_row:
                cell.font = Font(bold=True)
                cell.fill = PatternFill('solid', fgColor='CCCCCC')
```

## Quick Reference

| Task | Code |
|------|------|
| Create workbook | `Workbook()` |
| Active sheet | `wb.active` |
| Write cell | `ws['A1'] = value` |
| Append row | `ws.append([...])` |
| Font | `cell.font = Font(...)` |
| Fill | `cell.fill = PatternFill(...)` |
| Column width | `ws.column_dimensions['A'].width` |
| Freeze | `ws.freeze_panes = 'A2'` |
| Save | `wb.save(path)` |

## Related Skills

- **docx-creation** - Create Word documents
- **pptx-creation** - Create PowerPoint presentations
