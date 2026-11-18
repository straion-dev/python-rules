---
$schema: https://straion.com/schemas/rule/v1.json
id: 8b073ad1-eef8-4cd6-ab42-06c26aa5059b
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST NOT disable Cython `boundscheck` or `wraparound` in code that indexes with values derived from untrusted input.

## Examples

```python kind=violating
import cython

@cython.boundscheck(False)
@cython.wraparound(False)
def read_field(buf: cython.uchar[:], offset: cython.Py_ssize_t):
    return buf[offset]  # offset from the file header: out-of-bounds read
```

```python kind=compliant
import cython

def read_field(buf: cython.uchar[:], offset: cython.Py_ssize_t):
    return buf[offset]  # bounds-checked: raises IndexError
```
