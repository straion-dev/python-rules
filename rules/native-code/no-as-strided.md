---
$schema: https://straion.com/schemas/rule/v1.json
id: 84c2b196-3936-4879-ab5f-a0652020ccbc
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST NOT call `numpy.lib.stride_tricks.as_strided` with shapes or strides derived from untrusted input; use `sliding_window_view` instead.

## Examples

```python kind=violating
view = as_strided(arr, shape=(n, window), strides=(arr.strides[0], arr.strides[0]))
```

```python kind=compliant
view = sliding_window_view(arr, window)
```
