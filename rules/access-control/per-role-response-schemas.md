---
$schema: https://straion.com/schemas/rule/v1.json
id: 87619efd-ab90-4cc6-9f29-5524b1d84724
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST choose the response schema from the caller's permissions when field visibility differs by role.

## Examples

```python kind=violating
return UserAdminOut.model_validate(user)  # email and last_login_ip returned to every caller
```

```python kind=compliant
schema = UserAdminOut if current_user.is_admin else UserPublicOut
return schema.model_validate(user)
```
