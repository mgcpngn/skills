---
name: webapp-testing
description: Use when testing local web applications using Playwright. For verifying frontend functionality, debugging UI behavior, capturing screenshots, and viewing browser logs.
---

# Web Application Testing

## Overview

Test local web applications using Python Playwright scripts.

**Core principle:** Reconnaissance before action - understand the page state before interacting.

## When to Use

**Use when:**
- Testing local web application functionality
- Verifying UI behavior after changes
- Debugging frontend issues
- Capturing screenshots for documentation
- Inspecting browser console logs

## Decision Tree

```
User task
    │
    ▼
Is it static HTML?
    ├── Yes → Read HTML file directly
    │         Identify selectors → Write Playwright script
    │
    └── No (dynamic webapp)
             │
             ▼
        Is server running?
            ├── No → Start server first
            │        Then write Playwright script
            │
            └── Yes → Reconnaissance-then-action:
                      1. Navigate, wait for networkidle
                      2. Take screenshot or inspect DOM
                      3. Identify selectors from rendered state
                      4. Execute actions with discovered selectors
```

## The Pattern

### Basic Playwright Script

```python
from playwright.sync_api import sync_playwright

with sync_playwright() as p:
    browser = p.chromium.launch(headless=True)
    page = browser.new_page()
    
    # Navigate
    page.goto('http://localhost:5173')
    
    # CRITICAL: Wait for JS to execute
    page.wait_for_load_state('networkidle')
    
    # Your automation logic
    page.screenshot(path='screenshot.png')
    
    browser.close()
```

### Reconnaissance-Then-Action

**Step 1: Inspect rendered DOM**
```python
# Take screenshot for visual inspection
page.screenshot(path='/tmp/inspect.png', full_page=True)

# Get page content
content = page.content()

# List all buttons
buttons = page.locator('button').all()
for btn in buttons:
    print(btn.text_content())
```

**Step 2: Identify selectors**
From inspection, note:
- Button text: `text=Submit`
- Roles: `role=button[name="Submit"]`
- CSS: `#submit-btn`, `.btn-primary`
- Data attributes: `[data-testid="submit"]`

**Step 3: Execute actions**
```python
# Click using discovered selector
page.click('text=Submit')

# Fill form
page.fill('#email', 'test@example.com')

# Wait and verify
page.wait_for_selector('.success-message')
```

### Multiple Servers

For apps with backend + frontend:

```python
# Start servers in separate processes first, then:

with sync_playwright() as p:
    browser = p.chromium.launch(headless=True)
    page = browser.new_page()
    
    # Frontend served on :5173, backend API on :3000
    page.goto('http://localhost:5173')
    page.wait_for_load_state('networkidle')
    
    # Frontend will call backend API
    # ...
```

### Capturing Console Logs

```python
def handle_console(msg):
    print(f"[{msg.type}] {msg.text}")

page.on("console", handle_console)
page.goto('http://localhost:5173')
```

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| ❌ Inspect DOM before `networkidle` | ✅ Always `wait_for_load_state('networkidle')` |
| ❌ Hardcode selectors without checking | ✅ Screenshot/inspect first |
| ❌ No waits before actions | ✅ Use `wait_for_selector()` |
| ❌ Forget to close browser | ✅ Always `browser.close()` |

## Best Practices

1. **Use `sync_playwright()`** for synchronous scripts
2. **Always launch headless** in automation
3. **Wait for network idle** on dynamic apps
4. **Use descriptive selectors**: `text=`, `role=`, CSS, or IDs
5. **Add waits**: `wait_for_selector()`, `wait_for_timeout()`
6. **Close browser** in finally block or context manager

## Selector Priority

1. `data-testid` attributes (most stable)
2. Role selectors: `role=button[name="Submit"]`
3. Text selectors: `text=Submit`
4. CSS selectors: `#id`, `.class`
5. XPath (last resort)

## Quick Reference

| Task | Code |
|------|------|
| Navigate | `page.goto(url)` |
| Wait for load | `page.wait_for_load_state('networkidle')` |
| Screenshot | `page.screenshot(path='file.png')` |
| Click | `page.click(selector)` |
| Fill input | `page.fill(selector, value)` |
| Get text | `page.text_content(selector)` |
| Wait for element | `page.wait_for_selector(selector)` |

## Related Skills

- **test-driven-development** - Write tests for UI
- **systematic-debugging** - Debug failing tests
