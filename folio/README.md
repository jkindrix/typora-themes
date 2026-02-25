# Folio

A Typora theme designed for PDF generation and physical printing.

## Design Principles

1. **Print-first** — All sizing in pt/mm. No sub-pixel rounding ambiguity.
2. **Legibility floor** — Nothing below 7pt; body text at 10pt.
3. **Content integrity** — Overflow is visible, never clipped. No silent data loss.
4. **Orphan/widow control** — Minimum 3 lines on each side of every page break.
5. **Graceful degradation** — Table stripes include border fallbacks for monochrome printers.

## Typography

| Element | Size | Font |
|---------|------|------|
| Body text | 10pt | System sans-serif (-apple-system, Segoe UI, Noto Sans, ...) |
| Code blocks | 7.5pt | System monospace (SF Mono, Fira Code, Cascadia Code, Consolas, ...) |
| Inline code | 8pt | Same monospace stack |
| Footnotes | 0.9em | Inherited |
| h1 | 18pt | Bold, black |
| h2 | 15pt | Bold, black |
| h3 | 12pt | Bold, dark gray |
| h4 | 11pt | Bold, dark gray |
| h5 | 10pt | Bold, muted |
| h6 | 10pt | Italic, muted |

Line height is 1.5 across the document.

## Color Palette

| Token | Value | Usage |
|-------|-------|-------|
| `--color-bg` | `#ffffff` | Page background |
| `--color-text` | `#1a1a1a` | Body text |
| `--color-text-muted` | `#555555` | h5, h6, secondary text |
| `--color-heading` | `#000000` | h1–h4 |
| `--color-link` | `#0055aa` | Hyperlinks, TOC entries, footnote refs |
| `--color-rule` | `#cccccc` | Horizontal rules, heading underlines |
| `--color-code-bg` | `#f6f6f6` | Code block / inline code background |
| `--color-quote-border` | `#999999` | Blockquote left border |
| `--color-table-stripe-bg` | `#f8f8f8` | Even table rows |

All colors flatten to black/white in `@media print` for reliable output on any printer.

## Page-Break Behavior

The theme includes comprehensive page-break control for clean PDF pagination:

| Element | Strategy |
|---------|----------|
| Headings (h1–h6) | `break-inside: avoid; break-after: avoid` — headings stay with following content |
| Paragraphs | `orphans: 3; widows: 3` — minimum 3 lines on each side of a break |
| List items | `break-inside: avoid` — individual items don't split |
| Blockquotes | `orphans: 3; widows: 3; box-decoration-break: clone` — left border repeats on every page |
| Code blocks | `break-inside: avoid` — short blocks stay together; engine overrides for tall blocks |
| Tables | `break-inside: avoid` on rows; `display: table-header-group` repeats headers |
| Horizontal rules | `break-after: avoid` — never stranded at page bottom |
| Images / figures | `break-inside: avoid` — stay with captions |
| Definition terms | `break-after: avoid` — terms stay with their definitions |

## Utility Classes

Two HTML classes are available for manual pagination control:

```html
<!-- Force a page break -->
<div class="page-break"></div>

<!-- Prevent content from splitting across pages -->
<div class="keep-together">
  Content that must stay on one page.
</div>
```

## CSS Sections

The stylesheet is organized into 25 documented sections:

| # | Section | Purpose |
|---|---------|---------|
| 1 | Design Tokens | Colors, fonts, spacing, page geometry |
| 2 | Base / Document Root | html/body setup, font smoothing |
| 3 | Writing Area | Content column width (180mm / 195mm wide) |
| 4 | Headings | h1–h6 sizing, borders, page-break rules |
| 5 | Body Text | Paragraph spacing, orphan/widow control |
| 6 | Lists | Ordered, unordered, task lists, nesting |
| 7 | Blockquotes | Left border, italic text, page-break handling |
| 8 | Inline Code | Background, border, font sizing |
| 9 | Code Blocks | 7.5pt monospace, overflow visible |
| 10 | Tables | Striped rows, border fallbacks, header repeat |
| 11 | Horizontal Rules | Styling, break-after: avoid |
| 12 | Images | max-width scaling, break-inside: avoid |
| 13 | Table of Contents | Link coloring, break-inside: avoid |
| 14 | YAML Front Matter | Dashed border, light background |
| 15 | Footnotes | Separator, reduced font size |
| 16 | Definition Lists | dt/dd, kbd, abbr, sub/sup |
| 17 | Math | MathJax/KaTeX styling |
| 18 | Diagrams | Mermaid neutral theme |
| 19 | Utility Classes | .page-break, .keep-together |
| 20 | Typora UI | Editor-specific styling |
| 21 | Sidebar & File List | Navigation panel |
| 22 | Platform Fixes | macOS, Windows, Linux adjustments |
| 23 | Print Styles | @media print overrides |
| 24 | Export Styles | PDF/HTML export adjustments |
| 25 | CodeMirror | Syntax highlighting palette |

## Installation

1. Copy `folio.css` into Typora's theme folder
   - **macOS:** `~/Library/Application Support/abnerworks.Typora/themes/`
   - **Windows:** `%APPDATA%\Typora\themes\`
   - **Linux:** `~/.config/Typora/themes/`
2. Restart Typora
3. Select **Folio** from **Preferences** > **Appearance** > **Themes**

## Testing

The file `test-folio-theme.md` is a verification suite that exercises every CSS section. Open it in Typora with the Folio theme active, then export to PDF. A checklist at the bottom of the document covers all visual checkpoints.

## Compatibility

Tested against Typora 1.5+ on:
- macOS (WebKit)
- Windows (Chromium/Electron)
- Linux (Chromium/Electron)
