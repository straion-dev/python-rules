---
$schema: https://straion.com/schemas/rule-collection/v1.json
id: d066abd6-7b00-4ddc-92dd-cfb3beb70586
name: Memory Safety in Native Code
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

CWE Top 25 memory-safety weaknesses (out-of-bounds read and write, buffer overflows, use-after-free, NULL pointer dereference) where Python code reaches native memory: ctypes and cffi bindings, Cython, NumPy views and native dependencies.
