---
$schema: https://straion.com/schemas/rule/v1.json
id: 404256a5-c0f2-4a49-a5a7-bc0ab670bc65
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST serialize API responses through an explicit output schema that lists the returned fields; MUST NOT return ORM objects, `__dict__`, `model_to_dict()` or `.values()` directly.

## Examples

```python kind=violating
def get_user(request, uid):
    return JsonResponse(model_to_dict(User.objects.get(pk=uid)))  # includes password hash and internal flags
```

```python kind=compliant
class UserOut(BaseModel):
    id: int
    display_name: str

@app.get("/users/{uid}", response_model=UserOut)
def get_user(uid: int, db: Session = Depends(get_db)):
    return db.get(User, uid)
```
