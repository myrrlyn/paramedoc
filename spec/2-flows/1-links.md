# Hyperlinks

The basic hyperlink syntaxes are taken directly from CommonMark. Hyperlinks must
have a destination URL, and _may_ have a descriptive title.

## Bare URLs

```pmd
<{url}>
```

```html
<a href="{url}">{url}</a>
```

This conflicts with inline HTML. If an angle-bracketed string looks like an HTML
tag, the parser _may_ choose to emit a diagnostic, or _may_ emit the HTML tag,
but _should_ only emit a hyperlink. Paramedoc has its own syntax for production
of HTML tags. Do not presume that writing HTML directly will work.

## Inline Links

- ```pmd
  [{content}]({url})
  ```

  ```html
  <a href="{url}">{content}</a>
  ```

- ```pmd
  [{content}]({url} "{title}")
  ```

  ```html
  <a href="{url}" title="{title}">{content}</a>
  ```

## Reference Links

These links consist of two parts: a _usage site_ and a _definition site_. Many
usage sites can refer to the same definition. The definition may be anywhere in
the document, before or after any of its usages.

Usages can be _explicit_ or _implicit_:

- Explicit:

  ```pmd
  [{content}][{key}]

  [{key}]: {url}
  ```

  ```html
  <a href="{url}">{content}</a>
  ```

- With title:

  ```pmd
  [{content}][{key}]

  [{key}]: {url} "{title}"
  ```

  ```html
  <a href="{url}" title="{title}">{content}</a>
  ```

- Implicit: if no key is given, then the content is used as the key.

  ```pmd
  [{content}]

  [{content}]: {url} "{title}"
  ```

  ```html
  <a href="{url}" title="{title}">{content}</a>
  ```

- Additionally, the URL and optional title may be on following lines, if they
  are indented by two spaces as a continuation:

  ```pmd
  [{content}][{key}]

  [{key}]:
    {url}
    "{title}"
  ```

The `[{key}]:` syntax only produces a link definition if it is the first item on
its line, **and** it has a URL following it. The URL _should_ be bare, but _may_
be enclosed in angle brackets. An angle-bracketed URL may extend across multiple
lines, in which case the lines are joined with the interleaving whitespace
removed.
