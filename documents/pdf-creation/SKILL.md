---
name: pdf-creation
description: Use when creating PDF documents programmatically. For generating reports, invoices, documents with precise layout control.
---

# PDF Document Creation

## Overview

Create PDF documents programmatically using Python.

**Core principle:** Use ReportLab for full control, or WeasyPrint for HTML-to-PDF conversion.

## When to Use

**Use when:**
- Generating reports with precise layout
- Creating invoices, receipts
- Converting HTML to PDF
- Building documents from templates

## Setup

```bash
# ReportLab for full control
pip install reportlab

# WeasyPrint for HTML-to-PDF
pip install weasyprint
```

## ReportLab Usage

### Basic Document

```python
from reportlab.lib.pagesizes import letter, A4
from reportlab.pdfgen import canvas
from reportlab.lib.units import inch

# Create PDF
c = canvas.Canvas("output.pdf", pagesize=letter)
width, height = letter

# Draw text
c.drawString(1*inch, height - 1*inch, "Hello, World!")

# Save
c.save()
```

### Text Formatting

```python
from reportlab.lib.pagesizes import letter
from reportlab.pdfgen import canvas
from reportlab.lib.units import inch

c = canvas.Canvas("styled.pdf", pagesize=letter)
width, height = letter

# Set font
c.setFont("Helvetica-Bold", 24)
c.drawString(1*inch, height - 1*inch, "Title")

c.setFont("Helvetica", 12)
c.drawString(1*inch, height - 1.5*inch, "Regular text")

# Colors
c.setFillColorRGB(0.2, 0.4, 0.8)
c.drawString(1*inch, height - 2*inch, "Colored text")

c.save()
```

### Using Platypus (Document Templates)

```python
from reportlab.lib.pagesizes import letter
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.platypus import SimpleDocTemplate, Paragraph, Spacer, Table
from reportlab.lib.units import inch

# Create document
doc = SimpleDocTemplate("report.pdf", pagesize=letter)
styles = getSampleStyleSheet()
story = []

# Title
story.append(Paragraph("Report Title", styles['Heading1']))
story.append(Spacer(1, 0.25*inch))

# Paragraph
story.append(Paragraph("This is body text.", styles['Normal']))
story.append(Spacer(1, 0.25*inch))

# Build PDF
doc.build(story)
```

### Tables

```python
from reportlab.platypus import Table, TableStyle
from reportlab.lib import colors

data = [
    ['Header 1', 'Header 2', 'Header 3'],
    ['Row 1', 'Data', 'Data'],
    ['Row 2', 'Data', 'Data'],
]

table = Table(data)
table.setStyle(TableStyle([
    ('BACKGROUND', (0, 0), (-1, 0), colors.grey),
    ('TEXTCOLOR', (0, 0), (-1, 0), colors.whitesmoke),
    ('ALIGN', (0, 0), (-1, -1), 'CENTER'),
    ('FONTNAME', (0, 0), (-1, 0), 'Helvetica-Bold'),
    ('FONTSIZE', (0, 0), (-1, 0), 14),
    ('BOTTOMPADDING', (0, 0), (-1, 0), 12),
    ('BACKGROUND', (0, 1), (-1, -1), colors.beige),
    ('GRID', (0, 0), (-1, -1), 1, colors.black),
]))

story.append(table)
```

### Images

```python
from reportlab.platypus import Image

img = Image('logo.png', width=2*inch, height=1*inch)
story.append(img)
```

## WeasyPrint (HTML to PDF)

### Basic Conversion

```python
from weasyprint import HTML, CSS

# From HTML string
html = """
<html>
<head>
    <style>
        body { font-family: Arial; margin: 2cm; }
        h1 { color: #333; }
    </style>
</head>
<body>
    <h1>Report Title</h1>
    <p>Content goes here.</p>
</body>
</html>
"""

HTML(string=html).write_pdf('output.pdf')
```

### From HTML File

```python
HTML('template.html').write_pdf('output.pdf')
```

### With External CSS

```python
HTML('document.html').write_pdf(
    'output.pdf',
    stylesheets=[CSS('styles.css')]
)
```

### Template with Jinja2

```python
from jinja2 import Template
from weasyprint import HTML

template = Template("""
<!DOCTYPE html>
<html>
<head>
    <style>
        body { font-family: Arial; }
        table { border-collapse: collapse; width: 100%; }
        th, td { border: 1px solid #ddd; padding: 8px; }
    </style>
</head>
<body>
    <h1>{{ title }}</h1>
    <table>
        <tr>{% for h in headers %}<th>{{ h }}</th>{% endfor %}</tr>
        {% for row in data %}
        <tr>{% for cell in row %}<td>{{ cell }}</td>{% endfor %}</tr>
        {% endfor %}
    </table>
</body>
</html>
""")

html = template.render(
    title="Sales Report",
    headers=["Product", "Quantity", "Revenue"],
    data=[["Widget A", 100, "$1,000"], ["Widget B", 50, "$750"]]
)

HTML(string=html).write_pdf('report.pdf')
```

## Quick Reference

### ReportLab

| Task | Code |
|------|------|
| Create canvas | `canvas.Canvas(path)` |
| Draw text | `c.drawString(x, y, text)` |
| Set font | `c.setFont(name, size)` |
| Save | `c.save()` |

### Platypus

| Task | Code |
|------|------|
| Create doc | `SimpleDocTemplate(path)` |
| Add paragraph | `Paragraph(text, style)` |
| Add table | `Table(data)` |
| Build | `doc.build(story)` |

### WeasyPrint

| Task | Code |
|------|------|
| From string | `HTML(string=html).write_pdf(path)` |
| From file | `HTML(file).write_pdf(path)` |
| With CSS | `write_pdf(stylesheets=[CSS(...)])` |

## Related Skills

- **docx-creation** - Create Word documents
- **pptx-creation** - Create PowerPoint presentations
