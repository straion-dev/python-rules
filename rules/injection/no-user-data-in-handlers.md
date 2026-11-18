---
$schema: https://straion.com/schemas/rule/v1.json
id: 4d646e58-88c9-47a1-89ec-0e8a47766811
meta:
  tags:
    - security
  languages:
    - python
provenance:
  updatedBy: <straion>
---

MUST NOT render user-influenced values into `on*` event-handler attributes, `style` attributes or `<style>` blocks; pass them through `data-*` attributes and read them from JavaScript.

## Examples

```html kind=violating
<button onclick="openItem('{{ item.name }}')">Open</button>  {# the browser decodes &#39; before the handler runs #}
```

```html kind=violating
<div style="background: {{ profile.color }}">
```

```html kind=compliant
<button class="open-item" data-name="{{ item.name }}">Open</button>
<script>
  document.querySelectorAll(".open-item").forEach((b) =>
    b.addEventListener("click", () => openItem(b.dataset.name)));
</script>
```
