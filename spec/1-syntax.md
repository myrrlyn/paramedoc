# Paramedoc Syntax

Paramedoc, like Markdown, is designed to be primarily plaintext, with markup and
structure provided by in-band punctuation symbols. Like Markdown and HTML, it
has two kinds of content: *block* and *flow*. A Paramedoc document is composed
of one ore more *blocks*, each of which contains either one or more *blocks*, or
one or more *flows*. A flow cannot contain a block.

## Paragraph Text

The simplest Paramedoc document contains no structural tokens; only undecorated
text. This paragraph is such an example: it has text, including punctuation that
is part of the natural language, but no markup. Even the colon in the previous
sentence, which can serve as a structural token, has no effect here.

In the absence of any other directives, a run of text becomes enclosed in an
HTML paragraph, `<p>`. A paragraph is terminated by two newlines.

```pmd
paragraph one
continues here

this is paragraph two
```

```html
<p>paragraph one continues here</p>
<p>this is paragraph two</p>
```

## Flow Content

Flow content occurs within a run of text. There can be any number of flow items
within text, and some of them can nest. Some examples are `*emphasis*`,
`[links](/)`, and `"quotes"`.

## Block Content

As with Markdown, Paramedoc has two kinds of block syntax: delimited and
prefixed. Delimited blocks use an opening and a closing token, each of which
must appear on their own line, separated from other blocks by two newlines.
Prefixed blocks use one or more tokens at the beginning of the line. Content
which requires multiple lines *should* repeat the prefix on each new line, but
a block is only *required* to terminate at two newlines, or if the prefix
changes.

## Whitespace and Newlines

Paramedoc is visually-structured. It expects to be legible both as itself and as
HTML. As such, it allows the use of newlines and indentation as both unsemantic
visual arrangement and semantically-meaningful document control.

A single newline character has no effect on the document structure, and will be
replaced with a single space in the output. Similarly, a run of any number of
spaces (including a newline-replacement) are collapsed to a single space in the
output.

Because single newlines are equivalent to spaces, flow elements are permitted to
cross lines:

```pmd
this *emphasized
text* is one span
```

```html
<p>this <em>emphasized text</em> is one span</p>
```

This tolerance also extends to Paramedoc literals, described next.

## Literals

Within the context of Paramedoc control text (described later), a long string
may be indicated to be a single token by using `<{content}>` or `"{content}"`.
