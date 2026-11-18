---
$schema: https://straion.com/schemas/rule/v1.json
id: 379700bd-33d3-4a73-bc97-1e67be8fcf7a
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST list serializer fields explicitly; MUST NOT use `fields = "__all__"` or `exclude` on serializers whose output is returned to clients.

## Examples

```python kind=violating
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = "__all__"
```

```python kind=violating
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        exclude = ["password"]  # every new column is exposed automatically
```

```python kind=compliant
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ["id", "username", "date_joined"]
```
