# Definition Lists

A flow element consisting of `:{term}: {definition}` expands to a `<dt>`/`<dd>`
pair. All neighboring `<dt>`/`<dd>` pairs are grouped into a `<dl>` enclosure.

```pmd
:{term}: {definition}

:{with spaces}: {longer definition
  on multiple lines, indented}

:{last}: {this definition

  has two paragraphs}
```

```html
<dl>
  <dt>{term}</dt>
  <dd>{definition}</dd>

  <dt>{with spaces}</dt>
  <dd>{longer definition on multiple lines, indented}</dd>

  <dt>{last}</dt>
  <dd>
    <p>{this definition</p>
    <p>has two paragraphs}</p>
  </dd>
</dl>
```
