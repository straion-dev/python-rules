---
$schema: https://straion.com/schemas/rule/v1.json
id: 2b582bf3-1c35-4262-909a-67e7484581b8
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST reject SVG, HTML and XML files in uploads that expect images or documents.

## Examples

```python kind=violating
ALLOWED = {"image/png", "image/jpeg", "image/svg+xml"}  # SVG can carry <script>
```

```python kind=compliant
ALLOWED = {"image/png", "image/jpeg", "image/webp"}
mime = magic.from_buffer(upload.stream.read(2048), mime=True)
if mime not in ALLOWED:
    raise ValidationError("unsupported file type")
```
