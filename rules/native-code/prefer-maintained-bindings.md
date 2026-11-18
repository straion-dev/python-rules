---
$schema: https://straion.com/schemas/rule/v1.json
id: 6a4ef0ef-8c10-4614-9fc2-2ebbebb14473
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

SHOULD NOT write new `ctypes` or `cffi` bindings for code that processes untrusted input when a maintained Python package covers the need.

## Examples

```python kind=violating
libxml = ctypes.CDLL("libxml2.so.2")
doc = libxml.xmlReadMemory(body, len(body), None, None, 0)
```

```python kind=compliant
from defusedxml.ElementTree import fromstring

doc = fromstring(body)
```
