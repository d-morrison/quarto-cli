# Demo Quarto Book with RevealJS Support

This demo book showcases the new RevealJS format support for Quarto books, implemented in the `copilot/add-revealjs-format-support` branch.

## Overview

This feature adds the ability to create book projects that output both HTML pages (for reading) and RevealJS presentations (for presenting) from the same source content.

## Key Features

### 1. Multi-Format Book Output

The book configuration in `_quarto.yml` specifies both `html` and `revealjs` formats:

```yaml
format:
  html: 
    theme: cosmo
  revealjs:
    theme: night
    slide-number: true
```

### 2. RevealJS Directory Organization

When rendered, the RevealJS presentations are organized in a separate `revealjs/` subdirectory within the `_book` output folder:

```
_book/
├── index.html                 # HTML book pages
├── intro.html
├── chapter1.html
├── chapter2.html
├── summary.html
└── revealjs/                  # RevealJS presentations
    ├── index.html
    ├── intro.html
    ├── chapter1.html
    ├── chapter2.html
    └── summary.html
```

### 3. Sidebar Navigation with RevealJS Links

The book sidebar includes links to both the HTML version and the RevealJS presentation for each chapter. An easel icon (🎨) appears next to each chapter link, allowing readers to quickly switch to the presentation view.

### 4. Implementation Details

The implementation consists of several components:

#### `src/format/reveal/format-reveal.ts`
- Adds book extension support to the revealjs format
- Configures `multiFile: true` to support book structure
- Sets `formatOutputDirectory` to organize revealJS files in a separate directory

#### `src/project/types/book/book-config.ts`
- Generates `revealjsHref` for each chapter in the sidebar
- Passes configuration through chapter processing functions

#### `src/resources/projects/website/templates/sidebaritem.ejs`
- Adds UI elements to display RevealJS links in the sidebar
- Shows easel icon for accessing presentations

#### `src/resources/projects/book/book.scss`
- Styles the RevealJS link icons
- Provides hover effects and appropriate sizing

## Book Structure

This demo book includes:

- **index.qmd**: Preface introducing the demo
- **intro.qmd**: Introduction to Quarto and key features
- **chapter1.qmd**: Creating content with Markdown, code, and math
- **chapter2.qmd**: Advanced features like callouts, columns, and fragments
- **summary.qmd**: Summary and resources

Each chapter is written once but rendered in two formats:
1. **HTML**: Optimized for reading with full navigation
2. **RevealJS**: Optimized for presenting with slide-based layout

## Usage

To render this book (requires Quarto with the revealjs book support):

```bash
quarto render
```

This will generate:
- HTML book in `_book/` directory
- RevealJS presentations in `_book/revealjs/` directory

## Benefits

1. **Write Once, Present Anywhere**: Create content once and use it for both documentation and presentations
2. **Seamless Navigation**: Easy switching between reading and presentation modes
3. **Consistent Content**: Ensures presentations stay in sync with documentation
4. **Flexible Formatting**: Use RevealJS-specific features (like fragments and incremental lists) that work in presentations while still rendering appropriately in HTML

## Technical Requirements

- Quarto CLI with revealjs book extension support
- Modern web browser for viewing HTML and RevealJS outputs

## Related Files

- `_quarto.yml`: Book configuration with dual format output
- `*.qmd`: Quarto Markdown source files
- `.gitignore`: Excludes build outputs (`_book/`, `.quarto/`)

## Future Enhancements

Potential improvements to this feature:
- Support for format-specific content blocks
- PDF export from RevealJS presentations
- Custom themes for coordinated book/presentation appearance
- Preview mode showing side-by-side HTML and RevealJS views
