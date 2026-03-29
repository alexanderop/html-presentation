# html-presentation

A Claude Code skill that generates self-contained HTML presentations from any topic. Say "create a presentation about X" and get a single `.html` file you can open in any browser — no dependencies, no build step, no slides app needed.

**[Live demo — example presentation](https://alexanderop.github.io/html-presentation/examples/html-presentations-intro.html)**

## What it does

1. Generates a markdown file with slide content separated by `---`
2. Converts each slide to HTML using a built-in dark-theme template
3. Writes a single self-contained `.html` file
4. Opens it in your browser

## Example prompts

```
"Create a presentation about microservices"
"Make an HTML presentation on TypeScript best practices"
"Generate standalone slides about our Q4 roadmap"
"Present about how AI will replace jobs"
```

## Features

- **Dark theme** with gradient headings and accent colors
- **Keyboard navigation** — arrow keys, space, home/end, 1-9 jump
- **Touch/swipe** support for mobile
- **Fullscreen** mode (F key)
- **Progress bar** and slide counter
- **Help overlay** (? key)
- **Smooth transitions** between slides
- **Two-column layouts** for comparisons
- **Code blocks, tables, blockquotes** — all styled
- **Zero dependencies** — one HTML file, works offline

## Keyboard shortcuts

| Key | Action |
|-----|--------|
| `→` / `Space` | Next slide |
| `←` | Previous slide |
| `Home` | First slide |
| `End` | Last slide |
| `1-9` | Jump to slide |
| `F` | Toggle fullscreen |
| `?` | Toggle help |
| `Esc` | Close help |

## Installation

### With `npx skills` (recommended)

```bash
npx skills add alexanderop/html-presentation
```

### Manual

Clone into your project's `.claude/skills/` directory:

```bash
git clone https://github.com/alexanderop/html-presentation .claude/skills/html-presentation
```

Or symlink from a shared location:

```bash
git clone https://github.com/alexanderop/html-presentation ~/skills/html-presentation
ln -s ~/skills/html-presentation .claude/skills/html-presentation
```

## Output

Presentations are saved to a `presentations/` directory in your project root:

```
presentations/
  microservices.md    # Source markdown
  microservices.html  # Self-contained presentation
```

Open the HTML file in any browser. Share it by sending the single file — no server required.

## License

MIT
