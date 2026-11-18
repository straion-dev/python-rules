---
$schema: https://straion.com/schemas/rule/v1.json
id: 8168039f-a7fb-4a2f-ba80-0276dc622231
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST scan dependencies for known vulnerabilities (e.g. `pip-audit`) in CI and fail the build on findings that are not explicitly accepted.

## Examples

```bash kind=compliant
pip-audit --requirement requirements.txt
```

```bash kind=violating
pip-audit --requirement requirements.txt || true
```
