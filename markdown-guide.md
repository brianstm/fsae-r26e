---
layout: default
title: Markdown Guide (In‑Depth)
---

# Markdown Guide (In‑Depth)

This page is a deeper reference for writing content in Markdown as used by Jekyll (kramdown with GitHub‑Flavored Markdown features).

## Front matter

Every page can start with YAML front matter:

```yaml
---
layout: default
title: My Page
permalink: /my-page/
---
```

## Headings

```md
# H1

## H2

### H3

#### H4

##### H5

###### H6
```

## Emphasis and inline elements

```md
**bold** and **bold**
_italic_ and _italic_
~~strikethrough~~
`inline code`
```

## Paragraphs and line breaks

- Blank lines create new paragraphs.
- End a line with two spaces for a line break.

## Lists

Unordered:

```md
- Item A
- Item B
  - Nested B1
```

Ordered:

```md
1. First
2. Second
   1. Nested
```

Definition lists (kramdown):

```md
Term
: Definition text
```

## Links and images

```md
[Link text](https://static.wixstatic.com/media/27f4c4_8cb03475d7aa46ad980284ee333d5736~mv2.jpg/v1/fill/w_640,h_784,al_c,q_85,usm_0.66_1.00_0.01,enc_avif,quality_auto/27f4c4_8cb03475d7aa46ad980284ee333d5736~mv2.jpg)
[Relative link]({{ "/path/" | relative_url }})
![Alt text](/assets/fsae.avif)
```

Reference-style links:

```md
[Example][ex]

[FSAE]: https://www.nusformulasae.com/ "NUS FSAE"
```

## Code blocks

Fenced:

````md
```javascript
function hi() {
  console.log("hi");
}
```
````

````

Indented (4 spaces) also works but fenced is recommended.

## Tables

```md
| Name | Value |
| ---- | ----- |
| A    | 1     |
| B    | 2     |
````

Alignment:

```md
| Left | Center | Right |
| :--- | :----: | ----: |
| a    |   b    |     c |
```

## Blockquotes

```md
> Quote level 1
>
> > Nested quote
```

## Task lists (GFM)

```md
- [x] Done
- [ ] Todo
```

## Footnotes (kramdown)

```md
Here is a footnote reference[^1].

[^1]: Footnote text.
```

## Math (kramdown + MathJax)

Inline: `$x = a/b$`

Block:

```md
$$
E = mc^2
$$
```

## Callouts/Admonitions (simple)

Use blockquotes and bold labels:

```md
> **Note**: Remember to set `baseurl` for project sites.
```

## Includes and Liquid basics

Variables and filters:

```md
Site title: {{ site.title }}
Current year: {{ "now" | date: "%Y" }}
```

Links respecting baseurl:

```md
[Home]({{ "/" | relative_url }})
```

Conditionals/loops:

```md
{% assign items = site.pages | where: "layout", "default" %}
{% for p in items %}

- [{{ p.title }}]({{ p.url | relative_url }})
  {% endfor %}
```

## Images: paths and optimization

- Prefer relative paths plus `relative_url` for internal links.
- Use compressed images (WebP/AVIF/optimized PNG/JPEG) for faster pages.

## Common Mistakes

- Broken links: use `{{ "/path/" | relative_url }}`.
- Wrong baseurl: check `_config.yml` for project vs user site.
- Unclosed code fences cause rendering issues.
