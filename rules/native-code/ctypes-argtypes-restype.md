---
$schema: https://straion.com/schemas/rule/v1.json
id: ffc7f678-37a4-4844-b56e-da455439a1a9
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST declare `argtypes` and `restype` for every `ctypes` foreign function before calling it.

## Examples

```python kind=violating
lib = ctypes.CDLL("./libimg.so")
buf = lib.img_alloc(size)  # restype defaults to c_int: a 64-bit pointer is truncated
```

```python kind=compliant
lib = ctypes.CDLL("./libimg.so")
lib.img_alloc.argtypes = [ctypes.c_size_t]
lib.img_alloc.restype = ctypes.c_void_p
buf = lib.img_alloc(size)
```
