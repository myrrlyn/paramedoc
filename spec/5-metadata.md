# Document Metadata

A de-facto standard convention has emerged to use a structured *frontmatter*,
usually but not necessarily YAML, to allow a document to describe itself.
Paramedoc formalizes this: if the first non-comment, non-whitespace characters
in a document are three or more hyphens followed by a newline, then the parser
scans for another sequence of newline, that same number of hyphens, newline, and
begins processing after the terminator. The parser will save the interior
content of the frontmatter section as-is. An HTML emitter must attempt to parse
it as *at least one* data language, but Paramedoc does not specify what that
language needs to be.

An HTML emitter which has successfully parsed a frontmatter content *may* choose
to emit `<meta>` tags for them, but this is not required.

## Paramedoc

```pmd
---
title: Sample Text
author: myrrlyn
---

Paragraph text
```

```html
<meta name="title" content="Sample Text" />
<meta name="author" content="myrrlyn" />
<p>Paragraph text</p>
```

## Relation to Document Structure

Paramedoc strongly encourages each document to have as its first content an
`<h1>` heading acting as the document title. If the frontmatter contains a title
key, *and* the document does not contain an `# {H1 Heading}\n`, then the HTML
emitter may print `<h1>{frontmatter title value}</h1>` before the rest of the
processed document. If the document does contain an `<h1>` element, then the
frontmatter title is not printed in the output.

## Variable Substitution

Paramedoc reserves the syntax `@{{identifier}}` to denote substitution sites.
This syntax is not used anywhere else in the language, and is transparent to the
parser. HTML emitters *should* use any discovered substitution identifiers as
lookup sequences for the frontmatter, and replace the entire substitution key
with its frontmatter value, if discovered. If no value is discovered, then the
text should remain as-is.

Paramedoc does not specify how to interpret the identifier syntax. The most
common syntax is JSON object-traversal: `parent.child[array-item]`. Paramedoc
also does not specify how an HTML emitter

```pmd
---
authors:
  - myrrlyn <self@myrrlyn.net>
  - you <reader@myrrlyn.net>
---


```

[Phoenix]: https://phoenixframework.org
