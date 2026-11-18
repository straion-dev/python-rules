---
$schema: https://straion.com/schemas/rule/v1.json
id: 2b7400e0-edc7-4938-9a3f-5832b9552be9
meta:
  tags:
    - security
provenance:
  updatedBy: <straion>
---

MUST sanitize user-supplied rich HTML with an allowlist sanitizer (e.g. `nh3`) inside one project helper that returns `Markup`, and call it at render time rather than storing pre-sanitized HTML.

## Examples

```python kind=compliant
def render_user_html(raw: str) -> Markup:
    return Markup(nh3.clean(raw))  # the only place user HTML is marked safe
```

```python kind=compliant
return render_template("post.html", body=render_user_html(post.body))
```

```python kind=violating
post.body = nh3.clean(form.body)  # sanitized on save, later rendered with |safe
post.save()
```
