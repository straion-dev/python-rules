---
$schema: https://straion.com/schemas/rule/v1.json
id: 35b9628c-abe3-4fcb-bec5-4611507e6b98
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST check pointers returned by native functions for NULL before dereferencing them or passing them to other native calls.

## Examples

```python kind=violating
ctx = lib.ctx_new()
lib.ctx_load(ctx, data, len(data))
```

```python kind=compliant
lib.ctx_new.restype = ctypes.c_void_p
ctx = lib.ctx_new()  # NULL comes back as None
if not ctx:
    raise MemoryError("ctx_new failed")
lib.ctx_load(ctx, data, len(data))
```
