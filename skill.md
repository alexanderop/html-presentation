---
name: html-presentation
description: Generate a self-contained HTML presentation file from a topic or markdown content. This skill should be used when asked to "create an HTML presentation", "make slides as HTML", "generate a standalone presentation", "present about X as HTML", or when the user wants a portable presentation file they can open in any browser. Distinct from the blog presentation skill — this produces a standalone HTML file, not an Astro blog post.
---

# HTML Presentation Generator

Generate self-contained, single-file HTML presentations that open in any browser. No dependencies, no build step — just one `.html` file with embedded CSS and JS.

## Triggers

This skill applies when the user:
- Asks to create a standalone HTML presentation about a topic
- Wants a portable presentation file (not tied to the Astro blog)
- Says "html presentation", "standalone slides", "presentation file about X"
- Wants to quickly present something without a blog post

## Workflow

### Step 1: Generate Markdown Content

First, create a markdown file at `presentations/{slug}.md` with the presentation content.

**Structure the markdown using `---` as slide separators:**

```markdown
# Presentation Title

Subtitle or tagline

---

## Slide 2 Title

- Key point one
- Key point two
- Key point three

---

## Slide 3 Title

Content here with **bold** and `code` inline.

---

## Code Example

```python
def hello():
    print("Hello, world!")
```

---

## Thank You

Final slide content
```

**Content guidelines:**
- First slide is the cover — use an H1 and optional subtitle paragraph
- One main idea per slide
- Keep text concise — bullet points over paragraphs
- 8-15 slides is typical; adjust to topic complexity
- Use code blocks, tables, blockquotes, and images as needed
- Add `<!-- cover -->` comment before the first slide content (auto-applied by template)

### Step 2: Convert to HTML

Read the template at `assets/template.html` (relative to this skill's directory).

Convert each markdown slide (separated by `---`) into an HTML `<div class="slide">` block:

1. Split the markdown on `---` separators
2. Convert each section's markdown to HTML:
   - `# Heading` → `<h1>`, `## Heading` → `<h2>`, `### Heading` → `<h3>`
   - `**bold**` → `<strong>`, `*italic*` → `<em>`, `` `code` `` → `<code>`
   - `- item` → `<ul><li>item</li></ul>`
   - `1. item` → `<ol><li>item</li></ol>`
   - Code blocks → `<pre><code>...</code></pre>`
   - `> quote` → `<blockquote>`
   - `[text](url)` → `<a href="url">text</a>`
   - `![alt](src)` → `<img src="src" alt="alt">`
   - Paragraphs → `<p>`
   - Tables → `<table>`
3. Wrap each in: `<div class="slide"><div class="slide-inner">...content...</div></div>`
4. Add class `cover` to the first slide: `<div class="slide cover">`
5. Replace `{{TITLE}}` in the template with the presentation title
6. Replace `{{SLIDES}}` with all slide divs joined together

**Write the output to `presentations/{slug}.html`** in the project root.

### Step 3: Open in Browser

After writing the HTML file, open it:

```bash
open presentations/{slug}.html
```

On Linux, use `xdg-open` instead of `open`.

## Template

The HTML template is at `assets/template.html` relative to this skill. It includes:
- Dark theme with gradient headings
- Keyboard navigation (arrows, space, home/end, 1-9 jump)
- Touch/swipe support
- Fullscreen mode (F key)
- Progress bar and slide counter
- Help overlay (? key)
- Smooth slide transitions
- Responsive typography

## Slide Styling Tips

- Add two-column layouts with: `<div class="cols"><div>Left</div><div>Right</div></div>`
- The first slide automatically gets cover styling (centered, larger text)
- Use `<strong>` for accent-colored emphasis
- Use `<em>` for secondary accent color

## Example Output Path

For a presentation about "Atomic CSS":
- Markdown: `presentations/atomic-css.md`
- HTML: `presentations/atomic-css.html`

Ensure the `presentations/` directory exists before writing files (create it if not).
