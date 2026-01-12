---
name: docx-creation
description: Use when creating or editing Microsoft Word documents programmatically. For generating reports, proposals, documentation with proper formatting and styles.
---

# DOCX Document Creation

## Overview

Create and edit Microsoft Word documents programmatically using Python.

**Core principle:** Use python-docx for reliable, cross-platform document generation.

## When to Use

**Use when:**
- Generating reports programmatically
- Creating templated documents
- Batch document generation
- Converting data to formatted Word documents

## Setup

```bash
pip install python-docx
```

## Basic Usage

### Create Document

```python
from docx import Document
from docx.shared import Pt, Inches, RGBColor
from docx.enum.text import WD_ALIGN_PARAGRAPH

# Create new document
doc = Document()

# Add title
title = doc.add_heading('Document Title', level=0)

# Add paragraph
para = doc.add_paragraph('This is a paragraph.')

# Save
doc.save('output.docx')
```

### Text Formatting

```python
from docx.shared import Pt, RGBColor

para = doc.add_paragraph()
run = para.add_run('Bold and colored text')
run.bold = True
run.font.size = Pt(14)
run.font.color.rgb = RGBColor(0x42, 0x24, 0xE9)
```

### Headings

```python
# Different heading levels
doc.add_heading('Main Title', level=0)     # Title
doc.add_heading('Chapter 1', level=1)      # Heading 1
doc.add_heading('Section 1.1', level=2)    # Heading 2
```

### Tables

```python
# Create table
table = doc.add_table(rows=3, cols=3)
table.style = 'Table Grid'

# Fill cells
for i, row in enumerate(table.rows):
    for j, cell in enumerate(row.cells):
        cell.text = f'Row {i}, Col {j}'

# Header row formatting
header_row = table.rows[0]
for cell in header_row.cells:
    cell.paragraphs[0].runs[0].bold = True
```

### Lists

```python
# Bullet list
doc.add_paragraph('First item', style='List Bullet')
doc.add_paragraph('Second item', style='List Bullet')

# Numbered list
doc.add_paragraph('Step one', style='List Number')
doc.add_paragraph('Step two', style='List Number')
```

### Images

```python
from docx.shared import Inches

doc.add_picture('image.png', width=Inches(4.0))
```

### Page Breaks

```python
from docx.enum.text import WD_BREAK

# Add page break
doc.add_page_break()

# Or within a paragraph
para = doc.add_paragraph()
para.add_run().add_break(WD_BREAK.PAGE)
```

## Common Patterns

### Report Template

```python
def create_report(title, sections, output_path):
    doc = Document()
    
    # Title
    doc.add_heading(title, level=0)
    
    # Date
    from datetime import datetime
    doc.add_paragraph(f'Generated: {datetime.now().strftime("%Y-%m-%d")}')
    
    # Sections
    for section in sections:
        doc.add_heading(section['title'], level=1)
        doc.add_paragraph(section['content'])
        
        if 'table_data' in section:
            add_table(doc, section['table_data'])
    
    doc.save(output_path)
```

### Styled Table

```python
def add_styled_table(doc, headers, rows):
    table = doc.add_table(rows=1 + len(rows), cols=len(headers))
    table.style = 'Table Grid'
    
    # Header
    header_row = table.rows[0]
    for i, header in enumerate(headers):
        cell = header_row.cells[i]
        cell.text = header
        cell.paragraphs[0].runs[0].bold = True
    
    # Data rows
    for i, row_data in enumerate(rows):
        row = table.rows[i + 1]
        for j, value in enumerate(row_data):
            row.cells[j].text = str(value)
    
    return table
```

## Quick Reference

| Task | Code |
|------|------|
| Create doc | `Document()` |
| Add heading | `doc.add_heading(text, level)` |
| Add paragraph | `doc.add_paragraph(text)` |
| Add table | `doc.add_table(rows, cols)` |
| Add image | `doc.add_picture(path, width)` |
| Page break | `doc.add_page_break()` |
| Save | `doc.save(path)` |

## Related Skills

- **pptx-creation** - Create PowerPoint documents
- **xlsx-creation** - Create Excel spreadsheets
