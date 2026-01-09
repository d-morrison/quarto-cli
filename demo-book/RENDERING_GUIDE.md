# Demo Book Rendering Guide

## Quick Start

To render this demo book and see the RevealJS format support in action:

```bash
cd demo-book
quarto render
```

## Expected Output

After rendering, you'll see the following directory structure:

```
demo-book/
├── _quarto.yml              # Configuration
├── *.qmd                    # Source files
├── README.md                # Documentation
├── mockup.html              # UI preview
└── _book/                   # Generated output
    ├── index.html           # Preface (HTML)
    ├── intro.html           # Introduction (HTML)
    ├── chapter1.html        # Chapter 1 (HTML)
    ├── chapter2.html        # Chapter 2 (HTML)
    ├── summary.html         # Summary (HTML)
    ├── search.json          # Search index
    ├── libs/                # Dependencies
    └── revealjs/            # RevealJS presentations
        ├── index.html       # Preface (slides)
        ├── intro.html       # Introduction (slides)
        ├── chapter1.html    # Chapter 1 (slides)
        ├── chapter2.html    # Chapter 2 (slides)
        └── summary.html     # Summary (slides)
```

## Viewing the Book

### HTML Version (Reading Mode)

1. Open `_book/index.html` in a browser
2. You'll see a book with a sidebar navigation
3. Notice the **easel icons (🎨)** next to each chapter title in the sidebar
4. Click on chapter links to read the content in HTML format

### RevealJS Version (Presentation Mode)

1. Click any **easel icon (🎨)** in the sidebar
2. Or directly open files in `_book/revealjs/`
3. You'll see the same content formatted as slides
4. Use arrow keys or click to navigate through slides
5. Press `F` for fullscreen, `Esc` for overview

## Key Differences Between Formats

### HTML Format (Reading)
- Traditional book layout with continuous scrolling
- Full sidebar navigation always visible
- Optimized for reading and reference
- Includes search functionality
- All content visible at once

### RevealJS Format (Presenting)
- Slide-based presentation layout
- One section/topic per slide
- Optimized for presenting and teaching
- Supports presenter notes and speaker view
- Incremental reveals and animations
- Keyboard and touch navigation

## Content Overview

### Preface (`index.qmd`)
- Introduction to the demo
- Overview of features

### Chapter 1: Introduction (`intro.qmd`)
- What is Quarto?
- Key features overview
- Getting started guide

### Chapter 2: Creating Content (`chapter1.qmd`)
- Writing Markdown
- Adding code blocks
- Mathematical equations
- Lists and tables

### Chapter 3: Advanced Features (`chapter2.qmd`)
- Callouts and notes
- Column layouts
- Incremental lists (RevealJS-specific)
- Fragments and animations

### Summary (`summary.qmd`)
- What we learned
- Next steps
- Additional resources

## Format-Specific Features

### Content That Works in Both Formats
- Headings and paragraphs
- Bold, italic, code formatting
- Lists (bullet and numbered)
- Code blocks
- Mathematical equations
- Images and links

### RevealJS-Specific Features

The following features are designed for RevealJS but gracefully degrade in HTML:

```markdown
# Incremental Lists
::: {.incremental}
- First point
- Second point
- Third point
:::

# Fragments
::: {.fragment}
This appears on click
:::

::: {.fragment .fade-in}
This fades in
:::

# Speaker Notes
::: {.notes}
These notes are only visible in speaker view
:::
```

## Navigation Features

### In the Sidebar
- **Chapter links**: Click to view HTML version
- **Easel icons (🎨)**: Click to view RevealJS presentation
- **Active highlighting**: Current chapter is highlighted
- **Hover effects**: Links change appearance on hover

### In RevealJS
- **Arrow keys**: Navigate slides
- **Space**: Next slide
- **Shift+Space**: Previous slide
- **F**: Toggle fullscreen
- **S**: Speaker view (shows notes)
- **Esc**: Slide overview
- **?**: Show keyboard shortcuts

## Customization Options

### Themes

Change themes in `_quarto.yml`:

```yaml
format:
  html:
    theme: cosmo    # Try: default, cerulean, journal, etc.
  revealjs:
    theme: night    # Try: dark, league, sky, serif, etc.
```

### Additional RevealJS Options

```yaml
format:
  revealjs:
    theme: night
    slide-number: true
    show-slide-number: all
    hash-type: number
    preview-links: auto
    transition: slide
    background-transition: fade
    controls: true
    progress: true
    center: true
```

### Book Structure Options

```yaml
book:
  title: "Your Book Title"
  author: "Your Name"
  date: today
  chapters:
    - index.qmd
    - part: "Part 1"
      chapters:
        - chapter1.qmd
        - chapter2.qmd
    - part: "Part 2"
      chapters:
        - chapter3.qmd
```

## Troubleshooting

### If RevealJS links don't appear
- Ensure both formats are in `_quarto.yml`
- Check that you're using a Quarto version with book RevealJS support
- Verify the merge from `copilot/add-revealjs-format-support` branch

### If rendering fails
- Check for syntax errors in QMD files
- Ensure all dependencies are installed
- Try `quarto render --verbose` for detailed output

### If styles look wrong
- Clear browser cache
- Delete `_book/` and `.quarto/` directories
- Re-render from scratch

## Best Practices

1. **Write for both formats**: Keep content clear for reading and presenting
2. **Use headings wisely**: Each `##` becomes a new slide in RevealJS
3. **Test both outputs**: Verify content looks good in HTML and slides
4. **Use fragments sparingly**: Too many animations can be distracting
5. **Include speaker notes**: Add context in RevealJS that's not in slides
6. **Optimize images**: Use appropriate sizes for both formats

## Advanced Usage

### Custom CSS

Add custom styling for both formats:

```yaml
format:
  html:
    css: styles.css
  revealjs:
    css: slides.css
```

### Format-Specific Content

Show content only in specific formats:

```markdown
::: {.content-visible when-format="html"}
This only appears in HTML
:::

::: {.content-visible when-format="revealjs"}
This only appears in RevealJS
:::
```

### Cross-References

Use cross-references that work in both formats:

```markdown
See @fig-plot for details.

![A plot](plot.png){#fig-plot}
```

## Resources

- [Quarto Books Guide](https://quarto.org/docs/books/)
- [RevealJS Presentations](https://quarto.org/docs/presentations/revealjs/)
- [Markdown Basics](https://quarto.org/docs/authoring/markdown-basics.html)
- [Advanced Layout](https://quarto.org/docs/authoring/article-layout.html)
