---
$schema: https://straion.com/schemas/rule/v1.json
id: e46577a9-cb0d-4f83-9217-2145ff6c5d9d
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST quote every HTML attribute value that contains a template variable.

## Examples

```html kind=violating
<input name="q" value={{ query }}>  {# a space in query injects attributes: x onfocus=alert(1) autofocus #}
```

```html kind=compliant
<input name="q" value="{{ query }}">
```
