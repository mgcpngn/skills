---
name: pptx-creation
description: Use when creating or editing Microsoft PowerPoint presentations programmatically. For generating slides, reports, pitch decks with proper formatting.
---

# PPTX Presentation Creation

## Overview

Create and edit Microsoft PowerPoint presentations programmatically using Python.

**Core principle:** Use python-pptx for reliable, cross-platform presentation generation.

## When to Use

**Use when:**
- Generating presentations from data
- Creating templated slide decks
- Batch presentation generation
- Automating report slides

## Setup

```bash
pip install python-pptx
```

## Basic Usage

### Create Presentation

```python
from pptx import Presentation
from pptx.util import Inches, Pt
from pptx.enum.text import PP_ALIGN
from pptx.dml.color import RGBColor

# Create new presentation
prs = Presentation()

# Add title slide
slide_layout = prs.slide_layouts[0]  # Title Slide
slide = prs.slides.add_slide(slide_layout)

title = slide.shapes.title
subtitle = slide.placeholders[1]

title.text = "Presentation Title"
subtitle.text = "Subtitle goes here"

# Save
prs.save('output.pptx')
```

### Slide Layouts

```python
# Common layout indices:
# 0: Title Slide
# 1: Title and Content
# 2: Section Header
# 3: Two Content
# 4: Comparison
# 5: Title Only
# 6: Blank

layout = prs.slide_layouts[1]  # Title and Content
slide = prs.slides.add_slide(layout)
```

### Add Text Content

```python
# Title
slide.shapes.title.text = "Slide Title"

# Content placeholder
content = slide.placeholders[1]
tf = content.text_frame
tf.text = "First bullet point"

# Add more paragraphs
p = tf.add_paragraph()
p.text = "Second bullet point"
p.level = 0

p = tf.add_paragraph()
p.text = "Sub-bullet"
p.level = 1
```

### Text Formatting

```python
from pptx.util import Pt
from pptx.dml.color import RGBColor

para = tf.paragraphs[0]
run = para.runs[0]

run.font.size = Pt(24)
run.font.bold = True
run.font.color.rgb = RGBColor(0x00, 0x66, 0xCC)
```

### Add Shapes

```python
from pptx.enum.shapes import MSO_SHAPE

# Add rectangle
left = Inches(1)
top = Inches(2)
width = Inches(3)
height = Inches(1)

shape = slide.shapes.add_shape(
    MSO_SHAPE.RECTANGLE, left, top, width, height
)
shape.text = "Shape Text"
```

### Add Tables

```python
rows, cols = 3, 4
left, top = Inches(1), Inches(2)
width, height = Inches(6), Inches(2)

table = slide.shapes.add_table(rows, cols, left, top, width, height).table

# Set column widths
table.columns[0].width = Inches(1.5)

# Fill cells
for i in range(rows):
    for j in range(cols):
        table.cell(i, j).text = f"R{i}C{j}"
```

### Add Images

```python
left = Inches(1)
top = Inches(2)
pic = slide.shapes.add_picture('image.png', left, top, width=Inches(4))
```

### Add Charts

```python
from pptx.chart.data import CategoryChartData
from pptx.enum.chart import XL_CHART_TYPE

# Prepare data
chart_data = CategoryChartData()
chart_data.categories = ['Q1', 'Q2', 'Q3', 'Q4']
chart_data.add_series('Sales', (19.2, 21.4, 16.7, 28.0))

# Add chart
x, y, cx, cy = Inches(1), Inches(2), Inches(6), Inches(4)
chart = slide.shapes.add_chart(
    XL_CHART_TYPE.COLUMN_CLUSTERED, x, y, cx, cy, chart_data
).chart
```

## Common Patterns

### Report Deck Template

```python
def create_report_deck(title, sections, output_path):
    prs = Presentation()
    
    # Title slide
    slide = prs.slides.add_slide(prs.slide_layouts[0])
    slide.shapes.title.text = title
    
    # Content slides
    for section in sections:
        slide = prs.slides.add_slide(prs.slide_layouts[1])
        slide.shapes.title.text = section['title']
        
        tf = slide.placeholders[1].text_frame
        for bullet in section['bullets']:
            p = tf.add_paragraph()
            p.text = bullet
            p.level = 0
    
    prs.save(output_path)
```

### Data Table Slide

```python
def add_data_slide(prs, title, headers, data):
    slide = prs.slides.add_slide(prs.slide_layouts[5])  # Title Only
    slide.shapes.title.text = title
    
    rows = len(data) + 1
    cols = len(headers)
    
    table = slide.shapes.add_table(
        rows, cols, Inches(0.5), Inches(1.5), Inches(9), Inches(5)
    ).table
    
    # Headers
    for i, header in enumerate(headers):
        cell = table.cell(0, i)
        cell.text = header
        cell.text_frame.paragraphs[0].font.bold = True
    
    # Data
    for i, row in enumerate(data):
        for j, value in enumerate(row):
            table.cell(i + 1, j).text = str(value)
```

## Quick Reference

| Task | Code |
|------|------|
| Create prs | `Presentation()` |
| Add slide | `prs.slides.add_slide(layout)` |
| Set title | `slide.shapes.title.text = "..."` |
| Add shape | `slide.shapes.add_shape(...)` |
| Add table | `slide.shapes.add_table(...)` |
| Add image | `slide.shapes.add_picture(...)` |
| Save | `prs.save(path)` |

## Related Skills

- **docx-creation** - Create Word documents
- **xlsx-creation** - Create Excel spreadsheets
