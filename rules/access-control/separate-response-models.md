---
$schema: https://straion.com/schemas/rule/v1.json
id: 71555a8c-09f4-403c-8062-082fa4637ad5
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST NOT use input or persistence models that hold secrets (password hashes, tokens, API keys, internal flags) as response models.

## Examples

```python kind=violating
@app.post("/users", response_model=UserInDB)  # UserInDB has hashed_password
def create_user(body: UserCreate): ...
```

```python kind=compliant
@app.post("/users", response_model=UserOut)
def create_user(body: UserCreate): ...
```
