---
$schema: https://straion.com/schemas/rule/v1.json
id: 06413c53-8a2f-44c7-b1fd-d0fe3cbbf60f
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST pass server data into inline `<script>` blocks with Jinja2 `|tojson` or Django `json_script`, never by interpolating template variables or `json.dumps` output into JavaScript.

## Examples

```html kind=violating
<script>
  const search = '{{ query }}';           {# HTML escaping is not JavaScript escaping #}
  const items = {{ items_json|safe }};    {# json.dumps does not escape </script> #}
</script>
```

```python kind=violating
html = f"<script>const cfg = {json.dumps(cfg)};</script>"
```

```html kind=compliant
<script>
  const search = {{ query|tojson }};
  const items = {{ items|tojson }};
</script>
```

```html kind=compliant
{{ user_data|json_script:"user-data" }}
<script>
  const user = JSON.parse(document.getElementById("user-data").textContent);
</script>
```
