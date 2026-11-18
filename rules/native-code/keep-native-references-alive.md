---
$schema: https://straion.com/schemas/rule/v1.json
id: a6d4df9c-6506-4c84-ade0-6bf82d44e60b
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST keep a Python reference to every `ctypes`/`cffi` callback, buffer or object passed to native code for as long as the native side may use it.

## Examples

```python kind=violating
lib.set_handler(HANDLER(on_event))  # the callback object is garbage-collected while C still holds it
```

```python kind=violating
lib.set_name(ctypes.create_string_buffer(name.encode()))  # C stores the pointer; the buffer is freed after the call
```

```python kind=compliant
self._on_event = HANDLER(on_event)
lib.set_handler(self._on_event)
```
