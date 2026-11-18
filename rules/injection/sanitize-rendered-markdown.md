---
$schema: https://straion.com/schemas/rule/v1.json
id: 0633d9c1-c7f8-42ff-b017-930bd0403699
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST render user-supplied Markdown through the project's sanitizing helper (`render_user_html`) so the generated HTML is cleaned by an allowlist sanitizer (e.g. `nh3`).

## Examples

```python kind=violating
body = Markup(markdown.markdown(post.body))  # raw HTML and javascript: links pass straight through
```

```python kind=compliant
def render_user_markdown(raw: str) -> Markup:
    return render_user_html(markdown.markdown(raw))
```
