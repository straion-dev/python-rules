---
$schema: https://straion.com/schemas/rule/v1.json
id: 65fe313e-8563-474e-81cc-326a53710426
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST check lengths and offsets derived from untrusted input against the real buffer size before passing them to native code (`ctypes.memmove`, `from_buffer`, cffi `ffi.memmove`, foreign functions taking a pointer and a length).

## Examples

```python kind=violating
buf = ctypes.create_string_buffer(256)
ctypes.memmove(buf, data, len(data))
```

```python kind=violating
n = int.from_bytes(header[:4], "little")
lib.decode(payload, n)  # n comes from the attacker, not from len(payload)
```

```python kind=compliant
buf = ctypes.create_string_buffer(256)
if len(data) > ctypes.sizeof(buf):
    raise ValueError("payload too large")
ctypes.memmove(buf, data, len(data))
```

```python kind=compliant
n = int.from_bytes(header[:4], "little")
if n > len(payload):
    raise ValueError("declared length exceeds payload")
lib.decode(payload, n)
```
