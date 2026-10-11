# rushdown-math

Render LaTeX math in a rushdown document as KaTeX markup. Formulas are typeset by [katex-rs](https://github.com/katex-rs/katex-rs), a port of [KaTeX](https://katex.org) written in Rust, while the document is rendered.

Three notations are recognised:
- `$…$` for inline formula,
- `$$...$$` or `\`\`\`math ... \`\`\`` for block formula.

## Usage

Add the crate via `cargo add rushdown-math` and include it within your rushdown parser

```rust
use rushdown::new_markdown_to_html;
let parser = new_markdown_to_html(
    Default::default(),
    Default::default(),
    rushdown_math::math_parser_extension(),
    rushdown_math::math_html_renderer_extension(),
);
let mut html = String::new();
parser(&mut html, "Energy is $E = mc^2$.").unwrap();
assert!(html.contains(r#"<span class="katex">"#));
```

Don't forget to include the KaTeX stylesheet for better results.

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@latest/dist/katex.min.css" crossorigin="anonymous">
```
