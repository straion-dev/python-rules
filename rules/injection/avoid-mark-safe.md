---
$schema: https://straion.com/schemas/rule/v1.json
id: 0257f30d-c511-4a6e-a836-854f97236de0
meta:
  tags:
    - security
provenance:
  updatedBy: <straion>
---

MUST NOT apply `|safe`, `Markup()` or `mark_safe()` to user-influenced content anywhere except inside the project's single sanitizing helper (`render_user_html`).

## Examples

```python kind=violating
mark_safe(f"<b>{comment.author}</b>")
```

```html kind=violating
{{ post.body_html|safe }}
```

```python kind=compliant
format_html("<b>{}</b>", comment.author)
```

```python kind=compliant
return render_template("post.html", body=render_user_html(post.body))
```
